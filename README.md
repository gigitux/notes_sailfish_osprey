# notes_sailfish_osprey
#fix build hal
cd hybris/droid-hal-version-$DEVICE
ARCH=armv7hl
LOCAL_REPO=$ANDROID_ROOT/droid-local-repo/$DEVICE/
mb2 -t $VENDOR-$DEVICE-$ARCH \
 -s rpm/droid-hal-version-$DEVICE.spec \
 build || die
 mv -v RPMS/*.rpm $LOCAL_REPO
 cd ../../
 createrepo $LOCAL_REPO
 sb2 -t $VENDOR-$DEVICE-$ARCH -R -m sdk-install \
 zypper ref
