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
  <a href="#File_manipulation">File manipulation commands</a> •
  <a href="#Vim">Vim</a> 
</p><br><br>

<h3 #Goal> • 📍 Goal: </h3>
<p>The goal of this project is to teach how to set up my first server. It's not only my first experience configuring a server, but also my first experience installing a Linux operating system.</p><br>
<p> ⚠️ Starting from now, I will also write the notes in Portuguese to make it more accessible, considering that most of the material on the internet is in English. </p><br><br>
<h3 #Vitualization> • 🖥️ Virtualization: </h2>
<p>
  <strong>PT:</strong> Virtualização <strong>é a tecnologia que você pode usar para criar representações virtuais de 
servidores, armazenamento, redes e outras máquinas físicas</strong>.
  <strong>EN:</strong> Virtualization <strong>is the technology you can use to create virtual representations of servers, storage, networks, and other physical machines</strong>.<br><br>
</p>

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

1. **Separate (/home, /var, and /tmp) partitions:**
    - **/home:** O diretório **`/home`** contém os diretórios pessoais dos usuários. Ao separar isso em uma partição dedicada, os dados do usuário podem ser preservados, mesmo se você precisar reinstalar o sistema operacional. Isso facilita a atualização ou reinstalação sem perder dados pessoais.
    - **/var:** O diretório **`/var`** armazena dados variáveis, como logs, caches e arquivos temporários. Manter isso em uma partição separada pode ajudar a evitar problemas de espaço em disco se ocorrerem muitas gravações frequentes de logs ou outros dados variáveis.
    - **/tmp:** O diretório **`/tmp`** é usado para armazenar arquivos temporários. Ter uma partição separada para **`/tmp`** pode fornecer benefícios de segurança e desempenho, pois os arquivos temporários podem ser configurados para ter permissões restritas e podem estar em uma partição montada com opções específicas.
    
    Ao escolher essa opção, você tem mais controle sobre o espaço alocado para cada um desses diretórios e pode configurar as opções de montagem de cada partição de acordo com suas necessidades específicas.
    
    Essa abordagem também pode facilitar a manutenção e a recuperação de dados em determinadas situações, uma vez que problemas em um diretório específico (por exemplo, falta de espaço em **`/var`** ou **`/tmp`**) não afetarão diretamente outros diretórios do sistema.
    
    No entanto, essa escolha adiciona uma camada de complexidade ao gerenciamento do sistema de arquivos, então é importante entender as necessidades do seu sistema ao fazer essa escolha.
   
  <strong> A criptografia de disco é uma camada de segurança adicional que protege os dados no disco contra acesso não autorizado. </strong><br>
⚠️ Comando utilizado para que possamos verificar o particionamento do disco: **`lsblk`**

<h3 #AppArmor_UFW_SSHP> • 🛡️ AppArmor, UFW, SSH: </h3>

**O que é AppArmor?**

AppArmor é um sistema de controle de acesso obrigatório (MAC, Mandatory Access Control), similar ao SELinux.
Possiveis motivos para optar pelo AppArmor ao invés do SELinux?
**AppArmor foi projetado para ser mais simples de usar e configurar em comparação com alguns outros sistemas MAC, como SELinux.**   
    - O AppArmor é muitas vezes considerado mais fácil de configurar e usar em comparação com o SELinux. Ele utiliza perfis de aplicativos que são mais simples de compreender e implementar.
    - AppArmor adota um modelo de perfil mais simplificado em comparação com o SELinux. Os perfis do AppArmor são geralmente mais fáceis de criar e entender, o que pode ser uma vantagem para administradores menos familiarizados com controles de acesso obrigatório.
    - É uma integração padrão em algumas distribuições, como: Ubuntu.

**E como o AppArmor funciona?**

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
