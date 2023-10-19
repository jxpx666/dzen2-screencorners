# INSTALL

1. Put the `dzen2-screencorners` into your $PATH
2. Put the `.dzen2-screencorners` at your $HOME
3. Put the `dzen2-screencorners` into your autostart (.xprofile, .xsession, or .xinitrc). Something like: `( sleep 4 ; dzen2-screencorners & ) &`.
4. Configure `.dzen2-screencorners` with your own preferences.


# OTHER THINGS...
To control the dzen2-screencorners on my Blackbox Menu, I use a script like that:

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

And a Menu entry like that: 
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



