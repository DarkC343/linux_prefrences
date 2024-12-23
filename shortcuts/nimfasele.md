# نیم‌فاصله در کیبورد
## مقدمه
سلام‌ در این بخش آموزش استفاده راحت از نیم‌فاصله را در لینوکس تحت GNOME یاد خواهیم گرفت. نیم‌فاصله یک کاراکتر Zero-width Non-joiner می‌باشد که توسط کد 'U+200C' می‌توان آن را تولید کرد. برای مثال، در Fedora با یک لحظه نگهداری کلید ؟ و سپس تایپ 
 200C می‌توان نیم‌فاصله تولید کرد. کار سختی است!

استفاده از نیم‌فاصله در صفحه کلید iOS ساده است، زیرا کنار کلید Space است. در این‌جا یاد می‌گیریم عملکرد کلید 'Right Alt' در رایانه شخصی‌مون را به نیم‌فاصله تغییر دهیم.

## مراحل
```
sudo usermod -aG keyd <USER>
sudo vim /usr/share/X11/xkb/symbols/ir
sudo vim /usr/share/X11/xkb/rules/evdev.xml
<variant>
   <configItem>
    <name>Nimfasele</name>
    <description>Persian (with Nimfasele)</description>
  </configItem>
</variant>
rm -r ~/.local/share/gnome-shell/extensions/keyd
mkdir -p ~/.local/share/gnome-shell/extensions
ln -s /usr/local/share/keyd/gnome-extension-45 ~/.local/share/gnome-shell/extensions/keyd
gnome-extensions enable keyd
mkdir ~/.config/keyd
echo "[google-chrome]" > ~/.config/keyd/app.conf
echo "rightalt = macro(leftshift+space)" >> ~/.config/keyd/app.conf

keyd-application-mapper -v

partial alphanumeric_keys
xkb_symbols "Nimfasele" {
    name[Group1]= "Persian (with Nimfasele)";
    include "ir(winkeys)"

    // Map Right Alt and Shift+Shift to ZWNJ
    key <RALT> { [ U200C ] };
    key <SPCE> { [ space, U200C ] };
};
```
