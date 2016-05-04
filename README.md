# notes_sailfish_osprey
#fix build hal 
add another repo to kss: <br>
http://repo.merproject.org/obs/home:/mal:/testing2/sailfishos_latest_armv7hl/ <br>
cd hybris/droid-hal-version-$DEVICE <br>
ARCH=armv7hl <br>
LOCAL_REPO=$ANDROID_ROOT/droid-local-repo/$DEVICE/ <br>
mb2 -t $VENDOR-$DEVICE-$ARCH \ <br>
 -s rpm/droid-hal-version-$DEVICE.spec \ <br>
 build || die  <br>
 mv -v RPMS/*.rpm $LOCAL_REPO <br>
 cd ../../ <br>
 createrepo $LOCAL_REPO <br>
 sb2 -t $VENDOR-$DEVICE-$ARCH -R -m sdk-install \ <br>
 zypper ref <br>
________________________________________
edit udev rules <br>
edit /lib/udev/rules.d/998-droid-system.rules <br>

last line <br>:

ENV{ID_PART_ENTRY_SCHEME}=="gpt", ENV{ID_PART_ENTRY_NAME}=="?*", IMPORT{program}="/bin/sh /lib/udev/platform-device $env{DEVPATH}", SYMLINK+="block/bootdevice/by-name/$env{ID_PART_ENTRY_NAME}"
