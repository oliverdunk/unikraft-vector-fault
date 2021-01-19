# unikraft-vector-fault

Reproduction of a page fault when storing a large vector in a Unikraft C++ program.

## Steps to reproduce

1. Clone this repository.
2. Use `kraft configure -p kvm -m x86_64` to setup the project.
3. Build with `kraft build`.
4. Run with `kraft run -p kvm`.
5. Observe a page fault.

I'm not sure if reproducing this on other machines will require more/less items in the vector.

I did try using smaller vectors or values other than strings, but it was hard to get a reproduction simpler than this one.

This also seems to only apply to static declarations, rather than vectors constructed at runtime. I did manage to get a page fault at runtime but had to add _many_ more items.

Info about the line having trouble from GDB:

```
Line 85 of "/root/unikraft-vector-fault/build/libcxx/origin/libcxx-7.0.0.src/src/iostream.cpp" starts at address 0x12b3e3 <std::__1::ios_base::Init::Init()+19> and ends at 0x12b3e7 <std::__1::ios_base::Init::Init()+23>.
```
