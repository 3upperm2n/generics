LDG
===

NVIDIA GPUs of CUDA compute capability 3.5 and greater, such as the
[Tesla
K20](http://www.nvidia.com/object/personal-supercomputing.html),
support `__ldg()`, an intrinsic that loads through the read-only
texture cache, and can improve performance in some circumstances.
CUDA provides overloads of `__ldg()` for some built-in types:

`char`, `short`, `int`, `long long`, `int2`, `int4`, `unsigned
char`, `unsigned short`, `unsigned int`, `unsigned long long`,
`uint2`, `uint4`, `float`, `double`, `float2`, `float4`, `double2`.

However, for all other types, including user defined types, the native
overloads of `__ldg()` are insufficient.  To solve this problem, this
library provides a single template:

    template<typename T> __device__ T __ldg(const T*);

This template allows data of any type to be loaded using `__ldg`. The
only restriction on `T` is that it have a default constructor.

Usage
=====

To use this library, simply `#include <ldg/ldg.h>`.  
The `__ldg()` overloads provided natively by CUDA will be used if `T`
is natively supported.  If not, the template will be used.

See
[test.cu](http://github.com/BryanCatanzaro/ldg/blob/master/test/test.cu)
for an example.

