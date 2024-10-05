---
Created: 2022-11-16T06:22
---
#### Приложения для проброса USB
|Name|URL|Linux|Windows|Mac|Comment|
|---|---|---|---|---|---|
|[[USB Redirector\|USB Redirector]]|[https://www.incentivespro.com/usb-redirector.html](https://www.incentivespro.com/usb-redirector.html)||Если server (где USB устройство) — на Windows, то клиент бесплатный. У Server-версии триал|||
|[[USB Network Gate\|USB Network Gate]]|[https://www.eltima.com/products/usb-over-ethernet/post-download-win/](https://www.eltima.com/products/usb-over-ethernet/post-download-win/)|yes|Free trial 14 days|yes||
|[[RemoteFX\|RemoteFX]]||||||
|[[USB-IP\|USB-IP]]|[https://usbip.sourceforge.net/](https://usbip.sourceforge.net/)|||||
|[[https---github.com-cezanne-usbip-win\|https---github.com-cezanne-usbip-win]]|[https://github.com/cezanne/usbip-win](https://github.com/cezanne/usbip-win)||||[https://habr.com/ru/company/selectel/blog/668590/](https://habr.com/ru/company/selectel/blog/668590/)|
|[[VirtualHere\|VirtualHere]]|[https://www.virtualhere.com/windows_server_software](https://www.virtualhere.com/windows_server_software)|||||
|[[donglify\|donglify]]|[https://www.donglify.net/en/](https://www.donglify.net/en/)|||||
|[[USB over Network\|USB over Network]]|[https://www.fabulatech.com/usb-over-network-purchase.html#tab_USBNET_subscr](https://www.fabulatech.com/usb-over-network-purchase.html#tab_USBNET_subscr)|да|да|да||
  
  

> [!info]  
>  
> [https://alternativeto.net/software/usb-redirector/](https://alternativeto.net/software/usb-redirector/)  
Как перепрошивать
Windows
Mac
Проблема с японскими камерами
Проблема с регионом CH89101_AP2
Чек-лист при проблемах
6700 Wrong status signature
Подключение через USB over Network
Проблема: нет переключателя PAL/NTSC, у турка
Canon
Развитие
Материалы для пользователей
In-camera apps
# Как перепрошивать
libusbK в Zadig работает стабильнее с девайсами, которые расшарены по сети.
## Windows
1. Скачиваем USB-network gate, устанавливаем, вводим код, активируем триал **F5B84-27E98-7B527-2C390-13CEB**
2. Выбираем камеру в USB Network Gate, шарим
3. Подключаемся к моему VPN, чтобы камера была доступна по сети (из-за NAT может быть недоступна). Коннект разрывается
4. Подключаем камеру к компьютеру клиента, выбираем MSC-mode
5. У себя запускаю USB-network gate. Выбираю в Remote USB-devices Sony A7 IV
6. Устанавливаем драйвер libusb-win32
    1. Запускаем Zadig
    2. Выбираем меню Device → List All Devices
    3. Выбираем драйвер libusb-win32, нажимаем Reinstall Driver
7. Запускаем pmca-gui-v0.18-18-gd634e6c-win.exe от Администратора
8. На вкладке _Tweaks_ выбираем _Start Tweaking (Service Mode)_. Выбираем Unlock all languages или что-то такое. Возможно, не сразу подключится. Тогда надо ещё раз нажать _Start Tweaking (Service Mode)_
9. Перезапустить камеру
## Mac
1. Установка.
    1. Скачать USB over Network. Подходит для версий macOS Monterey, macOS Vеventura.
    2. Когда скачается, кликнуть на установочный пакет. Скажет, что не может установить, из-за настроек безопасности.
    3. Зайти в “Защита и безопасность”. “Разрешить использование приложений, загруженных из…”. Там надо будет нажать куда-то, предложат ввести пароль.
    4. Снова нажать на установочный пакет, установить.
    5. Запустить приложение. Покажет окошко с информацией. Можно закрыть.
2. Запуск
    
    1. Расшарить девайс
        
        ```Java
        valentin@Air-Valentin ~ % cd "/Applications/USB over Network.app/Contents/MacOS/"
        valentin@Air-Valentin MacOS % ./ctl dev list 
        ID  VID: PID: REV  Port  Device name and status
        0  2109:8817:0001  1-5  USB Billboard Device    /available, 0000000000000001/
        1  05e3:0749:1538  2-2  USB3.0 Card Reader /available, 000000001538/
        2  0bda:8153:3100  2-3  USB 10/100/1000 LAN /available, 001000001/
        3  054c:0da5:0200  1-1  ILCE-7M4 /available, D06EC06EF507/
        valentin@Air-Valentin MacOS % ./ctl dev share 3
        ```
        
    2. Добавить сервер
        
        ![[Untitled 28.png|Untitled 28.png]]
        
    3. Запустить pmca, нажать “Start Tweaking (service mode)”. Будет тайм-аут.
        
        ```Java
        Using drivers Windows-MSC, Windows-MTP, Windows-vendor-specific, libusb-MSC, libusb-MTP, libusb-vendor-specific
        Looking for Sony devices
        
        Querying mass storage device
        Sony DSC is a camera in mass storage mode
        
        Switching to service mode
        
        Waiting for camera to switch...
        Operation timed out. Please run this command again when your camera has connected.
        ```
        
    4. На маке расшарить второй девайс.
        
        ```Java
        valentin@Air-Valentin MacOS % ./ctl dev list                                   
        ID  VID: PID: REV  Port  Device name and status
        0  2109:8817:0001  1-5  USB Billboard Device    /available, 0000000000000001/
        1  05e3:0749:1538  2-2  USB3.0 Card Reader /available, 000000001538/
        2  0bda:8153:3100  2-3  USB 10/100/1000 LAN /available, 001000001/
        3  054c:0336:0100  1-1  Sony USB Device /available/
        valentin@Air-Valentin MacOS % ./ctl dev share 3
        ```
        
    5. Подключить в Windows
        
        ![[Untitled 1 16.png|Untitled 1 16.png]]
        
    6. Снова нажать “Start Tweaking (service mode)”. Дальше пойдёт, как по маслу.
    
      
    

> [!info] TCP and UDP ports used by USB Network Gate  
> USB Network Gate Product Page USB Network Gate requires the following ports to be open: TCP 5473 - for getting the list of shared USB devices and detailed information about them; UDP 5474 - for broadcasting, to automatically discover devi.  
> [https://electronicassist.freshdesk.com/support/solutions/articles/44001312428-tcp-and-udp-ports-used-by-usb-network-gate](https://electronicassist.freshdesk.com/support/solutions/articles/44001312428-tcp-and-udp-ports-used-by-usb-network-gate)  
- Инфа по с гитхаба по Задигу
    
    https://github.com/ma1co/Sony-PMCA-RE/issues/308
    
    The correct order of use is.
    
    1. use Zadig first switch the device driver once (libusb-win32)
    2. use pmca-console, enter pmca-console serviceshell
    3. The device will pop up, this is normal, do not shut down or unplug  
        the USB cable, then re-enter Zadig to install the device driver  
        (libusb-win32)  
          
        After the second installation, go to pmca-console, type pmca-console  
        serviceshell again and enter to the service-mode successfully.  
        
    
    ZV-E10
    
    https://github.com/ma1co/Sony-PMCA-RE/issues/290
    
    After I successfully opened service-mode and entered shell  
    mode, I briefly browsed the directory structure, but I didn't have any  
    idea how to modify it. I want to modify the system version number in the  
    system file to trick the official firmware installer to downgrade....  
    
Чужие темы и группы ВК:
- [https://vk.com/topic-21263686_33774377?offset=460](https://vk.com/topic-21263686_33774377?offset=400)
- [https://vk.com/topic-11388096_33781407](https://vk.com/topic-11388096_33781407)
- [https://vk.com/a6300](https://vk.com/a6300)
- Поискать ВК по тексту “Sony A7”
- [https://vk.com/sony_a7s](https://vk.com/sony_a7s)
  
Где ещё поискать:
- Написать тем, кому продал
- Другим продавцам
- Вова Никонов

> [!info] setup-ipsec-vpn/ikev2-howto.md at master · hwdsl2/setup-ipsec-vpn  
> Modern operating systems support the IKEv2 standard.  
> [https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/ikev2-howto.md#os-x-macos](https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/ikev2-howto.md#os-x-macos)  

> [!info] USB Redirector for Linux - USB over IP - USB over Network - Incentives Pro  
> USB Redirector for Linux can be used in USB server or USB client modes.  
> [https://www.incentivespro.com/usb-client-usage.html](https://www.incentivespro.com/usb-client-usage.html)  
Хитрость в том, что при удалённом подключении нужно ещё успеть пробросить устройство Sony USB Device, в которое переключается камера (в сервисном режиме) до того, как сработает таймаут в PMCA. С autoconnect почему-то не получалось, надо разбираться. Может, нужно ставить фильтр, чтобы подключались автоматически только определённые устройства.
- Пример
    
    ```Plain
    valentin@valentin-asus:~$ usbclnt -l
    
    ================== LIST OF REMOTE USB DEVICES ===================
    
       1: USB server at 10.147.17.207:32032
          Mode: manual-connect   Status: disconnected
    
       2: USB server at 192.168.10.2:32032
          Mode: manual-connect   Status: disconnected
    
       3: USB server at 10.147.17.8:32032
          Mode: manual-connect   Status: connected
       |
       `-   6: ILCE-7M4 - USB Mass Storage Device
               Vid: 054c   Pid: 0da5   Serial: D06EC06EDCCF
               Mode: manual-connect   Status: available for connection
    
    ===================== ======================= ===================
    
    valentin@valentin-asus:~$ usbclnt -c 3-6
    
    ====================== OPERATION SUCCESSFUL =====================
    USB device connected
    ===================== ======================= ===================
    
    
    valentin@valentin-asus:~$ usbclnt -l
    
    ================== LIST OF REMOTE USB DEVICES ===================
    
       1: USB server at 10.147.17.207:32032
          Mode: manual-connect   Status: disconnected
    
       2: USB server at 192.168.10.2:32032
          Mode: manual-connect   Status: disconnected
    
       3: USB server at 10.147.17.8:32032
          Mode: manual-connect   Status: connected
       |
       |-   6: ILCE-7M4 - USB Mass Storage Device
       |       Vid: 054c   Pid: 0da5   Serial: D06EC06EDCCF
       |       Mode: manual-connect   Status: not available
       |
       `-   8: Sony USB Device
               Vid: 054c   Pid: 0336   Port: 2-4
               Mode: manual-connect   Status: available for connection
    
    ===================== ======================= ===================
    
    valentin@valentin-asus:~$ usbclnt -c 3-8
    
    ====================== OPERATION SUCCESSFUL =====================
    USB device connected
    ===================== ======================= ===================
    ```
    
## Проблема с японскими камерами
https://github.com/ma1co/Sony-PMCA-RE/pull/356
## Проблема с регионом CH89101_AP2
Китайский, видимо.
Есть метод в [`tweaks.py`](http://tweaks.py)
```Plain
def onValue(self):
  region = self._backup.getRegion()
  if region[region.index('_')+1:] == 'J1':
    return self._getLangs('JP-MOD')
  else:
    return self._getLangs('ALLLANG')
```
Поменял на
```Plain
def onValue(self):
  region = self._backup.getRegion()
  return self._getLangs('RU2')
```
Чтобы всегда только языки с русского региона были и был минимум проблем. Не уверен, что это корректно будет работать с бэкапом. Вроде да, потому что там есть другой метод `offValue` — там, по-видимому, выбираются языки, которые по умолчанию стояли на камере.
## Чек-лист при проблемах
- Проверить, что регион не Китай и не Япония. Вроде можно посмотреть в режиме MTP, если в Mass Storage не получается
- Была проблема, что доходил до окна с твиками, но твик не применялся: GenericUsbException или таймаут. На камере открывалась галерея. Помогло поменять кабель.
- Та же проблема с GenericUSBException. Сначала грешил на сеть. Потом скопировал программу к индусу, установил libusb на основное устройство (Sony A7 III Usb Mass Storage Device). Запустил pmca. Вышла ошибка, не помню, какая. Установил libusb на Sony USB Device. Потом всё получилось.
    
    Примечательно, что до этого удалось прошить ZV-E10 дистанционно.
    
    Человек (индус Махмуд Сайман) сидел с интернета по телефону. Очень медленная связь была через ZeroTier. Очень долго ждал аутентификации и т.д.
    
## 6700 Wrong status signature
- terminal output
    
    ```JavaScript
    valentin@valentin-asus:~$ ./start-service-shell.sh 
    Using drivers libusb-MSC, libusb-MTP, libusb-vendor-specific
    Looking for Sony devices
    
    Querying mass storage device
    Traceback (most recent call last):
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/./pmca-console.py", line 104, in <module>
        main()
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/./pmca-console.py", line 88, in main
        senserShellCommand()
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/pmca/commands/usb.py", line 660, in senserShellCommand
        device = getDevice(driver)
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/pmca/commands/usb.py", line 222, in getDevice
        devices = list(listDevices(driver))
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/pmca/commands/usb.py", line 184, in listDevices
        info = MscDevice(drv).getDeviceInfo()
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/pmca/usb/__init__.py", line 26, in __init__
        self.reset()
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/pmca/usb/__init__.py", line 50, in reset
        self.driver.sendCommand(6 * b'\0')
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/pmca/usb/driver/generic/__init__.py", line 140, in sendCommand
        return self._readResponse(failOnError)
      File "/mnt/Windows/projects/Sony/Sony-PMCA-RE/Sony-PMCA-RE/pmca/usb/driver/generic/__init__.py", line 125, in _readResponse
        raise Exception('Wrong status signature')
    Exception: Wrong status signature
    ```
    
Всё разрешилось хуй пойми как. Видимо, сменой кабеля. Возможно, ещё удалённо получилось сделать, а клиент не проверил (забыл перезагрузить камеру).
## Подключение через USB over Network
Работает шустрее, особенно через ZeroTier. Есть CLI, и через CLI же можно применить license key.

> [!info] USB over Network Client User Manual - Using Command Line Interface  
> - USB over Network Client User Manual - Using Command Line Interface  
> [https://www.usb-over-network.com/usb-over-network-client-help/using-command-line.html](https://www.usb-over-network.com/usb-over-network-client-help/using-command-line.html)  
Конечно, всегда есть вероятность, что заблочат.
Можно установку ZT и USBoN завернуть в скрипт или exe. С автоматическим удалением после. Да и со скачиванием. Хотя, для USBoN нужен (?) полноценный инсталлятор. Завернуть такое сложнее.
# Проблема: нет переключателя PAL/NTSC, у турка
Model: ILME-FX30  
Product code: 32871820  
Serial number: 6503900  
Backup region: CX96701_AF1  
Говорит, Firmware 3.0
# Canon

> [!info] Tornado EOS  
> ▪ Read and Write Calibrations Data ▪ Read and Write Camera Serial Number ▪ Read and Write Sensor Serial Number ▪ Read and Write Camera Wi-Fi MAC ▪ Read and Write Shutter Counter ▪ Read and Write Mirror Counter ▪ Read Detailed Errors Log and Reset it ▪ Read and Set Mode: Norm/Fact/Service ▪ Set DateTime and Regional ▪ Clear Repair Data (Date, Company, etc) ▪ Update and Downgrade Firmware ▪ Switch Model Name (EOS/REBEL/KISS)  
> [https://tornadosw.com/tornado-eos.php](https://tornadosw.com/tornado-eos.php)  

> [!info] Tornado EOS - Trojan or the real thing?  
> Tornado EOS - Trojan or the real thing?  
> [https://www.magiclantern.fm/forum/index.php?topic=23241.0](https://www.magiclantern.fm/forum/index.php?topic=23241.0)  
Говорят про какой-то флаг, и что его можно задать для снятия блокировки языка, но как — не понятно
# Развитие
[[Приложение для русификации Sony. PMCA|Приложение для русификации Sony. PMCA]]
- [ ] Добавить информацию о прошивке Sony и Canon
- [x] Протестировать пробную версию Tornado на своей камере (в т.ч. через USB)
- [x] Как использовать USB Redirector Technician version на Linux - Никак
- [x] Скомпилировать программу для Windows (с увеличенными тайм-аутами)
- [ ] Сделать простой сайт на несколько страниц под популярные запросы. Нужно анализировать именно запросы
    - [ ] Как разблокировать русский
        - [ ] Как поменять язык на камере с японского на русский
        - [ ] Как поменять язык на камере с корейскго на руский
    - [ ] How to unlock languages
    - [ ] Форма обратной связи.
    - [ ] Вишенка — оплата картой через Freedom Pay и кыргызское ИП
    - [ ] Пока оплату можно принимать на карту (ЗК, Visa Direct) или Payoneer
    - [ ] Подогнать под популярные запросы, включающие модели камер
        - [ ] Узнать популярные запросы
- [x] Написать шаблоны фраз для Авито и ВКонтакте
- [x] Сделать страницу в Notion со ссылками на WA, Telegram, фотографиями, описанием процесса
- [ ] Запостить на другие платформы объявлений, в т.ч. в Казахстане и других странах ЕАЭС, Грузии (тем более у меня TBC есть!)
    - [ ] Sahibinden
    - [ ] Добавить другие сайты объявлений в зависимости от языков, которые станут доступны
- [x] Разобраться, как работать с Маком.
    - [x] Попробовать установить USB over Network на Linux
- [ ] Написать другим продавцам на Авито
- [ ] Fiverr. Могут забанить.
    - [x] Открыть счёт в Payoneer на своё настоящее имя
- [ ] Понаписать на DNS Shop в каменты к камерам, что можно русифицировать у меня или с помощью некого приложения для русиикации (описание будет только у меня на странице, а самого приложения не будет, только заглушка и ошибка скачивания, типа “Недоступно в вашем регионе” — но это в идеале и совсем потом…).
- [ ] Написать в объявлении на Авито что-то вроде: “Если не доверяете и не хотите давать доступ, можете воспользоваться программой такой-то, погуглите в интернете”. И название моей программы. Или в переписке давать.
Чья-то страниячка на Таобао

> [!info] taobao | 淘寶  
> 淘寶（Taobao）讓您隨心淘超值商品，爲您提供流行服飾、美妝洗護、3C數碼、大小家電、家俬家居、箱包皮具、運動戶外、五金工具、玩具等千萬件熱銷好貨，淘寶支持文字或圖片搜索商品。天貓淘寶海外作爲Taobao面向華人的跨境電商平台，覆蓋200多個國家和地區的消費者，其中核心站點包括：淘寶香港（taobao hk）、淘寶台灣（taobao tw）、淘寶澳門、淘宝新加坡、淘宝马来西亚、淘宝韩国（타오바오 사이트）、淘宝澳洲、淘宝加拿大、taobao world。  
> [https://www.taobao.com/list/item/677734793174.htm](https://www.taobao.com/list/item/677734793174.htm)  
Можно сделать подобное в разных странах на сайтах объявлений
# Материалы для пользователей
[[Инструкция для клиентов Anydesk|Инструкция для клиентов Anydesk]]
[[Инструкция для клиентов. Flexihub|Инструкция для клиентов. Flexihub]]
[[Сайт|Сайт]]
# In-camera apps

> [!info] Sony PlayMemories Camera Apps : Sony : Free Download, Borrow, and Streaming : Internet Archive  
> An archive of some Sony PlayMemories Camera Apps, as Sony has disabled new purchases of applications and will eventually discontinue access to download past.  
> [https://archive.org/details/sony-playmemories-camera-apps](https://archive.org/details/sony-playmemories-camera-apps)  

> [!info] ptool:ptool-faq [Personal View FAQs Wiki]  
> StreamParser by Chris Brandin as help tool to analyse AVCHD streams -  
> [http://www.personal-view.com/faqs/ptool/ptool-faq](http://www.personal-view.com/faqs/ptool/ptool-faq)  
Тулза для Panasonic
[[Заметки по клиентам|Заметки по клиентам]]