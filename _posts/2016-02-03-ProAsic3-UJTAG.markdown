---
layout: post
title: "ProAsic3 UJTAG"
date: 2016-02-03 12:00:00
categories: ProASIC3e jtag microsemi
---

Comecei a trabalhar com o FPGA ProASIC3e da Microsemi (antiga Actel) para rodar alguns testes de radiação. Como não é possível realizar a leitura da memória de configuração, fomos obrigados a encontrar uma alternativa para ler dados dentro do FPGA em tempo de execução.

Alguns FPGAs da Microsemi oferecem uma hard-macro que realiza a interface direta usando o JTAG, chamada UJTAG. Como exemplo existe o application note que mostra como usar ([AC227][ac227]). Porem este é para os FPGAs da linha ProASIC3plus.

Após algumas tentativas e modificações no código fornecido, foi obtido sucesso na comunicação. No exemplo é apresentado como realizar a escrita em FF dentro do FPGA.

No projeto que estamos desenvolvendo, era necessário também ler os dados, por isso existe uma pequena modificação que adiciona a possibilidade de leitura.

O processo de comunicação é todo baseado na FSM do JTAG ([Fig.3 AC227][ac227]), para "conversar" com o UJTAG é necessario executar o arquivo STP no FlashPro.

O projeto modificado está disponível neste [link]({{ site.url }}/downloads/how2useUJTAG.7z).  
O arquivo exemplo STP está localizado em `designer/impl1/TOP.stp`.


[ac227]: http://www.microsemi.com/document-portal/doc_view/129933-ac227-how-to-use-ujtag-app-note

