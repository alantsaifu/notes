https://linuxhint.com/compile-linux-kernel-centos7/ => total completed

Centos Kernel編譯rpm包
2022-01-29 雲計算基礎架構
參考：https://wiki.centos.org/HowTos/RebuildSRPM

Kernel source下載地址：https://vault.centos.org/centos/7.6.1810/updates/Source/SPackages/

建議使用非root用戶

創建相關目錄

[user@host]$ mkdir -p ~/rpmbuild/{BUILD,BUILDROOT,RPMS,SOURCES,SPECS,SRPMS}
[user@host]$ echo '%_topdir %(echo $HOME)/rpmbuild' > ~/.rpmmacros

下載kernel src包

wget https://archive.kernel.org/centos-vault/centos/7.6.1810/updates/Source/SPackages/kernel-alt-4.14.0-115.10.1.el7a.src.rpm

安裝相關包

[root@host]# yum install asciidoc audit-libs-devel bash bc binutils binutils-devel bison diffutils elfutils
[root@host]# yum install elfutils-devel elfutils-libelf-devel findutils flex gawk gcc gettext gzip hmaccalc hostname java-devel
[root@host]# yum install m4 make module-init-tools ncurses-devel net-tools newt-devel numactl-devel openssl
[root@host]# yum install patch pciutils-devel perl perl-ExtUtils-Embed pesign python-devel python-docutils redhat-rpm-config
[root@host]# yum install rpm-build sh-utils tar xmlto xz zlib-devel

解壓包生成source file

[user@host]$ cd ~/rpmbuild/SPECS
[user@host SPECS]$ rpmbuild -bp --target=$(uname -m) kernel.spec

編譯kernel

$cd /home/centos/rpmbuild/BUILD/kernel-alt-4.14.0-115.10.1.el7a/linux-4.14.0-115.10.1.el7a.x86_64$make rpm -j 30

編譯後生成相關文件

/home/centos/rpmbuild/RPMS/x86_64

kernel-4.14.0-1.x86_64.rpm  kernel-devel-4.14.0-1.x86_64.rpm  kernel-headers-4.14.0-1.x86_64.rpm

使用該rpm文件安裝kernel並設置從該kernel啓動
