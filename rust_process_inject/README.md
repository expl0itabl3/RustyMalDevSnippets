# Process Injection in Rust

This code is based on the [RustyProcessInjectors](https://github.com/HuskyHacks/RustyProcessInjectors/) project by HuskyHacks.

This Rust program performs code injection into the current running process on a Windows machine. Upon execution, the `create_thread()` function goes through the following steps to inject and execute the shellcode:
1. It starts by allocating a region in the current process's memory using the `VirtualAlloc` function, thereby creating a space for the shellcode.
2. The shellcode is then copied into this newly allocated memory space using `std::ptr::copy_nonoverlapping()`.
3. To ensure the shellcode can be executed but not further modified, the memory region's protection is altered from `PAGE_READWRITE` to `PAGE_EXECUTE_READ` using the `VirtualProtect` function.
4. Utilizing the `CreateThread` function, a new thread is created in the current process, which begins its execution at the start of the injected shellcode.
5. Finally, the `WaitForSingleObject` function is called to pause the executing thread until the injected shellcode completes execution.

The payload itself consists of shellcode designed to launch the Windows calculator (calc.exe).
