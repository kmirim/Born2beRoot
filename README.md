<h1 align="center" #Título-e-Imagem-de-capa> Born2beRoot </h1>
<p align="center">
  <img loading="lazy" src="https://img.shields.io/static/v1?label=Status&message=concluded&color=7159c1&style=for-the-badge&logo=ghost"/>
</p>
<img alt="banner born2beroot" src="https://github.com/kmirim/Born2beRoot/assets/132582320/966d68c4-6002-43d1-830e-8d940d9e09df" />
<br><br><p align="center" #descrição-do-projeto>Project to build and solidify knowledge about the Unix system and concepts such as Apparmor, SSH, UFW, etc.</p>
<br>

<h2 align="center" #index> Index </h2>

<p align="center"> • 
  <a href="#Goal">Goal</a> •
  <a href="#Virtualization">Virtualization</a> • 
  <a href="#LVM">LVM</a> •
  <a href="#AppArmor_UFW_SSH">AppArmor, UFW, SSH</a> • 
  <a href="#Apt_and_aptitude">Apt and aptitude</a> • 
  <a href="#Shell_Script">Shell Script</a> • 
  <a href="#Signature">Signature</a> • 
  <a href="#File_manipulation">File manipulation commands</a><br>•
  <a href="#System_information_gathering_commands">System Information Gathering Commands</a>
</p><br><br>

<h3 #Goal> • 📍 Goal: </h3>
<p>The goal of this project is to teach how to set up my first server. It's not only my first experience configuring a server, but also my first experience installing a Linux operating system.</p><br>
<p> ⚠️ Starting from now, I will also write the notes in Portuguese to make it more accessible, considering that most of the material on the internet is in English. </p><br><br>
<h3 #Vitualization> • 🖥️ Virtualization: </h2>
<p>
  <strong>PT:</strong> Virtualização <strong>é a tecnologia que você pode usar para criar representações virtuais de 
servidores, armazenamento, redes e outras máquinas físicas</strong>.

<h3 #LVM> • 💽 LVM: </h3>

Logical Volume Manager ou gerenciador de volume lógico <br>

Durante o processo de instalação do Debian (e de muitas outras distribuições Linux), é possivel escolher o uso do LVM para gerenciar o armazenamento do sistema. É uma abordagem alternativa ao particionamento tradicional de discos em sistemas Linux. Em vez de criar partições fixas diretamente no disco, o LVM introduz uma camada lógica adicional que oferece mais flexibilidade no gerenciamento do espaço de armazenamento.

Como isso funciona?

LVM é uma tecnologia que oferece uma camada de abstração sobre os discos físicos em um sistema Linux. Ele permite uma gestão mais flexível e dinâmica do espaço de armazenamento.
1. Volume Group (Grupo de Volumes): No LVM, você agrupa discos físicos em um Volume Group. Este grupo é tratado como uma entidade única para a alocação de espaço.
2. Logical Volume (Volume Lógico): Dentro do Volume Group, você cria Logical Volumes. Esses volumes são análogos às partições em um sistema de arquivos tradicional, mas são mais flexíveis. Eles podem ser redimensionados facilmente, o que é uma vantagem sobre as partições convencionais.
3. Physical Extents (Extensões Físicas): O espaço em disco dentro de um Volume Group é dividido em blocos chamados Physical Extents. Esses blocos são a unidade mínima de alocação.
4. File System: Um sistema de arquivos é então criado em cima do Logical Volume, da mesma forma que você faria com uma partição convencional.

<br><img alt="img da estrutura do lvm" src="https://github.com/kmirim/Born2beRoot/assets/132582320/f808301d-0715-4071-b3c8-5f6f3433ad85"><br><br>

<strong>Guided - use entire disk and set up encrypted LVM: </strong> Esta opção indica que o instalador configurará o LVM para gerenciar o armazenamento e, ao mesmo tempo, criptografará o conteúdo do disco. A criptografia de disco é uma camada de segurança adicional que protege os dados no disco contra acesso não autorizado.

