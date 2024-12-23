## Открыть командную строку (консоль, терминал)

1. **Поиск** — в окне «Поиск» напечатайте `cmd` и щелкните на иконку с лупой на панели задач. В новом окне напечатайте `cmd`
   и нажмите <kbd>Enter</kbd>. В списке выберети **запуск от имени администратора**.

2. **Выполнить** — нажмите комбинацию <kbd>Win</kbd> + <kbd>R</kbd>. Напечатайте `cmd` и нажмите <kbd>Enter</kbd>. Затем зажмите
   комбинацию  <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Enter</kbd> — командная строка будет работать **с правами администратора**.

3. **Диспетчер задач** — нажмите <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Esc</kbd>. В левом верхнем углу щелкните
   на «Файл» — «Запустить новую задачу». Напечатайте `cmd` и нажмите <kbd>Enter</kbd>. Отметить чекбокс:
   - [ ] Создать задачу **с правами администратора**

4. **Пуск** — откройте «Пуск» удобным способом. В *Windows 10*: найдите «Служебные — Windows». В *Windows 11*: «Инструменты Windows».
   Затем в списке выберите командную строку.


## Проверка и Восстановление — CHKDSK, SFC и DISM

Чтобы правильно и корректно проверить и восстановить системные файлы в Windows 10, запустите командную строку от
имени администратора и введите ниже команды по очереди:
1. **CHKDSK** — Check Disk
```
chkdsk c: /f /r
```
2. **SFC** — System File Checker
```
sfc /scannow
```
3. **DISM** — Deployment Image and Service Management
```
DISM /Online /Cleanup-Image /RestoreHealth
```
[SFC и DISM](https://mywebpc.ru/windows/recovery-of-system-files-in-windows/)


## Скачать Windows 10 (ISO-файл)

[Скачать образ диска Windows 10 (ISO-файл) — сайт Microsoft](https://www.microsoft.com/ru-ru/software-download/windows10ISO)

[Cкачать Windows 10 ISO — 5 способов](https://remontka.pro/download-windows-10-iso-microsoft/#microsoft)


## Производительность компьютера soft

**CPU-Z** - утилита, которая предоставит вам самую подробную информацию об установленном в системе процессоре, памяти, 
кэше и материнской плате. Разработчик: CPUID. [CPU-Z](https://www.cpuid.com/softwares/cpu-z.html)

**GPU-Z** — утилита предоставляет все данные по видеокарте [GPU-Z](https://www.techpowerup.com/gpuz/)

**HWinfo** — программа рассказывает о компьютере всё, что только возможно. Информация разделена по трём пунктам: системная, 
полный отчёт и мониторинг датчиков. [HWinfo](https://www.hwinfo.com/)

**HWMonitor** — позволит узнать температуру, скорость вентиляторов, напряжение. 


CrystalDiskMark – Crystal Dew World


## CHKDSK.exe

```
chkdsk C: /f /r
```
- проверка диска, в этой команде будет проверен на ошибки диск `C`
- при этом ошибки будут исправляться автоматически — параметр/флаг `/f`
- будет проведена проверка поврежденных секторов и попытка восстановления информации — параметр `/r` (должен быть
обязательно установлен флаг `/f`)

По итогам вы получите статистику проверенных данных, найденных ошибок и поврежденных секторов.

>  Внимание!
>
> Check Disk работает только с дисками, отформатированными в NTFS или FAT32.

Чтобы выполнить **оффлайн проверку диска** и исправление ошибок на нем, в командной строке от имени администратора выполните команду:

```
chkdsk C: /f /offlinescanandfix
```
- где `C:`  — буква проверяемого диска


### Запуск chkdsk при перезагрузки

Если будет продемонстрировано сообщение, что `выполнить команду chkdsk нельзя из-за использования тома иным процессором`: 
нажимаем <kbd>Y</kbd>, потом <kbd>Inter</kbd>, закрываем командную строку и перезагружаем компьютер. Проверка диска автоматически начнется в начале загрузки Windows 10.

### Предварительное отклюяение тома

Предварительное отключение тома (при необходимости). Все **открытые дескрипторы**\* для этого тома будут недействительны:
```
chkdsk C: /f /x
```
- должен быть обязательно установлен флаг `/f`

\* **дескриптор тома** — это уникальный идентификатор, который используется операционной системой для доступа к файлам 
на диске. Когда программа открывает файл, ей присваивается дескриптор тома, который используется для последующего доступа к файлу.


## DISM.exe

Восстановление хранилища компонентов Windows 10 с помощью DISM.exe

Утилита для развертывания и обслуживания образов Windows DISM.exe позволяет выявить и исправить те проблемы с хранилищем 
системных компонентов Windows 10, откуда при проверке и исправлении целостности системных файлов копируются оригинальные их версии.

Для использования DISM.exe, запустите командную строку от имени администратора. После чего можно использовать следующие команды:

```
dism /Online /Cleanup-Image /CheckHealth
```
— для получения информации о состоянии и наличии повреждений компонентов Windows. При этом **сама проверка не производится**, 
а лишь проверяются ранее записанные значения.

```
dism /Online /Cleanup-Image /ScanHealth
```
— **проверка целостности и наличия повреждений компонентов хранилища. Может занять продолжительное время и «зависать» 
в процессе на 20 процентах.

```
dism /Online /Cleanup-Image /RestoreHealth
```
— производит и **проверку и автоматическое восстановление системных файлов Windows**, также как и в предыдущем случае, 
занимает время и останавливается в процессе.

> Примечание:
> 
> в случае, если команда восстановления хранилища компонентов не работает по той или иной причине, вы можете использовать
> файл install.wim (или esd) со смонтированного ISO образа Windows 10 [Cкачать Windows 10 ISO](https://remontka.pro/download-windows-10-iso-microsoft/) в качестве источника файлов, требующих восстановления (содержимое образа должно соответствовать установленной системе). Сделать это можно с помощью команды:
```
dism /Online /Cleanup-Image /RestoreHealth /Source:wim:путь_к_файлу_wim:1 /limitaccess
```

Вместо `.wim` можно использовать файл `.esd` тем же образом, заменив в команде все `wim` на `esd`.

Для этого введите в командной строке такую команду:
```
DISM.exe /Online /Cleanup-Image /RestoreHealth /Source:C:\RepairSource\Windows /LimitAccess
```

> Примечание:
> 
> вместо заполнителя `C:\RepairSource\Windows` укажите расположение вашего источника восстановления. 



