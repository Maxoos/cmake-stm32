![](images/header.png)
# CMAKE stm32F4 example 2022

NOTE: Adjusted to work on Mac os X. Before using install: arm-none-eabi-gcc
brew install arm-none-eabi-gcc

Extra resources:
 - https://github.com/Teivaz/cmake-stm32
 - https://medium.com/@erbo-engineering/using-vs-code-for-embedded-stm32-development-14405ed4ac82

**To build install:**
 * cmake and make
 * arm-none-eabi toolchain: https://xpack.github.io/blog/2020/07/03/arm-none-eabi-gcc-v9-3-1-1-1-released/
 * make sure cmake,make,arm-none-eabi-gcc are reachable from path
 * openocd 0.11.0 (https://github.com/openocd-org/openocd/tree/v0.11.0)
 * Open CmakeList and change the chip version, for exmaple to work with STM32F411 include STM32F411XE. This will inclose the correct h file BSP

**Run: without vscode magic ;)**
1. `git submodule update --init`
2. `mkdir build && cd build`
3. `cmake ..`
4. `cmake --build . -- -j 16`
5. enjoy

**Run: With vscode magic**

1. To run and forget (execute the flash task)
2. To debug F5

Fallback source:
https://dev.to/younup/cmake-on-stm32-the-beginning-3766
https://github.com/ObKo/stm32-cmake

> If you want to use an older version of openocd (0.10.0) is the one you get by the ubuntu apt archives,
> Then you need to add a different override regex in your launch.json (https://github.com/Marus/cortex-debug/issues/166)
