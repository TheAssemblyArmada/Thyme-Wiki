This is the Thyme style guide.  
If you want to submit code, your pull requests will only be accepted if you follow this style.  

We provide a clang format file that can be used to apply many of the aspects of this style guide automatically, but things like variable naming you will have to follow yourself.  
We are also aware that not all the existing code may adhere fully to the guide, we'll fix this as bugs are fixed or features are added that touch these files.  

Don't submit pull requests that only fix style.

#### Why Do We Need a Style Guide?

You may ask "Why do we need a style guide"? Afterall, so long as the code is valid C/C++ it will compile and work, let's go wild.  
Three reasons, maintainability, readability and consistency.  

Parts of the style guide may seem overly verbose to seasoned programmers but we want the code to be accessible to those with less experience as well, so we insist that generally you write what you mean rather than the minimum the compiler will accept.  
You also might want to do a drive by contribution that scratches an itch for you, but then someone else needs to understand and maintain that code.  
For consistency, the actual style doesn't matter so much as the fact there is a style and every one follows it all of the time.

#### Naming Cases

These are the different casing styles that are used throughout the code. They will be referred to as these names in the rest of the guide.

* MACRO_CASE
* Capital_Case
* PascalCase
* camelCase
* concatcase
* snake_case

#### General

* C++11 is the language level the code must compile under, but only use features that aid readability or maintainability, not just to type less code and be more "productive".
* Indents use spaces, 4 spaces to be exact.
* Lines are up to 132 characters.

#### Comments

* Use '//' for comments within classes and functions, use '///' outside functions and classes to document their purpose (useful for producing documentation with doxygen).
* In general try and avoid comments after lines except for struct and class members.

#### Functions

* Functions use capital case for naming.
* Return type is on the same line as the function name.
* Functions taking no parameters should have empty parenthesis unless they are part of a file intended to follow C conventions and allow compilation with a C compiler where they have void.
* Virtual member functions declared in child classes should have the override identifier to check at compile time that they have the correct signature when they override functions in the base class.
* Function calls to functions with many parameters should be laid out like conditional scopes if the line is looking too long.
* Only use abbreviations in function names if they are likely to be well known or obvious. Not everyone will be a native English speaker.

```C
void Empty_Cpp_Function();

#ifdef __cplusplus
extern "C" {
#endif

void Empty_C_Function(void);

#ifdef __cplusplus
}
#endif

class ChildClass : public BaseClass
{
    virtual void Empty_Virtual_Function() override;
};

void Many_Param_Function(
    param1,
    param2,
    etc
);

```

#### Variables And Typedefs

* Local variables use snake case as do function parameters and plain old data (POD) struct members.
* Class member variables use camel case prefixed by "m_".
* Global variables, use camel case prefixed by "g_".
* Static class member variables use camel case prefixed by "s_".
* Static variables within a function use snake case prefixed by "_".
* Typedefs should use concat case and are suffixed with "_t".
* As with function naming, be conservative with the use of abbreviations.
* Pointer and reference operators belong to the variable, not the type and certainly not somewhere in between.

```C
int g_someGlobalVar;
typedef void(*funcptr_t)();
typedef int specialint_t;


int &g_someReference = g_someGlobalVar;
int *g_somePointer = &g_someGlobalVar;

class SomeClass
{
    int m_someMember;
    static int s_someStaticMember;
};

struct SomePODStruct
{
    int some_struct_member;
};

void Some_Function(int some_parameter)
{
    static int _some_static_var;
    int some_local_var;
}
```

#### Classes, Structs and Enums

* Named using pascal case.
* By convention, enum names are suffixed with "Type" though it isn't required.
* Enum entries are named in macro case and by convention are prefixed with some common prefix normally related to the enum name.
* If you have enums that go from 0 in an unbroken ascending order, don't bother specifying values for them, only specify where the pattern is broken.
* Leave a trailing ',' in an enum to make it easier for anyone wanting to expand it.
* Structs should only be used if you want a POD struct, if you want member functions (methods) and/or special constructors or destructors but still want members public, use a class and follow class conventions instead with a public accessor for the member variables.
* For 3D math primitives, you can use simple names such as x, y and z for a vector and have them public, but still use class rather than struct as you will likely need many methods for the class.
* Class access level descriptors are indented at the level of the class, not class members.
* Only functions that fit on one line should be declared within a class. If they are intended to be inline, but don't fit, define them outside the class as an inline function.
* If you think you might ever derive from a class, you should probably declare a virtual destructor so that the correct destructor gets called no matter what type of pointer the class is accessed from. If its to reimplement an existing class within the game, you will need to match whatever the game does until Thyme is standalone.
* Class constructor should used an initialisation list for all variables it is possible for. For long lists, one variable per line.

```C
enum SomeEnumType
{
   SOME_VALUE,
   SOME_WHATEVER,
   SOME_DUNNO,
   SOME_COUNT,
};

enum AnotherType
{
    ANOTHER_INVALID = -1,
    ANOTHER_VALUE,
    ANOTHER_TEST,
    ANOTHER_MAX = 0xFF,
};

struct SomeStruct
{
    int some_int;
    float some_float;
}

class SomeClass
{
public:
    SomeClass();
    virtual ~SomeClass() {}
    
    int Get_Member_Var() { return m_someMemberVar; }
    void Print_Stuff();
private:
    int m_someMemberVar;
}

// We want it inlined, but too big to fit in class declaration.
inline SomeClass::Print_Stuff()
{
    for (int i = 0; i < m_someMemberVar; ++i) {
        printf("%d", i);
    }
}

// Constructor defintion for lots of members in the cpp file.
LotOMembers::LotOMembers() :
    m_member1(),
    m_member2(),
    m_member3(),
    m_memberN()
{
}
```

#### WIP

More to come.