Selecionar a opção `"Separate /home, /var, and /tmp partitions"` durante a instalação de um sistema operacional Linux, como no Debian, refere-se à escolha de configurar partições separadas para diretórios específicos do sistema, em vez de colocar todos os diretórios no mesmo sistema de arquivos. Essa escolha oferece benefícios em termos de organização, desempenho e, em alguns casos, recuperação de dados.

 - **Separate (/home, /var, and /tmp) partitions:**
    - **/home:** O diretório **`/home`** contém os diretórios pessoais dos usuários. Ao separar isso em uma partição dedicada, os dados do usuário podem ser preservados, mesmo se você precisar reinstalar o sistema operacional. Isso facilita a atualização ou reinstalação sem perder dados pessoais.
    - **/var:** O diretório **`/var`** armazena dados variáveis, como logs, caches e arquivos temporários. Manter isso em uma partição separada pode ajudar a evitar problemas de espaço em disco se ocorrerem muitas gravações frequentes de logs ou outros dados variáveis.
    - **/tmp:** O diretório **`/tmp`** é usado para armazenar arquivos temporários. Ter uma partição separada para **`/tmp`** pode fornecer benefícios de segurança e desempenho, pois os arquivos temporários podem ser configurados para ter permissões restritas e podem estar em uma partição montada com opções específicas.
    
    Ao escolher essa opção, você tem mais controle sobre o espaço alocado para cada um desses diretórios e pode configurar as opções de montagem de cada partição de acordo com suas necessidades específicas.
    
    Essa abordagem também pode facilitar a manutenção e a recuperação de dados em determinadas situações, uma vez que problemas em um diretório específico (por exemplo, falta de espaço em **`/var`** ou **`/tmp`**) não afetarão diretamente outros diretórios do sistema.
    
    No entanto, essa escolha adiciona uma camada de complexidade ao gerenciamento do sistema de arquivos, então é importante entender as necessidades do seu sistema ao fazer essa escolha.
   
  <strong> A criptografia de disco é uma camada de segurança adicional que protege os dados no disco contra acesso não autorizado. </strong><br>
⚠️ Comando utilizado para que possamos verificar o particionamento do disco: **`lsblk`**
<br><br>
<h3 #AppArmor_UFW_SSHP> • 🛡️ AppArmor, UFW, SSH: </h3>

**1. O que é AppArmor?**

AppArmor é um sistema de controle de acesso obrigatório (MAC, Mandatory Access Control), similar ao SELinux.
Possiveis motivos para optar pelo AppArmor ao invés do SELinux?
**AppArmor foi projetado para ser mais simples de usar e configurar em comparação com alguns outros sistemas MAC, como SELinux.**   
    - O AppArmor é muitas vezes considerado mais fácil de configurar e usar em comparação com o SELinux. Ele utiliza perfis de aplicativos que são mais simples de compreender e implementar.
    - AppArmor adota um modelo de perfil mais simplificado em comparação com o SELinux. Os perfis do AppArmor são geralmente mais fáceis de criar e entender, o que pode ser uma vantagem para administradores menos familiarizados com controles de acesso obrigatório.
    - É uma integração padrão em algumas distribuições, como: Ubuntu.

