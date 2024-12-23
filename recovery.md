## Открыть командную строку от имени админстрации


Чтобы открыть окошко с командой одновременно нажмите клавишу Windows и кнопку R. Наберите в строке cmd, а затем зажмите комбинацию Ctrl+Shift+Enter. Командная строка будет работать с админскими правами


## Производительность компьютера soft

CPU-Z - https://www.cpuid.com/softwares/cpu-z.html#version-history

CPU-Z - утилита, которая предоставит вам самую подробную информацию об установленном в системе процессоре, памяти, кэше и материнской плате. Разработчик: CPUID.

Speccy - https://www.ccleaner.com/speccy

CCleaner - https://www.ccleaner.com/ru-ru/ccleaner/download


## Проверка и Восстановление системных файлов

Чтобы правильно и корректно проверить и восстановить системные файлы в Windows 10, запустите командную строку от имени администратора и введите ниже команды по очереди:

1 
```
chkdsk c: /f /r
```
2 
```
sfc /scannow
```
3 
```
DISM /Online /Cleanup-Image /RestoreHealth
```

https://mywebpc.ru/windows/recovery-of-system-files-in-windows/


## chkdsk C: /F /R — проверка диска

```
chkdsk C: /f /r — проверка диска, в этой команде будет проверен на ошибки диск C:
```

при этом ошибки будут исправляться автоматически (параметр/флаг /f);

будет проведена проверка поврежденных секторов и попытка восстановления информации (параметр /r), должен быть обязательно установлен флаг /f.

По итогам которой вы получите статистику проверенных данных, найденных ошибок и поврежденных секторов

Check Disk работает только с дисками, отформатированными в NTFS или FAT32.

Чтобы выполнить оффлайн проверку диска и исправление ошибок на нем, в командной строке от имени администратора выполните команду:

```
chkdsk C: /f /offlinescanandfix
```

где C:  — буква проверяемого диска

Если будет продемонстрировано сообщение, что выполнить команду chkdsk нельзя из-за использования тома иным процессором, нажимаем Y, потом Inter, закрываем командную строку и перезагружаем компьютер. Проверка диска автоматически начнется в начале загрузки Windows 10.



Предварительное отключение тома (при необходимости). Все открытые дескрипторы для этого тома будут недействительны:
```
chkdsk C: /f /x
```
Должен быть обязательно установлен флаг /f.



Дескриптор тома — это уникальный идентификатор, который используется операционной системой для доступа к файлам на диске. Когда программа открывает файл, ей присваивается дескриптор тома, который используется для последующего доступа к файлу.




## DISM.exe

Восстановление хранилища компонентов Windows 10 с помощью 

Утилита для развертывания и обслуживания образов Windows DISM.exe позволяет выявить и исправить те проблемы с хранилищем системных компонентов Windows 10, откуда при проверке и исправлении целостности системных файлов копируются оригинальные их версии.

Для использования DISM.exe, запустите командную строку от имени администратора. После чего можно использовать следующие команды:

```
dism /Online /Cleanup-Image /CheckHealth
```

— для получения информации о состоянии и наличии повреждений компонентов Windows. При этом сама проверка не производится, а лишь проверяются ранее записанные значения.

```
dism /Online /Cleanup-Image /ScanHealth
```

— проверка целостности и наличия повреждений хранилища компонентов. Может занять продолжительное время и «зависать» в процессе на 20 процентах.

```
dism /Online /Cleanup-Image /RestoreHealth
```

— производит и проверку и автоматическое восстановление системных файлов Windows, также как и в предыдущем случае, занимает время и останавливается в процессе.

Примечание: в случае, если команда восстановления хранилища компонентов не работает по той или иной причине, вы можете использовать файл install.wim (или esd) со смонтированного ISO образа Windows 10 (Как скачать Windows 10 ISO с сайта Microsoft)
https://remontka.pro/download-windows-10-iso-microsoft/
в качестве источника файлов, требующих восстановления (содержимое образа должно соответствовать установленной системе). Сделать это можно с помощью команды:

```
dism /Online /Cleanup-Image /RestoreHealth /Source:wim:путь_к_файлу_wim:1 /limitaccess
```
Вместо .wim можно использовать файл .esd тем же образом, заменив в команде все wim на esd.

Для этого введите в командной строке такую команду:

DISM.exe /Online /Cleanup-Image /RestoreHealth /Source:C:\RepairSource\Windows /LimitAccess

Примечание. Вместо заполнителя C:\RepairSource\Windows укажите расположение вашего источника восстановления. Дополнительные сведения об использовании средства DISM для восстановления Windows см. в статье