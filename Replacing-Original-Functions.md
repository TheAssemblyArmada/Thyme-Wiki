This is a guide to replacing one of the original games functions with a replacement you (or someone else) has written. Why do we want to replace the original functions you ask? Well for one it gives us a way to verify the functionality of our own re-implementations. It also allows us to alter the functionality of the game if our replacement does something different.

The exact method we are going to use depends on the type of function we are replacing. In C++ for our purposes we are looking at 2 different types of functions that can be replaced or "hooked" with the system we have in place.

#### Types of Functions.
The two types of functions we can hook are standard "free" functions and class "methods". The difference is that methods get passed a hidden pointer to the class they operate on and use the "thiscall" calling convention while free functions generally use the "cdecl" calling convention and do not have a hidden pointer to a class passed to them. Methods in a class marked as "static" can be considered "free" functions for the purposes of replacing them. For more information on calling conventions, see this [Wikipedia](https://en.wikipedia.org/wiki/X86_calling_conventions) page.

#### Unhookable Functions
Our hooking system is fairly simple, it basically replaces the address of a function (basically where the game knows to look to run or "call" a function) with another one. However this only works if you can get the address of the old function you want to replace and the new function you want to replace it with.

For the old address that is fairly straightforward if you can use a disassembler such as IDA or Ghidra to examine the original binary and pinpoint where a function of interest starts. For the new address it should be easy, after all you have written the code right? Wrong as Visual Studio will not let you get the raw address of certain functions, namely virtual functions and class constructors/destructors. To hook these we need to wrap them in standard class methods that we can get the address of as in the following example:

```C
#include <new> // For placement new to call the constuctor from a method.
class W3DFileSystem : public FileFactoryClass
{
public:
    W3DFileSystem();
    virtual ~W3DFileSystem();

    virtual FileClass *Get_File(const char *filename) override;
    virtual void Return_File(FileClass *file) override;

#ifdef GAME_DLL // This define is only set when building a hooking DLL.
    // Wrap a placement new call which will invoke the ctor on the "this" pointer
    W3DFileSystem *Hook_Ctor() { return new(this) W3DFileSystem; }

    // Wrap destructor by invoking it directly.
    void Hook_Dtor() { W3DFileSystem::~W3DFileSystem; }

    // Wrap a virtuals by calling them explicitly to get direct calls.
    FileClass *Hook_Get_File(const char *filename) { return W3DFileSystem::Get_File(filename); }
    void Hook_Return_File(FileClass *file) { W3DFileSystem::Return_File(file); }
#endif
};
```

With this we now have methods that we can hook that will call the ones we can't for us.

#### Hooking functions.
All functions are hooked from a single function called "Setup_Hooks" with different .cpp files to implement it depending on which program the dll is intended to be injected into. They are found in the source tree at src/hooker/setuphooks_*.cpp. The one that hooks the game binary is setuphooks_zh.cpp.

In the body of the Setup_Hooks function you will see calls like the following:
```
Hook_Function(0x004469C0, FileSystem::Are_Music_Files_On_CD); // This one is part of the CD Check.

Hook_Method(0x00446770, &FileSystem::Get_File_List_From_Dir);
```

The Hook_Function and Hook_Method functions take an integer which represents the address of the orignal function to replace and the function you want to replace it with. For hooking class methods, the leading & before the function name to get a member function pointer is mandatory, but is optional for static member functions and free functions.