**Como o AppArmor funciona?**

  - Segurança Baseada em Perfil:
        O AppArmor funciona com base em perfis. Cada aplicativo ou processo em execução no sistema tem um perfil associado que define os recursos e permissões que ele pode acessar.
        Os perfis são tipicamente definidos em arquivos de texto legíveis por humanos e especificam regras que restringem as ações de um programa. Essas regras definem quais arquivos, diretórios e capacidades o programa tem permissão para acessar.

 - Aplicação Baseada em Caminho:
        O AppArmor usa principalmente a aplicação baseada em caminho. Isso significa que ele se concentra em controlar o acesso a arquivos e diretórios específicos em vez de chamadas de sistema gerais.
        Quando um programa tenta acessar um arquivo, o AppArmor verifica se o acesso é permitido de acordo com as regras definidas no perfil associado a esse programa.

 - Integração com Serviços do Sistema:
        O AppArmor se integra a serviços e aplicativos do sistema. Por exemplo, no caso do Debian, é frequentemente usado para confinar serviços como servidores web, bancos de dados ou outros processos críticos.
        Os perfis são carregados no kernel durante a inicialização do sistema e são aplicados assim que os processos associados são iniciados.

  - Aplicação em Tempo de Execução:
        O AppArmor fornece aplicação em tempo de execução, o que significa que as políticas de segurança são aplicadas enquanto o sistema está em execução. Isso ajuda a evitar o acesso não autorizado a recursos sensíveis durante a operação do sistema.

  - Flexibilidade e Configurabilidade:
        O AppArmor permite controle granular sobre o comportamento do aplicativo. Você pode especificar quais arquivos ou diretórios um aplicativo pode ler, gravar ou executar. Essa granularidade ajuda a adaptar as políticas de segurança a casos de uso específicos.
        Os perfis podem ser personalizados para atender aos requisitos de segurança de aplicativos individuais.

  - Auditoria e Logs:
        O AppArmor fornece recursos de auditoria que registram eventos relacionados à segurança. Isso pode ser útil para monitorar e analisar o comportamento de aplicativos confinados.
        Os logs ajudam os administradores a identificar e solucionar problemas de segurança, fornecendo informações sobre quais recursos um aplicativo tentou acessar e se esses acessos foram permitidos ou negados.

  - Facilidade de Uso:
        O AppArmor é projetado para ser fácil de usar. Ele fornece uma camada adicional de segurança sem exigir uma configuração manual extensiva. O uso de perfis simplifica o processo de proteção de aplicativos.

Ao confinar aplicativos a perfis de segurança bem definidos, o AppArmor aprimora a segurança geral do sistema, minimizando o impacto potencial de vulnerabilidades de segurança em aplicativos individuais. É uma ferramenta eficaz para melhorar a postura de segurança de sistemas Linux.

⚠️ Comando utilizado para que possamos verificar se o serviço esta ativo: **`systemctl status apparmor`**

<h6> AppArmor tem relação com hostname, user e groups? </h6>

AppArmor (Application Armor) é um sistema de controle de acesso obrigatório (MAC - Mandatory Access Control) para sistemas Linux. Ao contrário do controle de acesso discricionário (DAC - Discretionary Access Control), onde os usuários têm controle sobre seus próprios objetos e arquivos, o MAC é um modelo de segurança mais restritivo e centralizado.

No contexto do Linux, que tradicionalmente utiliza o DAC, AppArmor adiciona uma camada adicional de controle de acesso baseada em perfis de aplicativos. 

