## Fixing Ubuntu Hyper-V conflicts
This was a fix for the weird double click behavior happening with 
mouse side buttons.  seems like when the button is physically pressed
2 events are interpreted: button down and button release.  The same 2
events are interpreted when the buttin is physically released.

Tried a few fixes proposed but the one that ended
 up working best is making it so that the horizontal scroll
 get mapped to forward and back 
```shell script
mouseId=`xinput list | grep -Po "xrdpMouse \K.*id=\K([0-9])"`
xinput set-button-map $mouseId 1 2 3 4 5 8 9 0 0
unset mouseId
```