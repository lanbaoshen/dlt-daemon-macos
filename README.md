# Diagnostic Log and Trace

Derived from [COVESA/dlt-daemon](https://github.com/COVESA/dlt-daemon), 
it's only developed and tested on **Ubuntu Linux 16 64-bit & Intel PC**.

Because of my poor C/C++ coding skill and I only need run it on macOS, 
I just fix error which is raised by `cmake` or `make` during deployment and execution.   

## Environment
- Test on chip:
  - Apple Silicon

- Test on macOS version:
  - 12.2.1
  - 12.3
  - 14.2.1

## Build and install
```
cd /path/to/workspace/dlt-daemon
mkdir build
cd build
cmake ..
make
optional: sudo make install
optional: sudo ldconfig # in case you executed make install
```

## Diff
- `src/lib/dlt_user.c`:
  - Remove `pthread_setname_np` first argument
  - Remove `pthread_condattr_setclock(&attr, CLOCK_MONOTONIC);`


- `src/lib/CMakeLists.txt` & `src/daemon/CMakeLists.txt`:
  - Remove `${SOCKET_LIBRARY}`, because do not need `-lsocket` 


- `src/offlinelogstorage/dlt_offline_logstorage_behavior.c`: 
  - Remove `return -1;` in `dlt_logstorage_open_log_output_file`


- `src/console/logstorage/CMakeLists.txt`:
  - Remove `add_definitions(-Werror)`, because `daemon` is deprecated on newer macOS
