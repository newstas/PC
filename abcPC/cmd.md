# Командная строка (cmd.exe) Windows 10 

- **Быстрый запуск:** нажмите **Win+R**, введите `cmd` и нажмите **Enter**. 
- **С правами администратора**: нажмите правой кнопкой на **«Пуск» -> Командная строка (администратор)**.

Устройства, пробуждающие ПК: 
- Откройте командную строку от имени администратора и введите `powercfg -devicequery wake_armed`, чтобы узнать, какое устройство мешает сну.
Мышь или сетевая карта часто вызывают это, но бывают и другие устройства, например:
```
C:\WINDOWS\system32>powercfg -devicequery wake_armed
NVIDIA USB Type-C Port Policy Controller
HID-compliant Optical Wheel Mouse (001)
Logicool HID-Compliant Keyboard (106 keys)
Qualcomm Atheros AR8151 PCI-E Gigabit Ethernet Controller (NDIS 6.30)
```
