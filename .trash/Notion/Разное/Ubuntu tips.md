---
Created: 2022-03-14T00:54
Updated: 2022-03-14T00:55
---
# Disable Ctrl+Alt+Left Ctrl+Alt+Right to switch workspaces

> [!info] How to disable Gnome ctrl+alt+down and ctrl+alt+up shortcut?  
> Thanks for contributing an answer to Unix & Linux Stack Exchange!  
> [https://unix.stackexchange.com/questions/394143/how-to-disable-gnome-ctrlaltdown-and-ctrlaltup-shortcut](https://unix.stackexchange.com/questions/394143/how-to-disable-gnome-ctrlaltdown-and-ctrlaltup-shortcut)  

In general this can happen because the OS (window system) has  
priority and intercepts this shortcut and stops propagation to your  
desired application.  
Solution: Removing the shortcuts using  
`dconf-editor`:

- Open a terminal
- `sudo apt-get install dconf-tools` (or `dconf-editor`)
- Now run `dconf-editor`
- in dconf-editor go to: `/org/gnome/desktop/wm/keybindings/`
- Find `switch-to-workspace-down`, put `['disabled']` instead of `default`
- same for `switch-to-workspace-up`
- quit `dconf-editor` and you are done

I always have this problem when I want to use some Eclipse IDE shortcuts:  
  
[https://bugs.eclipse.org/bugs/show_bug.cgi?id=321094](https://bugs.eclipse.org/bugs/show_bug.cgi?id=321094)