## Description:
This is a fork from [KonstaT's brilliant work](https://github.com/raspberry-vanilla/android_kernel_manifest) of Porting AOSP on Raspberry Pi 5.
The main purpose of this fork is to tinker around, explore, learn and experiment about what it take to port AOSP on any custom SoC.
[KonstaT's](https://github.com/KonstaT) work serves as a really great starting point.

### How to build:

1. Establish [Android build environment](https://source.android.com/setup/initializing) and install [repo](https://source.android.com/docs/setup/develop#installing-repo).

2. Initialize repo:

```
repo init -u https://android.googlesource.com/kernel/manifest -b common-android16-6.12-lts
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/aosp-rpi5/android_kernel_manifest/android-16.0/manifest_brcm_rpi.xml --create-dirs
```

3. Sync source code:

```
repo sync
```

4. Compile:

Raspberry Pi 5:
```
tools/bazel build --config=fast --config=stamp //common:rpi5
```

* Compiled kernel Image, dtbs, and overlays can be found in `bazel-bin/common/rpi5/arch/arm64/boot` directory.
* Replace existing files in `device/brcm/rpi5-kernel` directory of the Android source tree to include them in Android 16 build.
* You can also replace existing files in the boot partition of Raspberry Pi 5 Android 16 image.
