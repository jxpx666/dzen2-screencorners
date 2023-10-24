# DESCRIPTION
> `dzen2-screencorners` is is nothing more than an one-liner bash script that draws four black coloured widgets of `dzen2` 1x1 pixel sized positioned at the corners of the screen (+0+0, TopLeft [tl], +0-1, BottomLeft [bl], -1+0, TopRight [tr], -1-1, BottomRight [br]) and that can perform arbitrary commands in response to mouse and keyboard input.

# INSTALL
1. Move `dzen2-screencorners` (the bash script) to your `$PATH`
2. Move `.dzen2-screencorners` (the dotfile) to your `$HOME`
3. Append `dzen2-screencorners`  to your personal application autostart service (`.xprofile`, `.xsession`, or .`xinitrc`) a line like this one: `( sleep 4 ; dzen2-screencorners & ) &`  
4. Configure `.dzen2-screencorners` with your own preferences.

# OBS.:

1. `NOP`
> Lines of `.dzen2-screencorners` containing the `nop` command will not be sourced. You may also delete any lines you want from the dotfile (`.dzen2-screencorners`).

2. `ENTERTITLE`, `LEAVETITLE`
> Leave `*entertitle=grabkeys` and `*leavetitle=ungrabkeys` if you want to use the Keyboard. If you want to execute another command on `entertitle` or `leavetitle` action you can configure your dotfile (`.dzen2-screencorners`) with a line like this one: `tl*leavetitle=ungrabkeys,exec:xmessage "Hello World!"`.

3. `SYNTAX HIGHLIGHT`
You can use the `Xresources` file format syntax highlight in order to edit comfortably the `.dzen2-screencorners` dotfile. 

4. TRANSPARENCY
> If you hack the bash script to draw bigger squares or retangles of `dzen2` in arbitrary geometries (size and position) or modes, you can use `xcompmgr` alongside with `xorg-transset`, to make it transparent.

5. `MORE INFO`
> You can obtain more information about actions, options, arguments, keys, etc. supported by `dzen2-screencorners` in the `dzen2` official documentation. 

# OTHER THINGS...

1. `SHEET LIST`
> You can obtain a "sheet list" to remember your own configuration and even control some aspects of `dzen2-screencorners` with a script like this one: 

```
xmessage -buttons TopLeft,BottomLeft,TopRight,BottomRight,Dotfile,Script,Reload "$(echo -e 'dzen2\nscreencorners'|figlet)";

case "$?" in
	101)
	xmessage "$(cat $HOME/.dzen2-screencorners|grep -e "tl\\*" -e "TopLeft" |grep -e "nop" -v|sed 's/tl\*//g'|paste - -s -d "\n")" && dzen2-screencorners -i
	;;
	102)
	xmessage "$(cat $HOME/.dzen2-screencorners|grep -e "bl\\*" -e "BottomLeft" |grep -e "nop" -v|sed 's/bl\*//g'|paste - -s -d "\n")" && dzen2-screencorners -i
	;;
	103)
	xmessage "$(cat $HOME/.dzen2-screencorners|grep -e "tr\\*" -e "TopRight" |grep -e "nop" -v|sed 's/tr\*//g'|paste - -s -d "\n")" && dzen2-screencorners -i
	;;
	104)
	xmessage "$(cat $HOME/.dzen2-screencorners|grep -e "br\\*" -e "BottomRight" |grep -e "nop" -v|sed 's/br\*//g'|paste - -s -d "\n")" && dzen2-screencorners -i
	;;
	105)
	gio open  $HOME/.dzen2-screencorners
	;;
	106)
	gio open $HOME/.local/bin/dzen2-screencorners
	;;
	107)
	killall dzen2 && dzen2-screencorners
	;;
esac
```

# BLACKBOX 0.77 COMPATIBILITY

>To control `dzen2-screencorners` directly from my Blackbox 0.77 Root Main Menu, I used to run a script like this one:

```
(
echo -e "[submenu] (TopLeft) {PID: $(xdotool search --any 'dzen2-TopLeft' getwindowpid)}" &&
echo -e "[exec] (SIGUSR1 TopLeft) {kill -SIGUSR1 $(xdotool search --any 'dzen2-TopLeft' getwindowpid)}" &&
echo -e "[exec] (SIGUSR2 TopLeft) {kill -SIGUSR2 $(xdotool search --any 'dzen2-TopLeft' getwindowpid)}" &&
echo -e "[exec] (Sheet) {xmessage "$(cat $HOME/.dzen2-screencorners|grep -e "tl\\*"|grep -e "nop" -v|sed 's/tl\*//g'|paste - -s -d "\n")"}" &&
echo -e "[end]" &&
echo -e "[submenu] (BottomLeft) {PID: $(xdotool search --any 'dzen2-BottomLeft' getwindowpid)}" &&
echo -e "[exec] (SIGUSR1 BottomLeft) {kill -SIGUSR1 $(xdotool search --any 'dzen2-BottomLeft' getwindowpid)}" &&
echo -e "[exec] (SIGUSR2 BottomLeft) {kill -SIGUSR2 $(xdotool search --any 'dzen2-BottomLeft' getwindowpid)}" &&
echo -e "[exec] (Sheet) {xmessage "$(cat $HOME/.dzen2-screencorners|grep -e "bl\\*"|grep -e "nop" -v|sed 's/tl\*//g'|paste - -s -d "\n")"}" &&
echo -e "[end]" &&
echo -e "[submenu] (TopRight) {PID: $(xdotool search --any 'dzen2-TopRight' getwindowpid)}" &&
echo -e "[exec] (SIGUSR1 TopRight) {kill -SIGUSR1 $(xdotool search --any 'dzen2-TopRight' getwindowpid)}" &&
echo -e "[exec] (SIGUSR2 TopRight) {kill -SIGUSR2 $(xdotool search --any 'dzen2-TopRight' getwindowpid)}" &&
echo -e "[exec] (Sheet) {xmessage "$(cat $HOME/.dzen2-screencorners|grep -e "tr\\*"|grep -e "nop" -v|sed 's/tl\*//g'|paste - -s -d "\n")"}" &&
echo -e "[end]" &&
echo -e "[submenu] (BottomRight) {PID: $(xdotool search --any 'dzen2-BottomRight' getwindowpid)}" &&
echo -e "[exec] (SIGUSR1 BottomRight) {kill -SIGUSR1 $(xdotool search --any 'dzen2-BottomRight' getwindowpid)}" &&
echo -e "[exec] (SIGUSR2 BottomRight) {kill -SIGUSR2 $(xdotool search --any 'dzen2-BottomRight' getwindowpid)}" &&
echo -e "[exec] (Sheet) {xmessage "$(cat $HOME/.dzen2-screencorners|grep -e "br\\*"|grep -e "nop" -v|sed 's/tl\*//g'|paste - -s -d "\n")"}" &&
echo -e "[end]"
) > ~/.blackbox/include/dzen2-screencorners &
```

And a menu entry like this one: 

```
	[submenu] (Screencorners) {dzen2-screencorners}
		[exec] (dzen2-screencorners) {gio open ~/.local/bin/dzen2-screencorners}
		[exec] (.dzen2-screencorners) {gio open ~/.dzen2-screencorners}
		[sep]
		[include] (~/.blackbox/include/dzen2-screencorners)
		[sep]
		[exec] (Killall) {killall dzen2}
		[exec] (Play) {dzen2-screencorners}
	[end]
```

