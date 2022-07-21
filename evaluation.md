# Index

- [Como funciona uma máquina virtual](#como-funciona-uma-maquina-virtual)
- [A escolha do sistema operacional](#a-escolha-do-sistema-operacional)

## Como funciona uma máquina virtual:

> Uma máquina virtual cria um ambiente virtualizado entre o sistema host e o sistema (ou sistemas) client, tornando possível rodar um sistema operacional diferente dentro de outro. Onde os recursos da máquina física são divididos entre esses sistemas e são gerenciados pelo hypervisor.

## A escolha do sistema operacional:

> Debian. Escolhi o Debian por já ter alguma experiência prévia no uso e por ter uma comunidade maior e ser mais fácil de encontrar suporte.

## Diferenças básicas entre CentOS e Debian:

> Debian não existem firmwares non-free. O gerenciador de pacotes e seus formatos são diferentes, alguns arquivos de configuração ficam em diretórios diferentes, alguns programas padrões são diferentes e etc. A base é a mesma, o kernel Linux.

## O propósito de máquinas virtuais:

> Criação de servidores (Servidores normalmente requerem poucos recursos físicos disponíveis então é possível criar diversos servidores em máquinas virtuais diferentes na mesma máquina), testar aplicações com segurança sem correr riscos de danificar o sistema operacional real e testes de sistemas diferentes.

## A diferença entre apt e aptitude:

> O aptitude é um frontend para gerenciar os pacotes do sistema. Facilita a visualização dos pacotes instalados no sistema, remove-los, pesquisas. Dentre algumas de suas vantagens está o gerenciamento de dependências, quando você instala um pacote pelo APT junto de suas dependencias, quando você, posteriormente tentar remove-lo, o APT removerá apenas o pacote instalado e deixará as dependencias instaladas, já o APTITUDE desinsta-la tambem as dependencias que foram instaladas junto com o pacote. 

## O que é APPArmor:

> Camada de segurança do kernel responsável por gerenciar as permissões de uso dos recursos da máquina aos programas. Como acesso a rede, permissão para ler, gravar ou executar e acesso a aos recursos em geral da máquina. Funciona parecido com o modo de permissões de app em um dispositivo Android.

## Checar se o serviço UFW está ativo:

> sudo systemctl status ufw

## Checar se o serviço SSH está ativo:

>sudo systemctl status ssh

## Checar o sistema operacional em uso:

>uname -a - Todas as informações

>uname -v - Apenas a versão do kernel

## Checar se existe um usuário com as seguintes características:

>- O nome do usuário deve ser o login da intra
>- Ele deve pertencer ao grupo sudo e user42

> cat /etc/passwd - mostra todos os usuários do sistema

> groups <nomedousuario> - mostra todos os grupos ao qual o usuário pertence

## Criar um novo usuário:

> adduser <nomedousuário>

## Como as políticas de senhas foram feitas:

>Instalação do pwquality que permite criar algumas regras para as definições de senha.

>nano /etc/login.defs - Procure por PASS_MAX para achar as 3 primeiras regras

>nano /etc/security/pwquality.conf - Achar as outras regras


## Criar um grupo chamado "evaluating":

>addgroup <nomedogrupo>

## Porque o uso da política de senha:

> Tornar o sistema mais seguro e resistente a tentativas de quebra de senhas por força bruta.

## Checar o hostname (Deve ser igual ao login42):

> hostname

## Modificar o hostname pelo login do avaliador e que permaneça assim após o reboot da máquina:

> sudo hostnamectl set-hostname <novohostname>

## Restaurar o hostname original:

> hostname <nomeoriginal>

## Checar o esquema de partições:

> lsblk

## O que é LVM:

> É um gerenciador de volumes lógicos, que permite uma maior flexiblidade ao criar partições (volumes lógicos) e gerencia-las. O adm do sistema pode facilmente manejar espaço livre de um volume para outro conforme a necessidade, adionar novos volumes físicos a um grupo de volumes lógicos e aumentar sua capacidade sem que seja necessário a formatação e perda de dados dentro de cada volume lógico.

## Checar se o sudo está instalado:

> sudo apt-cache show sudo - Mostra o programa sudo instalado, versão, descrição e etc

> sudo dpkg -l - Mostra todos os programas instalados no sistema

## Adicionar o usuário recem criado ao grupo sudo:

> sudo adduser <nomedousuario> sudo

## Checar as regras para o sudo:

> cat /etc/sudoers.d/rules

## Checar se a pasta /var/log/sudo existe e tem um arquivo:

> cd /var/log/sudo

> ls -a

## Checar o conteúdo do arquivo desta pasta:

> cat sudo.log

## O que é UFW:

> Firewall do sistema, permite a criação de regras de entrada e saída pela rede.

## Listar regras ativas do UFW:

> sudo ufw status
> sudo ufw status numbered - Mostra as regras e sua numeração

## Adicionar regra para abrir a porta 8080:

> sudo ufw allow 8080

## Deletar última regra criada:

> sudo ufw delete allow 8080
ou
> sudo ufw delete <numerodaregra> 

## O que é SSH:

> Protocolo de segurança que permite a troca de dados entre servidor e cliente usando uma conexão simples e segura. Ele impede que os dados trocados entre as partes sejam expostos ou corrompidos por terceiros. Utilizando um método de criptografia tornando possível o acesso a esses dados apenas pelo client e servidor autorizados.

## Verificar se a porta usada pela conexão ssh é a 4242:

> sudo systemctl status ssh
> nano /etc/ssh/sshd_config

## Explicar o script de monitoramento e mostra-lo:

> Utlizando alguns comandos do próprio sistema e fazendo o uso do awk para manipular as nossas saídas.
nano /root/monitoring.sh

## O que é cron:

> É um agendador de tarefas que permite programar tarefas para serem executadas em determinado período de tempo.

## Como setar o script para rodar de 10 em 10 minutos:

> crontab -e (Como usuário root, o cron cria um perfil diferente para cada usuário do sistema)
O * significa que não importa o campo em questão (dia, minuto, mes e etc). Como o primeiro campo corresponde ao minuto, colocar uma / seguida por 10, significa que sera a cada 10 minutos.



Utils.:
adduser <usuario> <grupo> - adicionar um usuário ao grupo

addgroup - adicionar um grupo novo

less /etc/passwd | cut -d ":" -f 1  - imprimir todos os usuários do sistema

systemctl status sshd - checar o status do ssh e qual porta ele está usando

users - mostra a lista de usuários logados no sistema

