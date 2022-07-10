<h1 align=center>
  <b>Born2beroot</b>
</h1>
<p align=center>
  Neste projeto iremos criar uma máquina virtual e utiliza-la como um servidor seguindo regras específicas. O projeto permite   a utilização de duas distribuições Linux diferentes, podemos usar a <b> CentOs </b> ou a <b> Debian </b>.
  Para esta implementação eu escolhi usar a Debian.
</p>
<h1 align=center>
  <b>Debian 11</b>
</h1>
<p align=center>
  Debian é uma distribuição GNU/Linux composta integralmente de software grátis e open-source. É tambem uma das mais antigas distruibuições baseadas no Kernel Linux. Debian é a base de muitas outras distribuições, incluindo a muito popular <b>Ubuntu</b>.
</p>

<p align=center>
  Debian tem uma das maiores e ativas comunidades online, o que pode ser uma mão na roda para procurar ajuda para corrigir erros, bugs ou encontrar tutoriais. O que a torna uma boa escolha para este projeto.
</p>

<p align=center>
  Debian também é conhecida por ser uma distribuição estável, recebendo atualizações em sua versão stable apenas após terem sido exaustivamente testadas e por um longo período de tempo. O que também a torna uma escolha popular para servidores.
</p>

## :warning: Atenção!

Este repositório foi criado como um guia pessoal, contendo as minhas próprias anotações de como eu desenvolvi o projeto. Não deve ser utilizado como um manual completo de como entregar o projeto. Alguns conceitos podem ou não serem descritos aqui e você pode precisa-los para a sua defesa. Qualquer dúvida sobre algum comando ou conceito utilizado aqui deve ser resolvido fazendo a sua própria pesquisa.

## Pré-Requisitos

Para desenvolver este projeto será necessário o uso do programa `VirtualBox` e de uma imagem de instalação <b>estável</b> do `Debian`.

- <a href="https://www.virtualbox.org/wiki/Downloads">VirtualBox</a>
- <a href="https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-11.4.0-amd64-netinst.iso">debian-11.4.0-amd64-netinst.iso.</a>

## Instalação

Não ha muito segredo em criar uma máquina virtual. Após instalar o `VirtualBox` e clicar em novo, todo processo é bastante intuitivo, apenas certifique-se de liberar uma quantidade razoável de memória ram para sua máquina virtual. A única parte que irá fazer alguma diferença aqui para o nosso projeto é o tamanho do disco virtual. Caso escolha fazer apenas o mandatório do projeto 8.0GB é o suficiente. Para a parte bônus iremos precisar de algo em torno de 30.8GB para criar todas as outras partições pedidas pela guideline do projeto.

Criada a nossa máquina virtual teremos que adicionar a imagem baixada anteriormente do Debian a sua controladora IDE. Tornando possível para que a nossa recém criada máquina virtual encontre o disco de boot para começarmos a nossa instalação.

Selecione a sua máquina virtual, clique em configurações, clique em armazenamento, selecione disco vazio abaixo de Controladora: IDE e clique no ícone de disco ao lado de IDE Secundário Master e selecione a opção Escolher uma imagem de disco. Na nova janela que irá abrir apenas selecione a imagem baixada do Debian.

![Captura de tela 2022-07-10 060515](https://user-images.githubusercontent.com/97175725/178138463-0013bd68-4d04-46a3-b1bb-53b2f35c0363.png)

Feito isso, volte ao programa e clique em Iniciar para iniciar a nossa máquina virtual.
Se tudo tiver sido feito de maneira correta a maquina devera iniciar dando boot no Debian e aparecendo suas opções de instalação.

![Captura de tela 2022-07-10 061302](https://user-images.githubusercontent.com/97175725/178138658-6af7b24b-6b83-490d-b180-8f06d48a351f.png)

Selecione a segunda opção (Install). Como não é permitido a instalação de servidores gráficos ou qualquer ambiente de desktop, usando apenas a opção Install certificaremos que não instalaremos nada a mais do que precisamos.

A primeira coisa a se fazer é escolher uma linguagem para o sistema e para o processo de instalação. Eu utilizei a linguagem que vem por padrão e deixei em inglês. Após isso tera algumas telas de configuração de região e keymap. A keymap é importante que você selecione o layout correto do seu teclado para não ter problemas futuros, neste caso escolhi o keymap de português.

Agora aparecerá a tela de hostname, de acordo com a guideline do projeto você devera usar um hostname específico. Mas como podemos trocar isso após a instalação e deveremos saber como fazer, pode ser útil em termos de aprendizado deixar o que vem por padrão e aprender a trocar o hostname para o que é pedido após a instalação. O mesmo processo vale para nomes de usuário e senhas durante esta pré configuração. Tendo isto em mente, deixei tudo por padrão, selecionei nomes e senhas fáceis de usar e lembrar. Vou seguir com a régua pedida pelo projeto no pós da instalação.

