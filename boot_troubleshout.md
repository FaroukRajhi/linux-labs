# Change grub's default timeout from 1 seconds to 5 second.

Edit /etc/default/grub file:

sudo vi /etc/default/grub



change


GRUB_TIMEOUT=1


to


GRUB_TIMEOUT=5
# Install grub to /dev/vda
sudo grub2-install /dev/vda

