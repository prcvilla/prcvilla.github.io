---
layout: post
title: "Xilinx Platform Cable USB under Linux"
date: 2015-09-14 16:00:00
categories: Xilinx Platform Cable linux
---

Demorei um pouco para fazer funcionar o cabo, mas esse [link][xilinx-cable-drivers-linux] me ajudou.

Quatro passos fizeram funcionar de primeira:

> Deixar o cabo desconectado do USB.

* Instalar o `fxload` com `sudo apt-get install fxload`

* Criar o arquivo `/etc/udev/rules.d/xusbdfwu.rules` com o conteudo:
{% highlight bash %}
# version 0003
    ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0008", MODE="666"
    SUBSYSTEM=="usb", ACTION=="add", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0007", RUN+="/sbin/fxload -v -t fx2 -I /opt/Xilinx/14.7/ISE_DS/ISE/bin/lin64/xusbdfwu.hex -D $tempnode"
    SUBSYSTEM=="usb", ACTION=="add", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0009", RUN+="/sbin/fxload -v -t fx2 -I /opt/Xilinx/14.7/ISE_DS/ISE/bin/lin64/xusb_xup.hex -D $tempnode"
    SUBSYSTEM=="usb", ACTION=="add", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="000d", RUN+="/sbin/fxload -v -t fx2 -I /opt/Xilinx/14.7/ISE_DS/ISE/bin/lin64/xusb_emb.hex -D $tempnode"
    SUBSYSTEM=="usb", ACTION=="add", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="000f", RUN+="/sbin/fxload -v -t fx2 -I /opt/Xilinx/14.7/ISE_DS/ISE/bin/lin64/xusb_xlp.hex -D $tempnode"
    SUBSYSTEM=="usb", ACTION=="add", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0013", RUN+="/sbin/fxload -v -t fx2 -I /opt/Xilinx/14.7/ISE_DS/ISE/bin/lin64/xusb_xp2.hex -D $tempnode"
    SUBSYSTEM=="usb", ACTION=="add", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0015", RUN+="/sbin/fxload -v -t fx2 -I /opt/Xilinx/14.7/ISE_DS/ISE/bin/lin64/xusb_xse.hex -D $tempnode"
{% endhighlight %}

* Recarregar as regras do udev com `sudo udevadm control --reload-rule`

* Conectar o `Xilinx Platform Cable USB` e verificar a luz de indicação, se ficar verde com o FPGA conectado, tudo certo.

* Por fim, tive que instalar alguns pacotes para fazer a comunicação com o LEON3 usando o GRMON funcionar
  * Verifique as dependencias do GRMON com `ldd path/to/grmon/bin`
  * Buscar nos [pacotes do ubuntu][packages-ubuntu] as bibliotecas faltando e instalar.
    * Fazer a busca em `Search the contents of packages`
  * Ao rodar o GRMON, tive que instalar o libusb-0.1 com `sudo apt-get install libusb-0.1-4:i386`

[xilinx-cable-drivers-linux]: https://github.com/timvideos/HDMI2USB/wiki/Xilinx-Platform-Cable-USB-under-Linux
[packages-ubuntu]: http://packages.ubuntu.com/

