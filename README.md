# Stratavane_Browser
cool ah browser
,Stratavane Browser: install guide
A step-by-step guide to installing, running and updating Stratavane Browser on Linux. Keep it for next time you set up a new machine.
1. What you need
• Linux with Python 3.10 or newer (check with python3 --version).
• PyQt6 with WebEngine. This is the browser engine and it is required.
• Optional, only for the VPN features:
    ◦ openvpn for .ovpn profiles
    ◦ wireguard-tools for WireGuard .conf profiles
    ◦ polkit (provides pkexec) to ask for your password when needed
    ◦ iptables for the kill switch
    ◦ i2pd for .i2p sites
2. Install the packages
Pick your distribution.
Arch / Manjaro / EndeavourOS
sudo pacman -S python-pyqt6 python-pyqt6-webengine openvpn wireguard-tools polkit iptables i2pd
Debian / Ubuntu / Mint
sudo apt install python3-pyqt6 python3-pyqt6.qtwebengine openvpn wireguard-tools policykit-1 iptables i2pd
Fedora
sudo dnf install python3-pyqt6 python3-pyqt6-webengine openvpn wireguard-tools polkit iptables i2pd
Any distribution, using pip (if the packages above do not exist)
python3 -m venv ~/stratavane-env
~/stratavane-env/bin/pip install PyQt6 PyQt6-WebEngine
Then run the browser with ~/stratavane-env/bin/python Stratavane_Browser.py instead of python3.
If you only want the browser and do not need the VPN, I2P or kill switch, you can install just the first two packages.
3. Put the file in place
1. Copy stratavane_browser.py to your home folder, for example ~/Stratavane_Browser.py.
2. Do not run it with sudo. The browser refuses to start as root, and it asks for your password by itself only when a feature needs it (connect, kill switch, MAC changer, I2P).
4. Run it
python3 Stratavane_Browser.py
Useful options:
• --software turns off GPU rendering. Use it if the site thumbnails come out black.
• You can pass addresses to open them, for example python3 Stratavane_Browser.py https://example.com.
The terminal message GBM is not supported with the current configuration. Fallback to Vulkan rendering is only a graphics notice from Chromium. It is not an error.
5. Add a menu launcher (optional)
Create the file ~/.local/share/applications/stratavane.desktop with this content. Replace YOURNAME with your username.
[Desktop Entry]
Type=Application
Name=Stratavane Browser
Exec=python3 /home/YOURNAME/Stratavane_Browser.py
Terminal=false
Categories=Network;WebBrowser;
It then shows up in your application menu. If you used the pip method, put the full path of the venv python in Exec.
A shortcut for the terminal also works. Add this to your shell config:
alias stratavane='python3 ~/Stratavane_Browser.py'
6. First run: adding a VPN profile
1. Open the Stratavane page (it is the new tab page), or press F9 for the Shield panel.
2. Add your profile in either way:
    ◦ Drag the .ovpn or .conf file anywhere onto the window.
    ◦ Press Browse Custom .ovpn File and pick it in your file manager.
3. Select the profile. For VPNBook, press Fetch / Sync VPNBook Bundles to download the profiles and the current login.
4. Enter the username and password if the profile needs them, then press Connect. Approve the password prompt.
5. When connected, the address bar shows Protected.
If a profile contains scripts that run as root (lines such as up, down or PostUp), the browser warns you when you import it. Only accept profiles you trust.
7. Useful shortcuts
Key
Action
Ctrl+T
New tab
Ctrl+Shift+P
New private tab
Ctrl+W
Close tab
Ctrl+L
Focus the address bar
Ctrl+D
Bookmark the page
Ctrl+F
Find in page
Ctrl+H
Bookmarks and history
Ctrl+Shift+F
Search results panel
F9
Shield (VPN) panel
Ctrl+,
Settings
8. Customize it
Press Ctrl+, to open Settings. There you can move the tab bar (top, bottom, left, right), move the address bar, pick a theme, choose where the search results panel sits, and change the new tab page.
Apply the theme to Firefox
1. Open Settings, then the Firefox page.
2. Tick Apply this theme to Firefox automatically.
3. Close Firefox and open it again.
To undo it, press Remove the theme from Firefox on the same page.
9. Updating
Replace ~/Stratavane_Browser.py with the new file. Your settings, bookmarks, history and VPN profiles stay, because they are stored separately (see the next section).
10. Where your data lives
• ~/.stratavane holds settings, bookmarks, history, thumbnails and your imported VPN profiles.
• ~/.vpnbook holds the profiles synced from VPNBook.
• ~/.stratavane-browser-profile holds the browser cache and cookies.
11. Uninstall
1. Delete ~/Stratavane_Browser.py and the launcher file if you made one.
2. To also remove your data, delete the three folders listed above.
3. If you applied the Firefox theme, remove it first from Settings, Firefox, Remove the theme from Firefox.
12. Troubleshooting
Problem
Fix
Missing dependency message at start
Install PyQt6 and WebEngine (section 2).
Window does not open, or an error about root
Do not use sudo. Run it as your normal user.
Connect does nothing or no password prompt
You need a polkit authentication agent running. On a minimal desktop install one, for example polkit-gnome or lxqt-policykit.
Kill switch says it needs a VPN first
Connect to a VPN first, then turn the kill switch on.
openvpn is not installed
Install openvpn (section 2).
.i2p sites do not load
Install i2pd and press Start in the I2P section of the Shield panel.
Thumbnails are black
Start with python3 Stratavane_Browser.py --software.
Firefox did not change colors
Restart Firefox fully. Make sure the right profile is selected in Settings, Firefox.
