### Установка виртуальной машины Win на **OpenVZ**

[**___оригинал тут___**](https://www.tomvanbrienen.nl/how-to-create-windows-server-2016-2019-vms-openvz-7/)

Создать шаблон ВМ командой. Откуда взято win-2016 не поянтно. В документации пока ничего не нашел.

`prlctl create SRV-WIN2019 --distribution win-2016 --vmtype vm`

Добавить созданному шаблону образ диска из которого будет выполняться установка

`prlctl set SRV-WIN2019 --device-add cdrom --image /root/downloads/server2019.iso`

Настроить доступ через VNC к созданной ВМ

`prlctl set SRV-WIN2019 --vnc-mode manual --vnc-port 5905 --vnc-passwd YourPassword`

Установить адрес, шлюз, ДНС

`prlctl set SRV-WIN2019  --device-set net0 --ipadd X.X.X.X/24 --gw X.X.X.X \
--nameserver 8.8.8.8`

Установить доступное количество процессоров, объем памяти, жесткого диска.

`prlctl set SRV-WIN2019  --cpus 2`

`prlctl set SRV-WIN2019 --memsize 4G`

`prlctl set SRV-WIN2019 --diskspace 80G`

Установить лимит скорости записи на диск - MB/s

`prlctl set SRV-WIN2019 --iolimit 50`

Установить дополнения OpenVZ

`prlctl installtools SRV-WIN2019`


Поддерживаемые ОС
```
The following values are allowed:
win-2008                win-2012                win-2016                ubuntu
fedora-core             debian                  centos                  centos7
vzlinux                 vzlinux7                cloudlinux              cloudlinux7
opensuse
Experimental support:
win-2000                win-xp                  win-2003                win-vista
win-7                   win-8                   win-8.1                 win-10
win                     rhel                    rhel7                   suse
sles11                  sles12                  psbm                    redhat
mandriva                xandros                 mageia                  mint
linux-2.4               linux-2.6               linux                   freebsd
chrome                  msdos                   netware                 solaris
```
