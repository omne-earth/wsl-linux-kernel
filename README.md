git clone git@github.com:omne-earth/wsl-linux-kernel.git
git submodule init

sudo dnf update
sudo dnf group install "Development Tools"
sudo dnf install -y ncurses-devel openssl-devel elfutils-libelf-devel bc python3 cpio flex bison openssl-devel-engine

cd WSL2-Linux-Kernel
cp Microsoft/config-wsl .config
sed -i 's/CONFIG_USBIP_VHCI_HCD=m/CONFIG_USBIP_VHCI_HCD=y/g' .config
make -j$(nproc)

sudo make modules_install headers_install

cp arch/x86/boot/bzImage /mnt/c/Users/shree/.wsl-kernels/vhci/

wsl --shutdown
[wsl2]
kernel=C:\\Users\\shree\\.wsl-kernels\\vhci\\bzImage

uname -r
modinfo vhci-hcd
sudo modprobe vhci-hcd
lsmod | grep vhci_hcd