Usuários e grupos são usados no GNU/Linux para [controle de acesso](https://en.wikipedia.org/wiki/pt:Controle_de_acesso#Na_seguran.C3.A7a_da_informa.C3.A7.C3.A3o) — isto é, para controlar o acesso aos arquivos, diretórios e periféricos do sistema.

**Em resumo, AppArmor não está diretamente vinculado aos conceitos tradicionais de usuários e grupos no Linux, como acontece com o controle de acesso discricionário.**

  - DAC é mais tradicional e baseado em permissões associadas aos usuários e grupos. Ele permite que os usuários determinem quem pode acessar seus próprios arquivos e recursos.

- `root` é o `superusuário`
- Usuários não privilegiados podem utilizar o `su` ou `sudo` para escalar privilégios controlados.

E o que é `hostname`: É o nome único atribuído a um computador ou sistema na rede. No caso, o hostname é **meuuser42**

E `username`: é o nome associado a uma conta de usuário, e o username pode ser qualquer um, escolhi **meuuser.**

- **Comando para adicionar novo usuário:** `adduser -m -s /bin/bash *nomedousuário*`
- Como verificar quais usuários existem: **`whoami`**
- Como **remover** um usuário: `userdel *nomedousuario*`
    - `sudo userdel -r *nomedousuario` para que seja apagado o diretório home e o conteúdo associado.*
- Comando para definir uma senha para o *novousuário `passwd nomedousuario`*

**2. O que é UFW?**

- Uncomplicated Firewall: é uma ferramenta de firewall para sistemas operacionais baseados em Linux. Ele foi projetado para simplificar o processo de configuração e gerenciamento de firewalls, tornando-o mais acessível para usuários iniciantes.
- Por baixo dos panos, o UFW utiliza o iptables, que é uma infraestrutura mais complexa e poderosa para configurar firewalls no Linux. O UFW, portanto, age como uma camada mais amigável e simplificada sobre o iptables.
    - O iptables é uma ferramenta de linha de comando usada para configurar as regras do firewall no sistema operacional Linux. Ele é parte integrante do conjunto de ferramentas do Netfilter, que é a estrutura de filtragem de pacotes no kernel do Linux. O iptables permite que os administradores de sistema configurem regras que determinam como o tráfego de rede deve ser tratado, como permitir ou bloquear determinadas conexões.

- Para verificar que esta **ativo**: `sudo ufw status`
- Para verificar a **numeração da porta**: `sudo ufw status numbered`
- Para **abrir** uma porta: `sudo ufw allow *numero-da-porta*`
- Para **deletar** uma porta: `sudo ufw delete *numero-da-porta*`

**3. O que é SSH?**

O Secure Shell (SSH) é um protocolo de rede criptografado usado para comunicação segura entre um cliente e um servidor. Ele fornece uma maneira segura de acessar serviços de rede sobre uma rede não segura, como a Internet. O SSH oferece autenticação forte, comunicação criptografada e integridade de dados para garantir a segurança das informações transmitidas entre os sistemas.

Ex de utilização: 

- **Encaminhamento de Porta:**
    - SSH pode ser usado para criar túneis seguros, encaminhando tráfego de uma porta local para uma porta remota. Isso é útil para acessar serviços em máquinas remotas de forma segura.
    - **Um serviço SSH estará em execução apenas na porta 4242. Por razões de segurança, não deve ser possível conectar-se usando SSH como root.**
        - Restringir o acesso SSH a contas não privilegiadas adiciona uma camada extra de segurança contra esses ataques.
        - Quando os usuários se conectam inicialmente com uma conta não privilegiada, é mais fácil rastrear e registrar as atividades associadas a essa conta. Conectar-se como root diretamente pode complicar o rastreamento, especialmente em ambientes com vários administradores.
        - **Acesso Granular:** A autenticação em duas etapas, como primeiro fazer login como usuário não privilegiado e, em seguida, usar `sudo`
         para realizar tarefas administrativas, permite um controle mais 
        granular sobre quem pode realizar ações administrativas. Isso é útil em 
        ambientes compartilhados ou com várias pessoas gerenciando o sistema.

 - Como acessar a VM pelo SSH: `ssh nome-do-user@ip-da-maquina -p numero-da-porta`
 - Para acessar o ip da máquina podemos utilizar: `hostname -I (i maiúsculo)`
 - Verificar o status do serviço SSH: `sudo systemctl status ssh`
 - Para configurar a chave ssh é necessario editar o arquivo ssh que fica localizado: `etc/ssh/sshd_confi`

<h4> Configuração de senha: </h4>

- Instalar a biblioteca `libpam-pwquality` para configurar senha: `sudo apt-get install libpam-pwquality`
- Como **alterar a politica de senha:** `sudo nano /etc/pam.d/common-password`
- Outra forma: `etc/security/pwquality.conf`
- Alteração: `password  requisite     pam_pwquality.so  retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root`
    1. **`password`:**
        - Este é o tipo de controle PAM que está sendo configurado, especificamente para tratamento de senhas.
    2. **`requisite`:**
        - Indica que esta etapa é crucial para a autenticação ter sucesso. Se a verificação da senha falhar nesta etapa, a autenticação falhará.
    3. **`pam_pwquality.so`:**
        - Especifica o uso do módulo `pam_pwquality.so`, que fornece funcionalidades para impor políticas de qualidade de senha.
    4. **`retry=3`:**
        - Permite até 3 tentativas de entrada de senha antes de retornar uma falha na autenticação. Se o usuário errar a senha três vezes, o processo de autenticação falhará.
    5. **`minlen=10`:**
        - Define um comprimento mínimo de senha de 10 caracteres. Ou seja, as senhas precisam ter pelo menos 10 caracteres de comprimento para atender a essa política.
    6. **`ucredit=-1 lcredit=-1 dcredit=-1`:**
        - Estabelece políticas de complexidade de senha:
            - `ucredit`: Pelo menos uma letra maiúscula (`1` significa que é permitido pelo menos uma).
            - `lcredit`: Pelo menos uma letra minúscula.
            - `dcredit`: Pelo menos um dígito.
    7. **`maxrepeat=3`:**
        - Restringe a repetição de caracteres consecutivos na senha a 3. Isso ajuda a evitar sequências óbvias, como "12345" ou "abcdef".
    8. **`reject_username`:**
        - Não permite que o nome do usuário seja parte da senha. Isso é uma medida de segurança para evitar senhas previsíveis.
    9. **`difok=7`:**
        - Define o número mínimo de caracteres diferentes entre a nova senha e a senha antiga (caso o usuário esteja alterando a senha). Neste caso, são necessários pelo menos 7 caracteres diferentes.
    10. **`enforce_for_root`:**
        - Aplica essas políticas mesmo para o usuário root. Isso é útil para garantir que até mesmo o superusuário esteja sujeito a políticas de senha rigorosas.

<h3 #Apt_and_aptitude> • 📥 Apt and aptitude </h3>

  - Aptitude é um gerenciador de pacotes de nível superior, enquanto APT é um gerenciador de pacotes de nível inferior que pode ser usado por outros gerenciadores de pacotes de nível superior.
  - O Aptitude é mais vasto em funcionalidades do que o apt-get e integra funcionalidades do apt-get e suas outras variantes, incluindo apt-mark e apt-cache.
    - Em sistemas operacionais Debian é utilizado o comando `apt-get` para gerenciar pacotes de software.
**O Apt-get** ser um gerenciador de pacotes de nível inferior é restrito apenas à linha de 
comando, enquanto o Aptitude ser uma ferramenta de nível superior tem uma interface interativa padrão apenas em texto, juntamente com a opção de operação de linha de comando, inserindo os comandos necessários.

<h3 #Shell_Script> • 🐧 Shell Script</h3>

  - Script de shell é um programa que consiste em uma sequência de comandos que podem ser executados diretamente no prompt de comando. Esses scripts são usados para automatizar tarefas, realizar operações específicas no sistema operacional, ou agrupar uma série de comandos em um único arquivo para facilitar a execução.
    - Nesse projeto é utilizado para implementar o monitoring.sh, o script solicitado na parte mandatória.
    - O diretório `/usr/local/bin` é uma localização comum para armazenar executáveis (programas ou scripts executáveis) em sistemas Unix/Linux. Ao criar um arquivo nesse caminho, você está colocando um executável em um local acessível globalmente no sistema.
   
<h3 #Signature> • ✒️ Signature</h3>

  - É preciso entregar um arquivo signature.txt na raiz do meu repositório.
    - A assinatura é feita através de um **hash** que é utilizado para garantir a autenticidade do arquivo. Esse código é gerado a partir do comando `**sha1sum**` + seleção do arquivo `maquina-virtual.dvi`
  - O código gerado é o que deve estar no arquivo .txt.

<h3 #File_manipulation> • 📄 File manipulation commands</h3>

- `Touch` : cria arquivos ASCII
- `touch -t` : define *timestamp* = uma marca temporal, um conjunto de caracteres que identifica data e hora de algo ou evento.
- `cp` : copiar arquivos
- `cp -r` : copiar diretórios
    - `cp -a` : copia e altera o nome (sintaxe: `cp -a`****nome-do-arquivo nome-novo****)
- `find` : para procurar (sintaxe: *`find local nome-do-arquivo`*)
- `du-hs`  : espaço do disco utilizado
- O redirecionador ">" sobrescreve o conteúdo (caso exista), enquanto o ">>" adiciona ao final do arquivo.
- O parâmetro "-v" indica que o oposto será exibido.
- A flag `-r`  é de: recursivo
- A flag `-v` é para que seja feito o inverso
- `-i` para desconsiderar a diferença entre letras maiúsculas e minúsculas
O metacaracter é um caractere que tem um significado especial ou uma função além de seu valor literal. `^` significa **início de linha**.
- Visualizar apenas **diretórios**
    
    ```nasm
    ls -l /etc/ | grep ^d
    ```
    
- Se eu desejo verificar tudo que não é diretório
  
    ```nasm
    ls -l /etc/ | grep ^d -v
    ```
    
    Filtros de conteúdo: 
    
    Contador de palavras: wc e outro é nl (contabiliza por espaço)
    
    Recortar:
    
    ```jsx
    	cut
    ```
    
    Precisa necessariamente de alguns parâmetros: 
    
    -d = delimitador
    
    -f = campo 
    
    Trocar:
    
    ```jsx
    tr 
    ```
    
    Primeiro qual o char, segundo pelo que substituir
    
    Se incluir a flag `d` deleta o caracter indicado
    
    Para ordenar:
    
    ```jsx
    sort
    ```
    
    Para aparecer somente um:
    
    ```jsx
    unic
    ```
    
    Sintaxe do awk:
    
    ```jsx
    awk '/exemplo/ { print }' arquivo.txt
    ```
    
    Para comparar:
    
    ```jsx
    diff primeiro-arquivo segundo-arquivo
    ```
    
    <aside>
    Compactadores:
    
    </aside>
    
    ```jsx
    zip <flags> [caminho-do-arquivo][arquivo-a-ser-compactado]
    ```
    
    Para desempacotar
  ```jsx
  unzip <flags> [caminho-do-arquivo][arquivo-a-ser-descompactado]
  ```

**Visualizadores de texto:**

- cat = Exibe na saída padrão (tela) o conteúdo de um arquivo.
- more = Exibe na saída padrão (tela) o conteúdo de um arquivo, exibindo uma tela
de cada vez (ideal para arquivos extensos).
- less = Exibe na saída padrão (tela) o conteúdo de um arquivo, permitindo a
paginação através de comandos.
- head = Exibe na saída padrão (tela) as dez primeiras linhas de um arquivo (por
padrão, porém, a quantidade pode ser especificada).
- tail = Exibe na saída padrão (tela) as dez últimas linhas de um arquivo (por padrão,
porém, a quantidade pode ser especificada).
    - Muito utilizado para a visualização de logs.
 
**Conectores de comando:**

- Concatenação de comandos nada mais é do que “pegar” a saída de um comando e
utilizá-la como “entrada” para o comando seguinte.
- Para realizar a concatenação, devemos utilizar dutos (duto = PIPE = | )
- Podemos solicitar a execução de diversos comandos em sequência no Linux.
- Esta execução em sequência é diferente do processo de concatenação.
- A execução de comandos em sequência não utiliza a saída do comando anterior
como dados de entrada no comando seguinte.
- Conectores e operadores são geralmente utilizados em scripts.
**Para executar comandos em sequência, temos os seguintes conectores:**
 - Ponto e vírgula “;” para execução de comandos em sequência:
- Ex.: clear ; cd /etc ; cp -a services /root
- Operador “&&” (AND), **somente executará o comando seguinte, se o anterior for executado, ou seja** caso o primeiro comando execute com sucesso (código de retorno = 0), o segundo comando também será executado:
- Ex.: cd /Teste && rm -rf *
- Operador “||” (OR), caso o primeiro comando não execute com sucesso (código de retorno ≠ 0), o segundo comando será executado. RESUMINDO, quando um dos comandos for executado com sucesso, os comandos seguintes não são verificados:
- Ex.: `cd /home/Teste || mkdir /home/Teste`
- Para criar uma pasta com subdiretórios: mkdir nome-da-pasta/{nome-da-subpasta{nome-da-outra-subpasta},nome-da-subpasta}
- Comando `dmesg` (display message - from kernel ring buffer):  exibe as mensagens do buffer do Kernel, contendo módulos (drivers) e dispositivos de hardware carregados após a inicialização. 

<h3 #System_information_gathering_commands> • 🛠️ System Information Gathering Commands </h3>

`uname`: Exibe informações sobre o sistema instalado, incluindo a versão do
Kernel
• Ex.: `uname -a`
• O parâmetro “-a” (all) exibe todas as informações disponíveis

`uptime`: Exibe um resumo de informações sobre o sistema como:
• Hora atual;
• Tempo que o sistema está em execução (“up”, “no ar”);
• Quantidade de usuários logados;
• “Load Average”, que mostra quantos processos em média estão aguardando (na fila) para serem
executados, sendo que as separações por “vírgula” representam os intervalos de tempo de 1, 5
e 15 minutos.

`free` : Exibe informações sobre a utilização da memória RAM e SWAP.
• Ex.: free -m
• O parâmetro “-m” exibe a utilização em MB, da mesma forma que “-g” ou “-k” podem ser utilizados para exibição em GB e KB respectivamente.

- Podemos executar o “free -s 10”, para atualizar o status do consumo de memória a cada 10
segundos.

`df` : Exibe informações sobre o espaço livre/utilizado em disco:
• Ex.: df -h
• O parâmetro “-h” exibe de forma “inteligível” (humam readable).
`du` : Exibe o tamanho ocupado em disco de arquivos ou diretórios:
• Ex.: du -hs /etc
• O parâmetro “-s” exibe o tamanho total ocupado pelo diretório “/etc”;
• O parâmetro “-h” exibe de forma “inteligível” (humam readable).

`file`: Exibe o tipo de um determinado arquivo (se o mesmo é texto, imagem,
arquivo compactado, entre outros).
• Ex.: file <nome_do_arquivo>

`w` : Exibe a saída do comando “uptime” e informações sobre os usuários
conectados, como tempo ocioso e processo que este usuário está executando.

`who` : Exibe quais usuários estão logados no sistema, qual o “terminal” este
usuário está conectado, data e hora do Logon, e por fim, o IP de origem desta
conexão (caso seja uma conexão remota).

`whoami` : Exibe qual o nome do usuário logado no terminal atual

`ifconfig` : Permite verificar o IP atual ou configurar um IP para um determinado
adaptador de rede:
• Ex.: ifconfig <interface>

- route : Permite visualizar ou modificar rotas ou o “Default Gateway”:
• Ex.: route add default gw [X.X.X.X]
- Ex.: route -n
• Apenas exibe as rotas existentes;
- O comando “ip” possui diversas opções (chamadas de objetos), que permite ver e
alterar configurações de rede, roteamento e tunelamento.
- A principal utilidade do comando é definir um endereço IP. Segue exemplo:
• Listando as interfaces. Ex.: ip address ou ip addr list ou ip addr

- A remoção de um endereço IP possui sintaxe similar, tendo duas possibilidades:
• Remover todos os endereços de uma interface (caso tenha mais de um IP):
• Ex.: ip address flush dev enp0s3
• Remover apenas um endereço da interface “enp0s3”:
• Ex.: ip address del x.x.x.x/mask dev <interface>

`dmesg` : exibe todo o Hardware reconhecido/carregado pelo kernel durante a
inicialização.

`lspci` : exibe informações do chipset e dispositivos PCI:

`lsusb` : exibe informações sobre dispositivos USB conectado

  - Instalar/desinstalar dispositivos que o sistema não reconheça automaticamente, devemos realizar o download do módulo (driver) do dispositivo a ser instalado e utilizar os comandos abaixo:
    - exibe os módulos (drivers) carregados no sistema: `lsmod`
  - Instala/carrega um novo módulo no Kernel: `insmod`
      - Ex.: `insmod [arquivo] <opções>`
  - Remove um módulo: `rmmo` (devemos ter cautela na realização do mesmo, tendo em vista que ao remover um módulo, “desativamos” o hardware associado ao módulo)
      - Ex.: `rmmod <nome_do_modulo>`
  - listar todos os dispositivos de armazenamento conectados em nosso computador:
      - Ex.: fdisk -l
  
  - O diretório `/proc` é um diretório virtual do sistema Linux com algumas características importantes:
    - É um diretório utilizado exclusivamente pelo kernel para gerenciamento do sistema e seus recursos;
    - Existe apenas enquanto o computador está ligado;
    - Possui diversos arquivos com o tamanho de 0 bytes, porém, podemos encontrar conteúdos nestes arquivos;
    - O maior arquivo deste diretório se chama “kcore”, que possui tamanho próximo ao disponível na memória RAM;
    - Não podemos gravar ou criar arquivos neste diretório.


