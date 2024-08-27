## 参考
1. [`FreeRTOS_with_SystemView`](https://wiki.segger.com/FreeRTOS_with_SystemView)

## 说明
1. 本工程使用`RTT`用于日志输出以及`SystemView`事件跟踪；
2. 本工程通过`CubeMX`生成的`FreeRTOS`相关代码版本为`FreeRTOS V10.3.1`；
3. 本工程使用了[`dbger`](https://github.com/ShadowThree/dbger.git)和[`SystemView`](https://github.com/ShadowThree/SystemView.git)；

## 使用
1. 通过`git submodule add https://github.com/ShadowThree/SystemView.git ThirdUtils/SystemView`添加本项目到工程指定目录；
2. 添加如下头文件路径到工程：
```c
../ThirdUtils/SystemView/FreeRTOS_V10.3.1_portable_RVDS_ARM_CM4F_SystemView_FreeRTOS10_Patch    // 必须添加到 FreeRTOS 相关头文件之前
../ThirdUtils/SystemView/Config
../ThirdUtils/SystemView/Sample/FreeRTOSV10     // 因为 FreeRTOS 源码版本为 V10.3.0，所以选择这个
../ThirdUtils/SystemView/SEGGER
```
3. 添加如下源文件到工程：
```c
ThirdUtils\SystemView\FreeRTOS_V10.3.1_portable_RVDS_ARM_CM4F_SystemView_FreeRTOS10_Patch\port.c
ThirdUtils\SystemView\FreeRTOS_V10.3.1_portable_RVDS_ARM_CM4F_SystemView_FreeRTOS10_Patch\tasks.c
ThirdUtils\SystemView\Sample\FreeRTOSV10\SEGGER_SYSVIEW_FreeRTOS.c
ThirdUtils\SystemView\Sample\FreeRTOSV10\Config\Cortex-M\SEGGER_SYSVIEW_Config_FreeRTOS.c
ThirdUtils\SystemView\SEGGER\SEGGER_RTT.c
ThirdUtils\SystemView\SEGGER\SEGGER_SYSVIEW.c
```
4. 在`MDK keil`选中如下文件 --> 右击 --> `Options for File`，去掉`Include in Target Build`前面的勾：
```c
Middlewares/FreeRTOS/tasks.c        // 被 SystemView 中的 Patch 文件修改了
Middlewares/FreeRTOS/port.c         // 被 SystemView 中的 Patch 文件修改了
LOG/SEGGER_RTT.c                    // 和 SystemView 共用，在 SystemView 已经添加了
```
5. 在`FreeRTOSConfig.h`中引入如下头文件：
```c
#include "SEGGER_SYSVIEW_FreeRTOS.h"
```
6. 在`MDK keil`的魔术棒 --> `C/C++` 中勾选`GNU extensions`；
7. 在`main.c`中调用`SEGGER_SYSVIEW_Conf();`配置`SystemView`;
8. 编译下载，打开`SystemView`软件启动接收即可；

## 注意
1. 只能在`ARM Compiler V5`下移植；
2. 在`SEGGER_SYSVIEW_Conf.h`中添加如下定义：
```c
#define SEGGER_SYSVIEW_CORE SEGGER_SYSVIEW_CORE_CM3
```
3. 在`FreeRTOS`开始调度之前，执行如下代码：
```c
// 在 RTOS 环境中，只需要 Conf 即可
SEGGER_SYSVIEW_Conf();

// 以下两个只有在非 RTOS 环境下才需要
// SEGGER_SYSVIEW_Start();
// SEGGER_SYSVIEW_OnIdle();
```