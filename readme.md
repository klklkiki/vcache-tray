# VCACHE-TRAY

A tray utility to control dynamic CCD preference of heterogeneous AMD 3D V-Cache CPUs like 7950x3D and 7900x3D. Some privileged games ~~(aka. GenSh1t )~~ and programs are refused to set affinity, this utility may help to overcome this case to schedule these bad behaved programs to preferred CCD.

![](./asset/preview.png)

### Requirements

- Recommended to install **latest** BIOS and AMD chipset driver.
  - At least BIOS and drivers which support 7000x3D CPUs.
- Option `CPPC Dynamic Preferred Cores` in BIOS menu `AMD CBS/SMU` must be set to `AUTO` or `Driver` to allow OS control via `AMD 3D V-Cache Performance Optimizer` device
  - Otherwise this device will not work and appear in Device Manager.
- Recommend to turn off `Game Mode` and `xbox Game Bar` in Windows, since you are gonna use this utility to control CCD preferences and profiles manually.



### Note

- ⚠ On ASUS Proart-x670E, BIOS 1202, if `Max Clock Limit` is enabled in `PBO` menu, both BIOS and driver `CPPC prefer CCD` function will not work properly, dunno why.
- ⚠ Recommend switch the prefer CCD or setup profile before starting new program, it looks like some activated threads will stick on original CCD until they are terminated.
- ⚠ `Prefer CCD` may not affect programs or threads that have been set a affinity by themselves or manually.
- ⚠ Only tested on Windows 10 yet.



### How to use

Run it and switch modes via tray icon.

To start with Windows, add a task in `Task Scheduler`.

Pass `-h` to check more options, `--alloc_console` to check debug logs.



### How does it work

While I was investigating 3D V-Cache driver and planning to take over control of device, but I found that AMD leaved a registry interface `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\amd3dvcache\Preferences` to allow change things on the fly. It will take a **while**, like, up to serval minutes to take effect without restarting the 3dvcache service. That's it, this program is just a simple frontend of these registry interfaces.



### Build

Build with msys2 and cmake.

