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
Se tudo tiver sido feito de maneira correta a máquina devera iniciar dando boot no Debian e aparecendo suas opções de instalação.

![Captura de tela 2022-07-10 061302](https://user-images.githubusercontent.com/97175725/178138658-6af7b24b-6b83-490d-b180-8f06d48a351f.png)

Selecione a segunda opção (Install). _Como não é permitido a instalação de servidores gráficos ou qualquer ambiente de desktop, usando apenas a opção Install certificaremos que não instalaremos nada a mais do que precisamos._

A primeira coisa a se fazer é escolher uma linguagem para o sistema e para o processo de instalação. Eu utilizei a linguagem que vem por padrão e deixei em inglês. Após isso tera algumas telas de configuração de região e keymap. A keymap é importante que você selecione o layout correto do seu teclado para não ter problemas futuros, neste caso escolhi o keymap de português.

Agora aparecerá a tela de hostname, de acordo com a guideline do projeto você devera usar um hostname específico. Mas como podemos trocar isso após a instalação e deveremos saber como fazer, pode ser útil em termos de aprendizado deixar o que vem por padrão e aprender a trocar o hostname para o que é pedido após a instalação. O mesmo processo vale para nomes de usuário e senhas durante esta pré configuração. Tendo isto em mente, deixei tudo por padrão, selecionei nomes e senhas fáceis de usar e lembrar. E seguirei com a régua pedida pelo projeto no pós da instalação.

### Particionamento

Ainda dentro da instalação, precisaremos particionar o nosso disco. De acordo com o pedido pela guideline do projeto, deveremos fazer isso usando o `LVM` e criando ao menos 2 partições criptografadas (Mandatory). Se já tiver alguma experiência com particionamento pode se aventurar em usar o modo manual e criar as partições uma a uma. Para nos salvar alguem tempo basta selecionar a 3ª opção `Guided - use entire disk and set up encrypted LVM`.

Depois de selecionar o disco que iremos particionar, chegaremos nos esquemas de particionamento. Caso esteja fazendo apenas o mandatório basta selecionar `Separate /home partition`. Caso esteja fazendo o bônus selecione a última opção `Separate /home, /var, and /tmp partitions`. 
Crie uma passphrase forte para as partições encriptadas e anote em algum lugar. Isto será pedido sempre que iniciar o sistema. 
Como nossa máquina virtual e o disco criado para ser usada nela tem o único propósito de ser usado neste projeto é seguro dizer que você deve usar o máximo do disco para o particionamento.

Nesta parte de particionamento utilizamos o <b>Logical Volume Manager</b> ou LVM e é importante que se saiba o que é e porque o utlizamos nestre projeto.

### LVM
> **Logical Volume Manager** ou traduzido como Gerenciador de Volumes Lógicos, o nosso LVM, é um sistema para mapear e gerenciar memória de volumes de disco. Ela vem presente nos sistemas baseados no Kernel Linux e é um sistema mais flexível de lidar com os seus discos. Por exemplo, o sistema padrão de particionamento é limitado a criação de apenas 4 partições, com o LVM esta limitação não existe para a criação de volumes lógicos. Também podemos facilmente redimensionar esses volumes lógicos de acordo com a nossa necessidade. 
> Com a LVM os volumes físicos (Do nosso hardware) são combinados em _grupos de volume lógico_. Exceção a partição /boot/ que não pode estar em um grupo de volume lógico porque o gestor de inicialização não pode acessá-lo. Abaixo conceitos importantes para entender a LVM e como funciona.
- > **Grupo de volume lógico:** O grupo de volume lógico é dividido entre volumes lógicos, cada um pode ser atribuído seu ponto de montagem e seu tipo de sistema de arquivos. Quando um volume lógico atinge sua capacidade total, é possível adicionar espaço livre do grupo de volume lógico a este volume lógico e aumentar o seu tamanho. Se um novo disco rígido físico for adicionado ao sistema, ele pode ser adicionado ao grupo de volume lógico e os volumes lógicos contidos no grupo podem ser expandidos com o novo espaço livre. Tornando assim um sistema bem flexível e de fácil administração para seus discos.
- > **Volumes lógicos:** O correspondente as partições. Mas diferente delas, volumes lógicos podem utilizar de multiplos discos e não precisam estar físicamente contidos no mesmo disco.

Após estas configurações é só esperar a instalação do sistema base no disco.

Quando chegarmos nesta parte da instalação é importante que você desmarque todas as opções selecionadas com asterístico antes de clicar em Continue (Utilize o espaço para selecionar/deselecionar uma opção).

_**Não podemos instalar nenhum tipo de desktop environment!!!**_

![Captura de tela 2022-07-10 064455](https://user-images.githubusercontent.com/97175725/178139591-b070aa26-42a3-4ed1-a396-227e91febc83.png)

Instale o GRUB boot loader.
<a href="https://e-tinet.com/linux/grub/">O que é GRUB?</a>

Agora nossa instalação está completa! A máquina ira reiniciar sozinha e aparecerá o GRUB, basta apertar Enter (Ou aguardar alguns segundos que automaticamente ira confirmar a opção selecionada) e o nosso sistema irá iniciar.


