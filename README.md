## �ο�
1. [`FreeRTOS_with_SystemView`](https://wiki.segger.com/FreeRTOS_with_SystemView)

## ˵��
1. ������ʹ��`RTT`������־����Լ�`SystemView`�¼����٣�
2. ������ͨ��`CubeMX`���ɵ�`FreeRTOS`��ش���汾Ϊ`FreeRTOS V10.3.1`��
3. ������ʹ����[`dbger`](https://github.com/ShadowThree/dbger.git)��[`SystemView`](https://github.com/ShadowThree/SystemView.git)��

## ʹ��
1. ͨ��`git submodule add https://github.com/ShadowThree/SystemView.git ThirdUtils/SystemView`��ӱ���Ŀ������ָ��Ŀ¼��
2. �������ͷ�ļ�·�������̣�
```c
../ThirdUtils/SystemView/FreeRTOS_V10.3.1_portable_RVDS_ARM_CM4F_SystemView_FreeRTOS10_Patch    // ������ӵ� FreeRTOS ���ͷ�ļ�֮ǰ
../ThirdUtils/SystemView/Config
../ThirdUtils/SystemView/Sample/FreeRTOSV10     // ��Ϊ FreeRTOS Դ��汾Ϊ V10.3.0������ѡ�����
../ThirdUtils/SystemView/SEGGER
```
3. �������Դ�ļ������̣�
```c
ThirdUtils\SystemView\FreeRTOS_V10.3.1_portable_RVDS_ARM_CM4F_SystemView_FreeRTOS10_Patch\port.c
ThirdUtils\SystemView\FreeRTOS_V10.3.1_portable_RVDS_ARM_CM4F_SystemView_FreeRTOS10_Patch\tasks.c
ThirdUtils\SystemView\Sample\FreeRTOSV10\SEGGER_SYSVIEW_FreeRTOS.c
ThirdUtils\SystemView\Sample\FreeRTOSV10\Config\Cortex-M\SEGGER_SYSVIEW_Config_FreeRTOS.c
ThirdUtils\SystemView\SEGGER\SEGGER_RTT.c
ThirdUtils\SystemView\SEGGER\SEGGER_SYSVIEW.c
```
4. ��`MDK keil`ѡ�������ļ� --> �һ� --> `Options for File`��ȥ��`Include in Target Build`ǰ��Ĺ���
```c
Middlewares/FreeRTOS/tasks.c        // �� SystemView �е� Patch �ļ��޸���
Middlewares/FreeRTOS/port.c         // �� SystemView �е� Patch �ļ��޸���
LOG/SEGGER_RTT.c                    // �� SystemView ���ã��� SystemView �Ѿ������
```
5. ��`FreeRTOSConfig.h`����������ͷ�ļ���
```c
#include "SEGGER_SYSVIEW_FreeRTOS.h"
```
6. ��`MDK keil`��ħ���� --> `C/C++` �й�ѡ`GNU extensions`��
7. ��`main.c`�е���`SEGGER_SYSVIEW_Conf();`����`SystemView`;
8. �������أ���`SystemView`����������ռ��ɣ�

## ע��
1. ֻ����`ARM Compiler V5`����ֲ��
2. ��`SEGGER_SYSVIEW_Conf.h`��������¶��壺
```c
#define SEGGER_SYSVIEW_CORE SEGGER_SYSVIEW_CORE_CM3
```
3. ��`FreeRTOS`��ʼ����֮ǰ��ִ�����´��룺
```c
// �� RTOS �����У�ֻ��Ҫ Conf ����
SEGGER_SYSVIEW_Conf();

// ��������ֻ���ڷ� RTOS �����²���Ҫ
// SEGGER_SYSVIEW_Start();
// SEGGER_SYSVIEW_OnIdle();
```