Все нужные команды прописаны в файле для СI: `appveyor.yml` и `.travis.yml`
1. Создаём [[venv]]
2. Не забываем переключиться на ветку `production`
3. `pip install -r requirements.txt`
4. `python -OO -m PyInstaller pmca-console.spec` Может потребовать установить binutils: `sudo apt install binutils`
5. Скомпилированный файл будет лежать в `./dist`
Запустив `./dist/pmca-console`, можно получить такую ошибку:
```
Traceback (most recent call last):
  File "pmca-console.py", line 7, in <module>
    from pmca.commands.usb import *
  File "PyInstaller/loader/pyimod02_importers.py", line 384, in exec_module
  File "pmca/commands/usb.py", line 16, in <module>
    from ..marketserver.server import *
  File "PyInstaller/loader/pyimod02_importers.py", line 384, in exec_module
  File "pmca/marketserver/server.py", line 5, in <module>
    import tlslite
  File "PyInstaller/loader/pyimod02_importers.py", line 384, in exec_module
  File "tlslite/__init__.py", line 27, in <module>
  File "PyInstaller/loader/pyimod02_importers.py", line 384, in exec_module
  File "tlslite/api.py", line 18, in <module>
  File "PyInstaller/loader/pyimod02_importers.py", line 384, in exec_module
  File "tlslite/integration/tlsasyncdispatchermixin.py", line 10, in <module>
ModuleNotFoundError: No module named 'asyncore'
[PYI-3671:ERROR] Failed to execute script 'pmca-console' due to unhandled exception!
```
Это связано с тем, что asyncore был [удалён](https://bugs.python.org/issue45785) в версии Питона 3.11. Если ничего не переписывать, надо даунгрейднуть до версии 3.10. Например, с помощью утилиты  [[conda или miniconda|conda]].
В [репозитории](https://github.com/fail2ban/fail2ban/issues/3487) fail2ban обсуждаются другие пути решения.
Для miniconda это будет так. Создать окружение с версией python: 
`conda create -n myenv python=3.10`
Активировать окружение:
`conda activate myenv`
И теперь можем собирать проект с версией Питона 3.10, где ещё есть asyncore.
