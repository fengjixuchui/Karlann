# KARLANN
## It's a kernel-based keylogger for Windows x64.
## Foreword��
**Karlann**��һ��Windows�ں˼��̼�¼����Poc����ͨ����ȡWin32k���͵�Kbdclass��IRP����ȡ���̵�Scancode������Scancodeת���ɶ�Ӧ�Ĵ�Сд�ַ���  
## Description��
#### ԭ��
��Win32k�������ڶ��������ݵ�hKeyboard->FileObject->DeviceObject�滻ΪPoc������DeviceObject��
��Poc�����䵱�м������������Win32k��Kbdclass��IRP��  
�ص����ڻ�ȡ���FileObject�����FileObject��ZwReadFile����Irp->IrpSp->FileObject�У�
����Kbdclass����û�м�������ʱ��IRP����������DeviceExtension->ReadQueue�����У�
��ȻKbdclass��DeviceExtension�ṹ��û�й����������д󲿷����ݵ�ƫ���Դ�Windows 8��ʼ���ǲ���ģ�
���Կ����ҵ�ReadQueue����ʹ��KeyboardClassDequeueRead����ȡ��IRP��Ҳ��ȡ����FileObject��  
#### ȱ�ݣ�
��������������ʱ��ж�ؼ��̡�
#### δ�����Ľṹ��ͺ�����kbdclass.sys����
```
DeviceExtension->RemoveLock��DeviceExtension + REMOVE_LOCK_OFFET_DE��
DeviceExtension->SpinLock��DeviceExtension + SPIN_LOCK_OFFSET_DE��  
DeviceExtension->ReadQueue��DeviceExtension + READ_QUEUE_OFFSET_DE��  
kbdclass!KeyboardClassDequeueRead����������ʵ�֣�  
```
## Build & Installation��
1.������Windows 8.1 x64 6.3��9600�� - Windows 10 x64 21H1��19043.1889����������  
```
�Ѳ���ϵͳ�汾:  
Windows 8.1 x64 6.3(9600)       PASS
Windows 10 x64 1511(10586.164)  PASS
Windows 10 x64 1607(14393.447)  PASS
Windows 10 x64 1703(15063.0)    PASS
Windows 10 x64 1709(16299.15)   PASS
Windows 10 x64 1809(17763.2928) PASS
Windows 10 x64 21H1(19043.1889) PASS
```
2.ʹ��Visual Studio 2019����Release x64 Poc���������ܱ���Debug������IO_REMOVE_LOCK��Debug��Release�µĶ��岻ͬ��  
3.ʹ��OsrLoader��������  
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
https://github.com/HighSchoolSoftwareClub/Windows-Research-Kernel-WRK-
https://download.microsoft.com/download/1/6/1/161ba512-40e2-4cc9-843a-923143f3456c/translate.pdf