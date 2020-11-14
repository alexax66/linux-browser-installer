### About

*linux-browser-installer* is a Bourne shell script to install Linux versions of
the Chrome or Brave browser under FreeBSD into a Linux (Ubuntu Bionic) jail.
The script is based on the excellent [Howto](https://forums.freebsd.org/threads/linuxulator-how-to-run-google-chrome-linux-binary-on-freebsd.77559/) by @[patovm04](https://github.com/patovm04).

If not defined otherwise, Ubuntu Bionic (`$ubuntu_version`) is installed under
`/compat/ubuntu` (`$jail_path`). A modified version of FreeBSD's linux rc-script
(`rc.d/ubuntu`) is used to start the *linuxulator*.

### Please Note

You can't run different Linux jails at the same time. If you want to run
CentOS-based applications under `/compat/linux`, you have to set
`sysctl compat.linux.emul_path=/compat/linux`, and start the linux rc-script
(`service linux onestart`). Depending on which jail you intend to use by
default, set either (not both) `linux_enable="YES"` or `ubuntu_enable="YES"`
in `/etc/rc.conf`.

### Usage
#### Install Chrome or Brave browser

````
# ./linux-browser-installer install chrome
````

and/or

````
# ./linux-browser-installer install brave
````
If the jail is not existing yet, it will be created first.

#### Deinstall Chrome or Brave browser

````
# ./linux-browser-installer deinstall chrome
````

and/or

````
# ./linux-browser-installer deinstall brave
````

This command deinstalls the browser, and removes its wrapper
scripts from `/usr/local/bin` and `$jail_path/bin` along with its
desktop file.

#### Create jail

````
# ./linux-browser-installer jail create
````

#### Upgrade software installed in the jail

````
# ./linux-browser-installer jail upgrade
````

#### Delete jail

````
# ./linux-browser-installer jail delete
````
Before deleting the entire jail under `$jail_path`, this command
unmounts all the jail's filesystems, and removes their
entries from `/etc/fstab`, deletes the rc script, and removes its
variable(s) from `/etc/rc.conf`.

#### Update symlinks for icons and fonts

````
# ./linux-browser-installer symlink fonts
````
This command updates the symlinks from `$prefix/share/fonts`
`$jail_path/usr/share/fonts`. Use this after installing new fonts
to make them available to applications in the jail.

````
# ./linux-browser-installer symlink icons
````

This command updates the symlinks from `$prefix/share/icons` to
`$jail_path/usr/share/icons`. Use this after installing new icons
to make them available to applications in the jail.

#### Delete working files from current directory
````
# ./linux-browser-installer clean
````