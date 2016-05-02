# notes_sailfish_osprey
#fix build hal 
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
