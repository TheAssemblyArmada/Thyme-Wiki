This is a guide to replacing one of the original games functions with a replacement you (or someone else) has written. Why do we want to replace the original functions you ask? Well for one it gives us a way to verify the functionality of our own re-implementations. Without replacing them one at a time, we would have to implement a significant amount of the binary to test some code. It also allows us to alter the functionality of the game if our replacement does something different.

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
```C
// Hooks a static member function, free function would be the same.
Hook_Function(0x004469C0, FileSystem::Are_Music_Files_On_CD);

// Hooks a member function.
Hook_Method(0x00446770, &FileSystem::Get_File_List_From_Dir);
```

The Hook_Function and Hook_Method functions take an integer which represents the address of the original function to replace and function pointe to the function you want to replace it with. For hooking class methods, the leading & before the function name to get a member function pointer is mandatory, but is optional for static member functions and free functions.

If you want to hook an overloaded function, where more than one function share a name, then you need to use a static cast to force the variant of the function you want to hook.

```C
// This example uses a static cast to pick which of a set of overloaded methods in the Utf8String class will be hooked.
Hook_Method(0x0040D640, static_cast<void (Utf8String::*)(char const *)>(&Utf8String::Set));
```

#### Considerations for Virtual Methods
When reimplementing a class with virtual methods, you must declare the functions in the same order they were declared in the original code such that they generate the same layout for the new virtual method pointer table compared to the old. Generally this is the same order they appear in the table in the original binaries. If you have virtual methods that are overloaded and are next to each other in the table and have the same name however, you may find that Visual Studio reverses them, thus in the original code they were the other way around.

Also note that hooking the constructor of a class with virtual methods will also replace all the virtual calls to all the virtual methods in that class at the same time. If hooking a constructor causes issues, it may be a virtual function that isn't implemented correctly and not the constructor.
