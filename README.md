# STM32F103C8T6做USB-TypeC版J-link OB 的固件与烧录工具

## 固件
hex: OB-STM32_V754_mod-2030-02-02.hex
驱动：JLink_Linux_V766a_x86_64.deb(linux) or JLink_Windows_V764c_x86_64.exe (win10)

带有 windows jlink驱动的nrf工具：
nrf-command-line-tools_10_1_1_installer_64.exe

# 注册序列号

通过J-Link Commander修改序列号
将JLINK通过USB线再次与PC机连接，打开第1步安装的JLINK驱动中的J-Link Commander，输入下面的指令“Exec SetSn = 01234567”回车确认即可

Jlink_ob注册神器_2019.rar

## swd 接线
F103C8T6版Jlink OB引脚--------------------目标EVB
PA7（TMS-SWDIO）--------------目标EVB的SWDIO
PA5（TCLK-SWCLK）------------目标EVB的SWCLK
PA1（nRESET）-------------------目标EVB的Reset
> IO 中间加 100欧电阻
> 必要时上拉470欧电阻 reset pin

## 测试程序
arduino-blink
目标板使用 stm32f103c6t6,
vscode 安装platformio插件打开工程文件夹。

## log
vscode 点击upload, 终端log 如下
```bash
RAM:   [=         ]  10.9% (used 1116 bytes from 10240 bytes)
Flash: [===       ]  32.3% (used 10580 bytes from 32768 bytes)
Building .pio/build/bluepill_f103c6/firmware.bin
Configuring upload protocol...
AVAILABLE: blackmagic, cmsis-dap, jlink, serial, stlink
CURRENT: upload_protocol = jlink
Uploading .pio/build/bluepill_f103c6/firmware.bin
SEGGER J-Link Commander V8.12f (Compiled Feb 12 2025 12:14:53)
DLL version V7.66a, compiled May 19 2022 15:17:54


J-Link Command File read successfully.
Processing script file...
J-Link>h
J-Link connection not established yet but required for command.
Connecting to J-Link via USB...O.K.
Firmware: J-Link OB-STM32F103 V1 compiled Feb  2 2030 16:45:54
Hardware version: V1.00
J-Link uptime (since boot): N/A (Not supported by this model)
S/N: -1
VTref=3.300V
Target connection not established yet but required for command.
Device "STM32F103C6" selected.


Connecting to target via SWD
InitTarget() start
InitTarget() end
Found SW-DP with ID 0x1BA01477
DPIDR: 0x1BA01477
CoreSight SoC-400 or earlier
Scanning AP map to find all available APs
AP[1]: Stopped AP scan as end of AP map has been reached
AP[0]: AHB-AP (IDR: 0x14770011)
Iterating through AP map to find AHB-AP to use
AP[0]: Core found
AP[0]: AHB-AP ROM base: 0xE00FF000
CPUID register: 0x411FC231. Implementer code: 0x41 (ARM)
Found Cortex-M3 r1p1, Little endian.
FPUnit: 6 code (BP) slots and 2 literal slots
CoreSight components:
ROMTbl[0] @ E00FF000
[0][0]: E000E000 CID B105E00D PID 001BB000 SCS
[0][1]: E0001000 CID B105E00D PID 001BB002 DWT
[0][2]: E0002000 CID B105E00D PID 000BB003 FPB
[0][3]: E0000000 CID B105E00D PID 001BB001 ITM
[0][4]: E0040000 CID B105900D PID 001BB923 TPIU-Lite
Cortex-M3 identified.
PC = 08001F58, CycleCnt = 000A5E35
R0 = 0000694F, R1 = 00000001, R2 = 40011000, R3 = 000003BF
R4 = 000003E8, R5 = 00006590, R6 = 20000704, R7 = AA205A5C
R8 = 12AC000E, R9 = C3DA2400, R10= 69349700, R11= 4660BD54
R12= 20000630
SP(R13)= 200027E0, MSP= 200027E0, PSP= 082316C0, R14(LR) = 08001F59
XPSR = 81000000: APSR = Nzcvq, EPSR = 01000000, IPSR = 000 (NoException)
CFBP = 00000000, CONTROL = 00, FAULTMASK = 00, BASEPRI = 00, PRIMASK = 00
FPU regs: FPU not enabled / not implemented on connected CPU.
J-Link>loadbin .pio/build/bluepill_f103c6/firmware.bin, 0x08000000
'loadbin': Performing implicit reset & halt of MCU.
Reset: Halt core after reset via DEMCR.VC_CORERESET.
Reset: Reset device via AIRCR.SYSRESETREQ.
Downloading file [.pio/build/bluepill_f103c6/firmware.bin]...
Comparing flash   [100%] Done.
J-Link: Flash download: Bank 0 @ 0x08000000: Skipped. Contents already match
O.K.
J-Link>r
Reset delay: 0 ms
Reset: Halt core after reset via DEMCR.VC_CORERESET.
Reset: Reset device via AIRCR.SYSRESETREQ.
J-Link>q

Script processing completed.

=================== [SUCCESS] Took 12.83 seconds ===================
```