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

```C
int g_someGlobalVar;
typedef void(*funcptr_t)();
typedef int specialint_t;

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

#### WIP

More to come.