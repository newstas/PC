## Командная строка (консоль, терминал, cmd, command prompt)

1. **Поиск** — в окне «Поиск» напечатайте `cmd` и щелкните на иконку с лупой на панели задач. В новом окне напечатайте `cmd`
   и нажмите <kbd>Enter</kbd>. В списке выберети **запуск от имени администратора**.

2. **Выполнить** — нажмите комбинацию <kbd>Win</kbd> + <kbd>R</kbd>. Напечатайте `cmd` и нажмите <kbd>Enter</kbd>. Затем зажмите
   комбинацию  <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Enter</kbd> — командная строка будет работать **с правами администратора**.

3. **Диспетчер задач** (task manager) — нажмите <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Esc</kbd>. В левом верхнем углу щелкните
   на «Файл» — «Запустить новую задачу». Напечатайте `cmd` и нажмите <kbd>Enter</kbd>. Отметить чекбокс:
   - [ ] Создать задачу **с правами администратора**

4. **Пуск** — откройте **Пуск** удобным способом. В *Windows 10*: найдите **Служебные — Windows**. В *Windows 11*: **Инструменты Windows**,
   затем в списке выберите **Командную строку**.


## Панель управления (control panel)

1, 2, 3 — методы как (в предыдущем параграфе) с Командной строкой, но вместо `cmd` набираем `control panel`. В 4 — выбираем **Панель управления**


## Безопасный режим (safe mode)

1. При запуске системы необходимо зажать клавиши <kbd>Ctrl</kbd> + <kbd>F8</kbd>

2. Через **Msconfig (конфигурация системы)** — комбинацию <kbd>Win</kbd> + <kbd>R</kbd>. Напечатайте `msconfig` и выбираем вкладку
   **Загрузка**, затем выбераем опцию **Безопасная загрузка** и нажимаем **Применить**

