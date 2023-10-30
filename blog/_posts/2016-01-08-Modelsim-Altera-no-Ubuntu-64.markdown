---
layout: post
title: "Modelsim Altera Edition no Ubuntu 64"
date: 2016-01-08 12:00:00
categories: Modelsim Ubuntu
---

Sem muitos segredos, baixei a última versão (ModelSimSetup-15.0.0.145-linux.run) no site da [altera][altera-dl]. Após, basta dar permissão de execução (`chmod +x`) e rodar o instalador (`./ModelSimSetup-15.0.0.145-linux.run`).

Um detalhe é que o modelsim é 32-bits, e no meu caso faltou uma biblioteca (libxft2).
Para isso, basta instalar:

{% highlight bash %}
sudo apt-get install libxft2:i386
{% endhighlight %}

Para abrir o modelsim, navegue ate o diretório do binário e execute `./vsim`.

Ou, se preferir, um script:

{% highlight bash %}
#!/bin/bash
export PATH=$PATH:/opt/altera/15.0/modelsim_ase/linuxaloem/
vsim
{% endhighlight %}

Este [link][post-modelsim] possui diversas soluções para o mesmo problema.

[altera-dl]: http://dl.altera.com/
[post-modelsim]: http://mattaw.blogspot.com.br/2014/05/making-modelsim-altera-starter-edition.html

