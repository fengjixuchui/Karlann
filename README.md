
# KARLANN
## It's a kernel-based keylogger for Windows x64.
## Foreword��
**Karlann**��һ��Windows�ں˼��̼�¼��������ͨ����ʱɨ��ķ�ʽ��ȡkbdclass.sys�������ļ���Scancode������Scancodeת���ɶ�Ӧ�Ĵ�Сд�ַ���  
![Karlann](Karlann.gif)
## Description��
#### ԭ��
kbdclass.sys�������ؼ�������KeyboardClassHandleRead��KeyboardClassServiceCallback��KeyboardClassReadCopyData  
![Karlann](Karlann.jpg)  
����KeyboardClassReadCopyData�����ǽ�Scancode��kbdclass.sys�Ļ�����������IRP�У�  
���ں���KeyboardClassHandleRead��ϣ������IRP��������ReadQueue��������ֱ�Ӵӻ���������Scancode��IRP������IRP��  
���ں���KeyboardClassServiceCallback��ϣ������Scancode��������������������ֱ�ӿ�����IRP������IRP��  
��˴��������̣߳��ֱ�Ϊ��PocDequeueReadThread��PocReadCopyDataThread��PocMoveDatatoIrpThread��  
**PocDequeueReadThread**�����ڴ�kbdclass��IRP����ReadQueue������IRP����ֹKeyboardClassServiceCallback���IRP��  
**PocReadCopyDataThread**�����ں�KeyboardClassServiceCallback�������²����������Scancode���ݴ浽TempBuffer�У���ֹKeyboardClassHandleRead��InputCount != 0�������  
**PocMoveDatatoIrpThread**�����ڽ�TempBuffer�е�Scancode����PocDequeueReadThread�����IRP�У�����������IRP��  
#### ���㣺
��Ϊû��hook������ֻ�����߳�����IRP��Scancode������С���ʻ�©��Scancode����Ҫ�����ڼ��̰���̫��ʱ��ͨ��Makecode��BreakCodeֻ��©һ����Ŀǰ����֧���ļ��޳壩�����Զ��⴦��һ�»�ȡ��Scancode��ȷ���õ���ȷ�ļ������ݡ�  
#### δ�����Ľṹ��ͺ�����kbdclass.sys����
```
DeviceExtension->SpinLock��DeviceExtension + SPIN_LOCK_OFFSET_DE��  
DeviceExtension->ReadQueue��DeviceExtension + READ_QUEUE_OFFSET_DE��  
kbdclass!KeyboardClassReadCopyData����kbdclass.sys��ɨ�躯���������룩  
kbdclass!KeyboardClassDequeueRead����������ʵ�֣�  
```
## Build & Installation��
1.������Windows 8.1 x64 6.3��9600�� - Windows 10 x64 21H1��19043.1889����������  
```
�Ѳ���ϵͳ�汾:  
Windows 8.1 x64 6.3(9600)
Windows 10 x64 1511(10586.164)
Windows 10 x64 1709(16299.15)
Windows 10 x64 1809(17763.2928) 
Windows 10 x64 1903(18362.30) 
Windows 10 x64 21H1(19043.1889)  
```
2.ʹ��Visual Studio 2019����Debug x64 Poc����  
3.ʹ��OsrLoader����kdmapper��������  
## License��
**Karlann**, and all its submodules and repos, unless a license is otherwise specified, are licensed under **GPLv3** LICENSE.  
Dependencies are licensed by their own.  
## Warning��
Using this program might render your computer into an unstable state.  
For educational purposes only, use at your own responsibility.  
## References��
https://github.com/Aekras1a/Labs/tree/master/Labs/WinDDK/7600.16385.1/src/input/kbdclass  
https://github.com/ZoloZiak/WinNT4/tree/master/private/ntos/dd/kbdclass  
https://github.com/ZoloZiak/WinNT4/tree/master/private/ntos/dd/i8042prt  
https://github.com/reactos/reactos/tree/master/drivers/hid/kbdhid  
https://github.com/ZoloZiak/WinNT4/tree/master/private/ntos/w32/ntuser/kernel  