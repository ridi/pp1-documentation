PAPER PRO (PP1) Documentation (WIP)

##Requirements

- Ubuntu 12.04 LTS
- jdk1.6.0_45


##Downloading source code

```
$ git clone --recursive git@github.com:rbx-rdm/pp1.git
```

This will also clone following submodules (via `--recursive` option) as subdirectories:
- pp1-external
- pp1-frameworks
- pp1-kernel_imx
- pp1-packages
- pp1-prebuilts


##Getting started

* Make sure `jdk1.6.0_45` is included in $PATH variable

* Install dependancies using `chk_build_env.sh` script
```
$ cd pp1
pp1$ ./chk_build_env.sh
```

* Setup build config using `build_config.sh` script
```
pp1$ ./build_config.sh nbkk52
```

##Building firmware

* Build Uboot
```
pp1$ ./build_android_img.sh uboot
```

* Build kernel
```
pp1$ ./build_android_img.sh kernel
```

* Build Android firmware
```
pp1$ ./build_android_img.sh android-{eng / userdebug / user}
```
- android-eng : adb enabled, apks are not resigned with platform key
- android-userdebug : adb enabled, apks resigned, can be rooted via `adb root`
- android-user : adb disabled, apks resigned


##Installing firmware

###Putting device in fastboot mode
1. Turn device off (Press and hold Power button for 5 seconds and press Ok or hold Power button for 10 seconds)
2. Press and hold Power button and Right PageUp button simultaneously for more than 5 seconds (LED will change from green to white)
3. Plug in micro USB cable connected to PC

###Using 'fastboot.sh all' command
1. Enter `./fastboot all`
2. Enter user password (script contains `sudo` command)
3. Connect device in fastboot mode (using instructions above)
4. Wait for installation and reboot (you may disconnect after seeing `---> Finished`)


##More materials

- List of Directories ([toc.md][toc.md])
- 

