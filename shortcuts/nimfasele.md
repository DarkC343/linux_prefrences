# نیم‌فاصله در کیبورد
## مقدمه
سلام‌ در این بخش آموزش استفاده راحت از نیم‌فاصله را در لینوکس تحت GNOME یاد خواهیم گرفت. نیم‌فاصله یک کاراکتر Zero-width Non-joiner می‌باشد که توسط کد 'U+200C' می‌توان آن را تولید کرد. برای مثال، در Fedora با یک لحظه نگهداری کلید Ctrl+Shift+u و سپس تایپ 
 200C می‌توان نیم‌فاصله تولید کرد. کار سختی است!

استفاده از نیم‌فاصله در صفحه کلید iOS ساده است، زیرا کنار کلید Space است. در این‌جا یاد می‌گیریم عملکرد کلید 'Right Alt' در رایانه شخصی‌مون را به نیم‌فاصله تغییر دهیم.

## مراحل
### Nimfasele defitinion
Edit `/usr/share/X11/xkb/symbols/ir` as super-user to define a new custom keyboard. We reuse standard "ir(winkeys)" with additional changes.
```
partial alphanumeric_keys
xkb_symbols "Nimfasele" {
    name[Group1]= "Persian (with Nimfasele)";
    include "ir(winkeys)"

    // Map Shift+Space to ZWNJ        --> good for google-chrome and every other program.
    key <SPCE> { [ space, U200C ] };
    // Map Shift+F7 to ZWNJ           --> good for skype that correctly renders "U+2067" unicode character to Nimfasele.
    key <FK07> { [ F7, U2067 ] };
};
```

Edit `/usr/share/X11/xkb/rules/evdev.xml` as super-user to add a new keyboard to the OS setting.
```
<variant>
   <configItem>
    <name>Nimfasele</name>
    <description>Persian (with Nimfasele)</description>
  </configItem>
</variant>
```

Logout/restart is required to make changes work. Then, add `Persian (with Nimfasele)` from keyboard settings.

### [keyd](https://github.com/rvaiya/keyd/) setup

Add current user (yourself) to `keyd` group.
```
sudo usermod -aG keyd <USER>
```

Edit `/etc/keyd/default.conf` as super user to map right-alt to shift+space. In Chrome, right-alt with persian keyboard causes the '3-dot' icon on the top-right to be highlighted/hovered, which we prevent and assign it to Nimfasele.
```
[ids]
*

[main]
rightalt = macro(leftshift+space)
```

Make above setting work.
```
sudo keyd reload
```

Steps to enable application-specific keyboard rules include installing the shell-extension from the disk. You may follow [this](https://github.com/rvaiya/keyd/blob/9c758c0e152426cab3972256282bc7ee7e2f808e/scripts/keyd-application-mapper#L418) to do it accurately.
```
rm -r ~/.local/share/gnome-shell/extensions/keyd
mkdir -p ~/.local/share/gnome-shell/extensions
ln -s /usr/local/share/keyd/gnome-extension-45 ~/.local/share/gnome-shell/extensions/keyd
gnome-extensions enable keyd
mkdir ~/.config/keyd
echo "[skype]" > ~/.config/keyd/app.conf
echo "rightalt = macro(leftshift+f7)" >> ~/.config/keyd/app.conf
keyd-application-mapper
```

You may need to debug the procedure using `sudo keyd monitor` and `keyd-application-mapper -v` commands.
