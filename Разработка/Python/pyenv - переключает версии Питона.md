Собирает из исходников - это самое плохое. Ебучая сложная установка. Альтернатива - [[conda или miniconda]].
# Установка
`curl https://pyenv.run | bash`
Затем ещё это. Неизвестно, обязательно или нет:
*First, add the commands to `~/.bashrc` by running the following in your terminal:*
```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```
*Then, if you have `~/.profile`, `~/.bash_profile` or `~/.bash_login`, add the commands there as well. If you have none of these, add them to `~/.profile`. to add to `~/.profile`:*
```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.profile
```
И пришлось ещё перезагрузить потом.
`pyenv install 3.10`
Будет жаловаться, что нет компилятора C++, тогда надо поставить:
`sudo apt install build-essential`
==TODO== Так и не закончил