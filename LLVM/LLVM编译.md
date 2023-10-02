# LLVM编译

``` bash
cmake -S llvm -B build -G Ninja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DLLVM_USE_LINKER=gold -DLLVM_PARALLEL_COMPILE_JOBS=4 -DLLVM_PARALLEL_LINK_JOBS=4 -DLLVM_ENABLE_ASSERTIONS=ON -DLLVM_BUILD_LLVM_DYLIB=ON
```

- -DCMAKE_BUILD_TYPE=RelWithDebInfo
    保留一定的Debug信息
- -DLLVM_USE_LINKER=gold
    使用gold作为链接器而非ld（这在编译Debug版本时可以省内存？）
- -DLLVM_PARALLEL_COMPILE_JOBS=4 -DLLVM_PARALLEL_LINK_JOBS=4
    限制并行的进程数，可以避免内存不够问题。
- -DLLVM_ENABLE_ASSERTIONS=ON
    RelWithDebInfo的类型没有断言，这里手动开启。
- -DLLVM_BUILD_LLVM_DYLIB=ON
    启动动态链接，在关闭状态下，构建项目时会采用静态链接，内存要求高。
  此外，在使用new_pm时，静态链接不要求在每一次修改后重新构建，只需要重新编译动态库即可。

