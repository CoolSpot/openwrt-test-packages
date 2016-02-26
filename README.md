# openwrt-test-packages
OpenWRT packages feed for test cases for issues I discovered in OpenWRT.

## throw-catch-sigsegv
I believe uClibc++ incorrectly implements C++ exception ABI, allocating not enough memory in the "__cxxabiv1::__cxa_allocate_exception" .  
That causes memory corruption (buffer overflow) inside "__cxxabiv1::__cxa_throw".  
When binary is compiled for OpenWRT's musl standard library, the program crashes with SIGSEGV in the "free" call from "__cxxabiv1::__cxa_free_exception" because musl is very sensitive for memory corruption.

### Installing the feed
```
cd ~/Documents/openwrt
echo "src-git openwrttest https://github.com/coolspot/openwrt-test-packages.git" >> ./feeds.conf
./scripts/feeds update openwrttest
./scripts/feeds install -a -p openwrttest
```

### Building the package
```
make menuconfig
\# In the menuconfig select the package Test/sub-test/throw-catch-sigsegv to be built
make package/throw-catch-sigsegv/install
\# Copy the package on the device (or VM)
scp ./bin/malta/packages/openwrttest/throw-catch-sigsegv_2016-02-25_malta_mips.ipk qemu:/tmp/
\# on the device (or VM)
root@OpenWrt:~# opkg install /tmp/throw-catch-sigsegv_2016-02-25_malta_mips.ipk
```

### Contact me
Ivan Kold \<openwrt at coolspot.33mail.com\>
