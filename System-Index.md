Compiled programs in C and C++ typically have a lib/ directory and often also a bin/ directory.

On **GoboLinux**, these will be symlinked into /System/Index such as for ping:

    /System/Index/bin/ping  
    /System/Index/lib/libpng.so.3  

Traditional Unix paths are also symlinks to the /System/Index directory structure:

    /bin     -> /System/Index/bin  
    /usr/bin -> /System/Index/bin  
    /usr/lib -> /System/Index/lib  
    /etc     -> /System/Settings

