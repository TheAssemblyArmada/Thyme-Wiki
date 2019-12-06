This is a guide for calling one of the games original functions when it doesn't have a working reimplementation in Thyme as of yet. Mainly this should be used to provide an implementation of a function within the body of a function when reimplementing the actual replacement isn't yet feasible, though it can also be used for one off calls.

#### What Do I Need To Know
In order to call one of the original functions, you need to have worked out the address it starts at in the original binary, its calling convention, and the order of any arguments it takes, including any hidden arguments like the this pointer or pointers to structures or classes if it returns a class.

#### Creating the Call
You need to use one of the Call_* utility functions from hooker.h. These use variadic templates to ensure the correct types are passed to the called function, provided you gave the right ones to the template.

```C
// This wraps an original function call as the implementation of our own function.
void DX8Wrapper::Shutdown()
{
#ifdef GAME_DLL // Use this to only compile in hooking dll builds.
    // Use the PICK_ADDRESS macro in compilation units that will be compiled
    // for both the game and world builder binaries.
    Call_Function<void>(PICK_ADDRESS(0x00800860, 0x004F98D0));
#endif
}

// A more complicated example, this one returns a default value for standalone
// as a stub implementation for now.
w3dtexture_t DX8Wrapper::Create_Texture(
    unsigned width, unsigned height, WW3DFormat format, MipCountType mip_level_count, w3dpool_t pool, bool rendertarget)
{
#ifdef GAME_DLL
    return Call_Function<w3dtexture_t, unsigned, unsigned, WW3DFormat, MipCountType, w3dpool_t, bool>(
        PICK_ADDRESS(0x008036F0, 0x004FDF00), width, height, format, mip_level_count, pool, rendertarget);
#else
    return w3dtexture_t();
#endif
}

// An example of a call to a class method, note that the this pointer is passed.
void Render2DClass::Render()
{
#ifdef GAME_DLL
    Call_Method<void, Render2DClass>(PICK_ADDRESS(0x0080AAC0, 0x004F4980), this);
#endif
}
```