3. Через **средаства восстановления Windows (Windows RE)** [WinRE](https://support.microsoft.com/ru-ru/windows/%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0-windows-1af6ec8c-4d4a-4b23-adb7-e76eef0b847f#WindowsVersion=Windows_10):
   - нажимаем на **Пуск** и выбираем пункт **Выключение**, после этого, зажав клавишу <kbd>Shift</kbd>, щелкаем по пункту **Перезагрузка**
   - по завершении данных действий Windows перейдет в спецрежим и на голубом экране **высветится меню UEFI** (подобие BIOS)
   - Следующим шагом является вход в пункт **Диагностика** - **Дополнительные параметры** и пункт **Параметры загрузки**
   - После захода в пункт **Перезагрузка** нажимаем на клавишу <kbd>4</kbd> и Windows **совершит запуск в безопасном режиме**

**! Если при загрузке безопасного режима произошла ошибка**, возможно, повреждена ветка реестра Safeboot, которая отвечает за загрузку 
безопасного режима. Восстановить ветку реестра можно с помощью заранее экспортированного REG-файла. Для этого:
- Скачайте архив [SafeBoot.zip](https://media.kaspersky.com/utilities/ConsumerUtilities/safeboot.zip) и запустить файл SafeBootWin8.reg
  для Windows 8, 8.1, 10, 11, затем запустить безопасный режим


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


## Восстановление целостности реестра — scanreg /fix 

- нажмите комбинацию клавиш <kbd>Windows</kbd> + <kbd>R</kbd>
- в появившемся окне введите команду `scanreg /fix`


## Сведения о системе — msinfo32

- нажмите комбинацию клавиш <kbd>Windows</kbd> + <kbd>R</kbd>
- в появившемся окне введите команду `msinfo32`


## Информация о лицензии Windows

**SLMGR** - средство управления лицензированием программного обеспечения Windows:
- **Выполнить:** <kbd>Windows</kbd> + <kbd>R</kbd> далее `slmgr.vbs /dli` - сведений о лицензии (кратко)
- **Выполнить:** <kbd>Windows</kbd> + <kbd>R</kbd> далее `slmgr.vbs /dlv` - подробных сведений о лицензии
   - VK7JG-NPHTM-C97JM-9MPGT-3V66T для редакции Pro,
   - YTMG3-N6DKC-DKB77-7M9GH-8HVX7 для редакции Home,
   - BT79Q-G7N6G-PGBYW-4YWX6-6F4BT для Home SL.

*Например: покажет `Частичный ключ продукта: 3V66T`, как видим, в системе уже есть ключ (3V66T). 
Эти ключи значит, что что компьютер получил персональную цифроваю лицензию с сервера активации компании Microsoft. 
При это, ключ продукта был заменен сервером.*

- **Выполнить:** <kbd>Windows</kbd> + <kbd>R</kbd> далее `slmgr.vbs /ato` - активация Windows (иногда помогает)

Состояние лицензии лицензии **Licetse Status**:
- Unlicensed — нет лицензии
- Licensed — имеет лицензию
- Notification — срок ознакомительного использования окончен

Лицезнии Retail и OEM
- Retail — коробочная верся, можно установить на новый компьютер при условии удаления со старого.
- OEM (производитель оригинального оборудования) — привязана к оборудованию того компьютера, на котором она установлена, нельзя переустановить на другой компьютер. Лицензионный ключ OEM может быть прошит в BIOS/UEFI. Смотреть с помощью программы ShowKeyPlus.

**Программа ShowKeyPlus**

[Скачать ShowKeyPlus](https://github.com/superfly-inc/showkeyplus/releases) — программа определяет ключ продукта Windows
- **Посмотреть ключ в BIOS/UEF материской платы** - вы увидите в строке **OEM Key** вшитый ключ, а в строке **OEM Edition** вы увидите
название той версии Windows, которой соответствует **ОЕМ ключ**. Для успешной активации установленной Windows этим ключем,
**OEM Edition** должна совпадать со строкой **Product Name**. Если **OEM Edition** не совпадает со строкой **Product Name** - ваша система
не активируется. Придется устанавливать именно ту версию, что указаноа в **OEM Edition**. 
*Например: OEM Key: OEM key not present in firmware — ключ OEM не присутствует в прошивке BIOS/UEFI (Windows 7,8,10)*
- **Посомтреть ключ в папаке Windows или Windows.old** Посмотреть с помощью ShowKeyPlus ключ в старой версии Windows — можно
в папке `Windows.old`: выберите **Retrieve key from backup** и в открывшемся окне перейдите `диск С - Windows - System32 - config`
и нажмите 2 раза открыт.  Программа просканирует файл и покажет ключ в строке Installed Key.
- **Проверить соостветствии ключа установленной Windows** - нажмите **Check Product Key** - в поле **Product Key** введите лицензионный ключ
и чуть нижепрограмма покажет версию операцтонной системы соответсвующую ключу. Если установленная версия Windows на вашем компьютере или ноутбуке
 соответствует версии которую показывает ShowKeyPlus, значит у вас получится активировать свою систему.
 

## Скачать Windows 10 (ISO-файл)

[Скачать образ диска Windows 10 (ISO-файл) — сайт Microsoft](https://www.microsoft.com/ru-ru/software-download/windows10ISO)

[Cкачать Windows 10 ISO — 5 способов](https://remontka.pro/download-windows-10-iso-microsoft/#microsoft)


## Ninite

**Ninite** — Установите и обновите все ваши программы одновременно [Ninite](https://ninite.com/)


## Производительность компьютера Analyse-Tool Soft

Программы для полной инвентаризации и мониторинга оборудования (Complete Hardware Inventory and Monitoring)

**CPU-Z** - утилита, которая предоставит вам самую подробную информацию об установленном в системе процессоре, памяти, 
кэше и материнской плате. От Франк Делаттре из Франции. Разработчик: CPUID. [CPU-Z](https://www.cpuid.com/softwares/cpu-z.html)

**GPU-Z** — утилита предоставляет все данные по видеокарте. Разработчик: TechPowerUp [GPU-Z](https://www.techpowerup.com/gpuz/)

**GPU Caps Viewer** - утилита от Geeks3D для графической карты, которая тестирует ее на производительность, показывает текущую температуру 
графического процессора, расширения **OpenGL**, информацию о поддержке OpenGL API и прочие храктеристики графической карты. 
[GPU Caps Viewer](https://www.geeks3d.com/20240212/gpu-caps-viewer-1-63-released/)

**Онлайн проверка OpenGL и WebGL** - [WebGL Caps Viewer](https://www.geeks3d.com/webgl/)) от Geeks3D и [threejs.org](https://threejs.org/examples/) 
WebGL основан на тетехнологии OpenGL ES 2.0

**HWinfo** (HardWareInfo) — программа для получения подробной информации о комплектующих ПК, рассказывает о компьютере всё, 
что только возможно. Информация разделена по трём пунктам: системная, полный отчёт и мониторинг датчиков. частота кадров (FPS), 
время отображения кадра (Frametimes) и уровень занятости графического процессора (GPU Busy) Использует NASA [HWinfo](https://www.hwinfo.com/)

**HWMonitor** — мониторинг напряжения, температуры и скорости вентиляторов. На ноутбуках MacBook, имеется приложение **smcFanControl**.
Разработчик: CPUID [HWMonitor](https://www.cpuid.com/softwares/hwmonitor.html)

**CrystalDiskMark** – бенчмарк для устройств хранения данных. В первую очередь чтобы узнать, как быстро происходит чтение и запись данных. От японца Noriyuki Miyazaki. [CrystalDiskMark](https://crystalmark.info/en/software/crystaldiskmark/)

**CrystalDiskInfo** — утилита для диагностики работы жёстких дисков и твердотельных накопителей ПК. От японца Noriyuki Miyazaki. [CrystalDiskInfo](https://crystalmark.info/en/software/crystaldiskinfo/)

**OCCT** (OverClock Checking Tool) — OCCT – это основной конкурент AIDA64, который также предоставляет очень подробную информацию о комплектующих и позволяет проверить их работу в стресс-тесте, дают интенсивную нагрузку на CPU, GPU или RAM. [OCCT](https://www.ocbase.com/)

**MemTest64** — утилита, которая позволяет проверять системную память на наличие проблем на аппаратном уровне.очень простая в обращении, 
достаточно нажать на кнопку «Начать тест». Разработчик: TechPowerUp [MemTest6](https://www.techpowerup.com/download/techpowerup-memtest64/)

**TreeSize Free** — выводит список всех папок и документов, сортируя их по размеру. [TreeSize Free](https://www.jam-software.com/treesize_free)

**WizTree** — анализатор дискового пространства. [WizTree](https://www.diskanalyzer.com/)

**UserBenchmark** (хороший поиск лучших комплектуютих онлайн) — это простая программа для тестирования компьютера и сравнения результатов с другими пользователями (не всегда работает).  [UserBenchmark](https://www.userbenchmark.com/)

**FurMark** (волосатый бублик) это лучшее приложение для проверки видеокарты компьютера. Ни одна друга утилита не нагружает ГПУ так, как это делает Furmark. Быстрый графический тестOpenGL и Vulkan с онлайн-оценками от Geeks3D. [FurMark](https://geeks3d.com/furmark/)

### Дисплей

[Monitest.ru — онлайн](https://monitest.ru/) / [EIZO Monotor Test — онлайн](https://www.eizo.be/monitor-test/) / [tft.vanity.dk/](http://tft.vanity.dk/) / 
[TFT Monitor Test - скачать](https://tireal.com/tfttest.php) / [Другие Monitor Test](http://www.benchmarkhq.ru/russian.html?/b_monitor.html)


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


##Ключи активации Windows 10 с сервера Microsoft

Персональную цифроваю лицензию с сервера активации компании Microsoft:

Версия | Ключ
---    | ---
Home/Core                           | TX9XD-98N7V-6WMQ6-BX7FG-H8Q99         
Home/Core (Country Specific)        | PVMJN-6DFY6-9CCP6-7BKTT-D3WVR   
Home/Core (Single Language)         |  7HNRX-D7KGG-3K4RQ-4WPJ4-YTDFH   
Home/Core N                         | 3KHY7-WNT83-DGQKR-F7HPR-844BM  
Professional                        | W269N-WFGWX-YVC9B-4J6C9-T83GX  
Professional N                      | MH37W-N47XK-V7XM9-C7227-GCQG9 
Professional Enterprise		   	   |
Professional Workstation			   |
Enterprise                          | NPPR9-FWDCX-D2C8J-H872K-2YT43  
Enterprise N                        | DPH2V-TTNVB-4X9Q3-TJR4H-KHJW4  
Education                           | NW6C2-QMPVW-D7KKK-3GKT6-VCFB2  
Education N                         | 2WH4N-8QGBV-H22JP-CT43Q-MDWWJ  
Enterprise 2015 LTSB                | WNMTR-4C88C-JK8YV-HQ7T2-76DF9 
Enterprise 2015 LTSB N              | 2F77B-TNFGY-69QQF-B8YKP-D69TJ  
Enterprise 2016 LTSB                | DCPHK-NFMTC-H88MJ-PFHPY-QJ4BJ   
Enterprise 2016 LTSB N              | QFFDN-GRT3P-VKWWX-X7T3R-8B639 

Версия | Ключ
---    | ---
Windows 10 Enterprise N Eval | MNXKQ-WY2CT-JWBJ2-T68TQ-YBH2V 
Windows 10 Enterprise S Eval | 7TNX7-H36JG-QFF42-K4JYV-YY482 
Windows 10 Enterprise S N Eval |	D3M8K-4YN49-89KYG-4F3DR-TVJW3 
Windows 10 Enterprise Eval |	VPMWD-PVNRR-79WJ9-VVJQC-3YH2G 
Windows 10 Starter |	D6RD9-D4N8T-RT9QX-YW6YT-FCWWJ 
Windows 10 Education N |	84NGF-MHBT6-FXBX8-QWJK7-DRR8H 
Windows 10 Education |	YNMGQ-8RYV3-4PGQ3-C8XTP-7CFBY 
Windows 10 Professional |	VK7JG-NPHTM-C97JM-9MPGT-3V66T 
Windows 10 Professional N |	2B87N-8KFHP-DKV6R-Y2C8J-PKCKT 
Windows 10 Core |	YTMG3-N6DKC-DKB77-7M9GH-8HVX7 
Windows 10 Core N |	4CPRK-NM3K3-X6XXQ-RXX86-WXCHW 
Core Single Language |	BT79Q-G7N6G-PGBYW-4YWX6-6F4BT 
Core Country Specific |	N2434-X9D7W-8PF6X-8DV9T-8TYMD 

Версия | Ключ
---    | ---
Windows 10 Home | YTMG3-N6DKC-DKB77-7M9GH-8HVX7 
Windows 10 Home N | 4CPRK-NM3K3-X6XXQ-RXX86-WXCHW 
Windows 10 Pro | VK7JG-NPHTM-C97JM-9MPGT-3V66T 
Windows 10 Pro N | 2B87N-8KFHP-DKV6R-Y2C8J-PKCKT 
Windows 10 Pro for Workstations | DXG7C-N36C4-C4HTG-X4T3X-2YV77 
Windows 10 Pro N for Workstations | WYPNQ-8C467-V2W6J-TX4WX-WT2RQ 
Windows 10 S | 3NF4D-GF9GY-63VKH-QRC3V-7QW8P 
Windows 10 Education | YNMGQ-8RYV3-4PGQ3-C8XTP-7CFBY 
Windows 10 Education N | 84NGF-MHBT6-FXBX8-QWJK7-DRR8H 
Windows 10 Pro Education | 8PTT6-RNW4C-6V7J2-C2D3X-MHBPB 
Windows 10 Pro Education N | GJTYN-HDMQY-FRR76-HVGC7-QPF8P 
Windows 10 Enterprise | XGVPP-NMH47-7TTHJ-W3FW7-8HV2C 
Windows 10 Enterprise S | NK96Y-D9CD8-W44CQ-R8YTK-DYJWX 
Windows 10 Enterprise N | WGGHN-J84D6-QYCPR-T7PJ7-X766F 
Windows 10 Enterprise G N | FW7NV-4T673-HF4VX-9X4MM-B4H4T 
Windows 10 Enterprise N LTSB 2016 | RW7WN-FMT44-KRGBK-G44WK-QV7YK


