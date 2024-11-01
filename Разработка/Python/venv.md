[Доки](https://docs.python.org/3/library/venv.html)
# Для чего нужен
# Как создать
`python -m venv ./venv`
Если получаем такую ошибку:
```
The virtual environment was not created successfully because ensurepip is not
available.  On Debian/Ubuntu systems, you need to install the python3-venv
package using the following command.

    apt install python3.12-venv

You may need to use sudo with that command.  After installing the python3-venv
package, recreate your virtual environment.
```
Надо установить соответствующую версию venv. Обычно, как я понял, и предлагается та версия пакета, которую нужно установить.
Узнать версию питона: `python -V`
# Как активировать
| Platform   | Shell                                   | Command to activate virtual environment |
| ---------- | --------------------------------------- | --------------------------------------- |
| POSIX      | bash/zsh                                | `$ source _<venv>_/bin/activate`        |
|            | fish                                    | `$ source _<venv>_/bin/activate.fish`   |
|            | csh/tcsh                                | `$ source _<venv>_/bin/activate.csh`    |
|            | pwsh                                    | `$ _<venv>_/bin/Activate.ps1`           |
| Windows    | cmd.exe                                 | `C:\> _<venv>_\Scripts\activate.bat`    |
| PowerShell | `PS C:\> _<venv>_\Scripts\Activate.ps1` |                                         |
Если коротко, `source ./venv/bin/activate`
