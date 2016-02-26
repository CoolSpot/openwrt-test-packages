# openwrt-test-packages
OpenWRT packages feed for test cases for issues I discovered in OpenWRT.

## throw-catch-sigsegv
I believe uClibc++ incorrectly implements C++ exception ABI, allocating not enough memory in the "__cxxabiv1::__cxa_allocate_exception" .
That causes memory corruption (buffer overflow) inside "__cxxabiv1::__cxa_throw". 
When binary is compiled for OpenWRT's musl standard library, the program crashes with SIGSEGV in the "free" call from "__cxxabiv1::__cxa_free_exception" because musl is very sensitive for memory corruption.

## Contact me
Ivan Kold <openwrt at coolspot.33mail.com>
