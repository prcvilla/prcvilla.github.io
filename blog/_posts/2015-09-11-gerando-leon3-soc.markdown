---
layout: post
title: "Gerando um SoC com LEON3"
date: 2015-09-11 17:00:00
categories: leon3
---

* Antes de iniciar e' necessario ter as ferramentas do FPGA corretamente instaladas no computador host.
  * Fiz este tutorial com a placa de desenvolvimento ML402 da Xilinx com um FPGA Virtex 4, portanto e' necessario o ISE 14.7 funcionando, bem como os cabos JTAG.
  * No caso da Xilinx, e' necessario executar o script de configuracao das ferramentas para ficarem acessiveis no terminal.

Exemplo:
{% highlight bash %}
. /opt/Xilinx/14.7/ISE_DS/settings64.sh
{% endhighlight %}

* Baixar no site da Gaisler o [LEON3/GRLIB source code][leon3-grlib]
  * Neste exemplo foi baixado a versao: grlib-gpl-1.4.1-b4156
* Descompactar em um local conhecido
* Na raiz da pasta descompactada, existe uma subpasta 'designs', onde todos os FPGA/placas suportadas estao disponiveis.

Exemplo:
{% highlight bash %}
grlib-gpl-1.4.1-b4156/designs/leon3-xilinx-ml40x/
{% endhighlight %}

* Acessar o diretorio desejado e executar a ferramenta de geracao do SoC LEON3 com o comando:
{% highlight bash %}
make xgrlib
{% endhighlight %}

* Nesta mesma pasta, existe um arquivo README.txt com as informacoes da configuracao padrao, como mapeamento de memorias, LEDs, switches, etc.
* A opcao xgrlib e' para fazer a simulacao, sintese e implementacao do SoC, caso deseje modificar o LEON3, basta clicar na opcao xconfig.
* Alternativamente, pode-se chamar diretamente a opcao xconfig com o make, modificar o LEON3 e salvar a configuracao.
* Uma vez satisfeito com a configuracao do LEON3, basta selecionar a ferrameta de sintese e rodar.
  * Neste caso: Xilinx ISE e pressionar 'Run'.
* No caso de estar tudo certo, vai ser gerado uma imagem (.bit) para o FPGA com o nome de `leon3mp.bit`
* Apos, basta gravar no FPGA e conectar usando o GRMON.

[leon3-grlib]: http://www.gaisler.com/index.php/downloads/leongrlib
