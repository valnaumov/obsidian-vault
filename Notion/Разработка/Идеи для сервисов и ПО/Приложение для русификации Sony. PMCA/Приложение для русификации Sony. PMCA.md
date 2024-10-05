---
Платформа:
  - Desktop
Статус: В процессе
💲: true
---
# Текущие задачи
[[Текущие задачи|Текущие задачи]]
[[Реверс-инжениринг (то, что не касается непосредственно разработки)|Реверс-инжениринг (то, что не касается непосредственно разработки)]]
# Эмуляция
https://github.com/ma1co/OpenMemories-CI
Надо использовать `nflasha` and `boot`, `[**bootrom.enc**](https://github.com/ma1co/OpenMemories-CI/blob/master/firmware/NEX-3/bootrom.enc)` , как говорит ma1co здесь [https://github.com/ma1co/Sony-PMCA-RE/pull/116](https://github.com/ma1co/Sony-PMCA-RE/pull/116).
Ещё немного про QEMU
https://github.com/ma1co/qemu
  
# MSC-драйвер
Либа под андроид. Можно ли адаптировать?
https://github.com/magnusja/libaums/
Нужно ли писать драйвер, чтобы менять язык. Там что-то упоминалось про Backup file, в котором якобы все эти настройки прописываются. А где он хранится? Или не файл, а просто комманды посылаются?
Возможно, даже не нужно ничего переписывать

> [!info]  
>  
> [https://github.com/magnusja/libaums/tree/develop/libusbcommunication](https://github.com/magnusja/libaums/tree/develop/libusbcommunication)  
Нужно override UsbCommunication и всё?
# Дополнительные материалы

> [!info] Command list - Pastebin.com  
> Pastebin.  
> [https://pastebin.com/cQH9x4z9](https://pastebin.com/cQH9x4z9)  
Какие-то коды операций

> [!info] Sony Alpha hacks talk - Personal View Talks  
> is possible to put software into camera one more time even if is already newest update, but if installed soft is hacked, probably "hard update" will help, problem is that updater will not re-update it because by this soft camera is obviously updated.  
> [https://www.personal-view.com/talks/discussion/12756/sony-alpha-hacks-talk/p11](https://www.personal-view.com/talks/discussion/12756/sony-alpha-hacks-talk/p11)  
Форум, где с [malco](https://www.personal-view.com/talks/profile/malco) общаются
Полезная инфа: про некий backup.bin
https://github.com/ma1co/Sony-PMCA-RE/issues/428

> [!info] sony-hack:languages [Personal View FAQs Wiki]  
> As you may (not) know, many cameras from Sony sold in Japan have this strange feature of allowing only menus in Japanese language.  
> [https://www.personal-view.com/faqs/sony-hack/languages](https://www.personal-view.com/faqs/sony-hack/languages)  

> [!info] Guide: Sony A7III/A7RIII/A9 Firmware Language mod - Personal View Talks  
> NOTE: this method is still pending an encryption method, but until then I thought it would be nice to prepare your firmware folders for when the update hits!  
> [https://www.personal-view.com/talks/discussion/21766/guide-sony-a7iiia7riiia9-firmware-language-mod/p1](https://www.personal-view.com/talks/discussion/21766/guide-sony-a7iiia7riiia9-firmware-language-mod/p1)  
Как использовать [fwtool.py](http://fwtool.py) от ma1co

> [!info] Sony Global - Source Code Distribution Service  
> Source code download  
> [https://oss.sony.net/Products/Linux/DI/category01.html#ca3](https://oss.sony.net/Products/Linux/DI/category01.html#ca3)  
## USB

> [!info] USB in a NutShell - Chapter 1 - Introduction  
> Introduces the Universal Serial Bus covering the various chapters of the spec and what is required to be read.  
> [https://www.beyondlogic.org/usbnutshell/usb1.shtml](https://www.beyondlogic.org/usbnutshell/usb1.shtml)  
[[i]]

> [!info] SCSI command  
> In SCSI computer storage, computers and storage devices use a client-server model of communication.  
> [https://en.wikipedia.org/wiki/SCSI_command](https://en.wikipedia.org/wiki/SCSI_command)  
[https://www.seagate.com/files/staticfiles/support/docs/manual/Interface manuals/100293068j.pdf](https://www.seagate.com/files/staticfiles/support/docs/manual/Interface%20manuals/100293068j.pdf)
## Использование libusb
Возможно, есть смысл попробовать писать программу под использование драйвера libusb. Надо его как-то устанавливать/заменять.
Эта дискуссия на Гитхабе может быть полезна: [https://github.com/raspberrypi/picoprobe/issues/15](https://github.com/raspberrypi/picoprobe/issues/15).
Установщик для libusbK. Возможно, устанавливать сразу с нашей программой для определённого vendorId. И если есть возможность, сносить при деинсталляции.

> [!info] Creating Client Installers With InfWizard  
> Self-contained end-user installer applications created by InfWizard.  
> [https://libusbk.sourceforge.net/UsbK3/usbk_installers.html](https://libusbk.sourceforge.net/UsbK3/usbk_installers.html)  
# Стек

> [!info] Создаем нативное Kotlin приложение на Spring Boot Native, Gradle и GraalVM без докера под MacOS и Windows  
> English version В этой статье я хочу рассказать о практическом опыте нативной компиляции production приложения, написанного на Kotlin со Spring Boot, Gradle с использованием GraalVM .  
> [https://habr.com/ru/articles/760074/](https://habr.com/ru/articles/760074/)  
# Nikon

> [!info] Nikon Hacker • View topic - MOVED: Add another language to my D5200 camera  
> Dedicated to the improvement of DSLRs  
> [https://nikonhacker.com/viewtopic.php?f=4&t=1760&sid=307675d3e41708c0d3498d86c39a425a&start=10](https://nikonhacker.com/viewtopic.php?f=4&t=1760&sid=307675d3e41708c0d3498d86c39a425a&start=10)  

> [!info] NikonEmulator - Nikon Hacker  
> (formerly FrEmulator)  
> [https://nikonhacker.com/wiki/NikonEmulator](https://nikonhacker.com/wiki/NikonEmulator)