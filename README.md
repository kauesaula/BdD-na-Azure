##Como criar uma VM na Azure

1° Passo: Pesquisar "Azure Virtual Machine" e navegar. Tamém é possível acessar via "Create +"
2° Passo: Preenchimento de informações básicas (as mais relevantes):

Resource Group: Agrupamento lógico de todos os recursos pertencentes a uma solução de software ou de produtos. Em outras palavras, é o grupo onde os recursos da sua VM estarão guardados. Facilita o gerenciamento, o controle de acesso e o monitoramento de custos.
Region: Não necessariamente onde o usuário está localizado geograficamente, mas sim em que região ele quer hospedar a VM. Bom exemplo de design descentralizado da Nuvem. A latência, custos e conformidades com leis de soberania de dados variam dependendo da região.
Avaliability Options: Aqui é onde é defina a resiliência da VM contra falhas de hardware ou de data center.Availability Zones: locais físicos únicos, com infraestrutura própria, dentro de uma região da Azure.
Availability Sets: agrupam VMs dentro de um mesmo datacenter em diferentes domínios de falha (racks de servidores diferentes) e domínios de atualização (grupos de VMs que são reiniciadas juntas durante manutenções do host)
No infrastructure redundancy required: quando não há necessidade de alta disponibilidade, como em ambientes de teste ou desenvolvimento.
Security Type: Define o nível de segurança da VM.Standard: segurança padrão.
Trusted launch virtual machines: proteção através de Secure Boot e vTPM (módulo de plataforma virtual confiável).
Confidential virtual machines: criptografa a memória da VM enquanto ela está em uso.
Image: modelo/template usado para criar a VM. Contém o sistema operacional (como Windows ou Linux) e, em alguns casos, softwares pré-instalados.
Azure Spot Instance: permite que o usuário compre capacidade de computação não utilizada da Azure com um desconto significativo. A Azure pode desligar sua VM a qualquer momento se precisar da capacidade de volta.
Size: capacidade computacional da VM (e às vezes da Rede). É importante escolher um tamanho adequado às suas necessidades por conta da capacidade computacional que você está alugando com aquela opção. Naturalmente, quanto maior capacidade, maior o custo.
Inbound Ports: define as portas por onde a máquina virtual poderá ser acessada.RDP (3389): Para acesso à área de trabalho remota em VMs Windows.
SSH (22): Para acesso seguro via linha de comando em VMs Linux.
HTTP (80) / HTTPS (443): Para permitir tráfego web.
3° Passo: Preenchimento de informações de Disco:

OS disk type: armazena o sistema operacional. A escolha afeta diretamente a performance e o custo.Standard HDD: mais barato e ideal para cargas de trabalho menos sensíveis à latência.
Standard SSD: bom equilíbrio entre custo e performance. Adequado para servidores web de baixo tráfego, ambientes de desenvolvimento e teste.
Premium SSD: alto desempenho baseado em SSD, ideal para bancos de dados e cargas de trabalho de produção que exigem baixa latência e alto IOPS (operações de entrada/saída por segundo).
Ultra Disk: o desempenho mais alto, para cargas de trabalho extremamente exigentes.
Data disks: é altamente recomendado adicionar discos de dados para armazenar aplicações e dados de usuários, separando-os do disco do SO.
Encryption: por padrão, todos os Managed Disks da Azure são criptografados em repouso (SSE - Server-Side Encryption) com chaves gerenciadas pela Microsoft.
4° Passo: Preencher as informações de Network:

Virtual Network (VNet): rede privada e isolada do usuário na Azure. Permite que os recursos da Azure (não só as VMs) se comuniquem de forma segura entre si, com a internet e com suas redes locais (on-premises). Toda VM precisa estar dentro de uma VNet.
Subnet: intervalo de endereços IP dentro da VNet. Segmentar uma VNet em sub-redes permite organizar e proteger os recursos. Ex.: ter uma sub-rede para servidores web e outra para bancos de dados, com regras de segurança diferentes para cada uma.
Public IP: endereço IP que permite que sua VM seja acessada a partir da internet. Se você não atribuir um IP público, a VM só poderá ser acessada de dentro da mesma VNet ou de redes conectadas.
NIC network security group (NSG): firewall virtual da VM. Contém uma lista de regras de segurança que permitem o tráfego de rede para a interface de rede (NIC) da VM.
Inbound Ports: são regras para as portas definida na guia "Basics" (RDP, SSH, etc.). São criadas automaticamente dentro do NSG.
5° Passo: Opções de Gerenciamento e Comportamento da máquina, como monitoramento, identidade, auto-shutdown e backup.
6° Passo: Custom Data: É um campo que permite provisionar recursos ou instalar softwares dentro da máquina no momento do provisionamento. Ideal para automatizar os first-steps da VM.
7° Passo - Finalização: Adição de Tags, review e criação da VM.

Para que posso utilizar uma VM? Quando identifico a necessidade?
Para identificar a necessidade de uma VM, primeiramente deve-se identificar se seu PaaS ou SaaS é capaz de atender às suas necessidades envolvendo flexibilidade e controle das necessidades da aplicação. Quando você sente que precisa ter uma maneira mais eficiente de manter o controle total sobre seu ambiente computacional, incluindo sistema operacional e softwares instalados, e os serviços que você contratou te deixam na mão, é totalmente cabível construir uma VM para te atender melhor.
Casos comuns de uso de VM:

Migração de Aplicações ("Lift-and-Shift"): Quando você quer mover uma aplicação que roda em um servidor físico local para a nuvem com o mínimo de alterações. Você simplesmente cria uma VM com as mesmas especificações e sistema operacional e "levanta e desloca" a aplicação.
Hospedagem de Sites e Aplicações Web: Para hospedar um servidor web (como Apache ou IIS) ou uma aplicação que requer uma configuração específica do sistema operacional que não é oferecida por serviços de plataforma (PaaS) como o Azure App Service.
Servidores de Banco de Dados: Quando você precisa de controle total sobre a instância do banco de dados (por exemplo, SQL Server, MySQL, PostgreSQL), incluindo versões específicas, configurações de performance ou replicação que não estão disponíveis nos serviços de banco de dados gerenciados do Azure.
Ambientes de Desenvolvimento e Teste: Desenvolvedores frequentemente precisam de VMs para criar ambientes de teste isolados e personalizados, que podem ser criados e destruídos rapidamente conforme a necessidade.
Cargas de Trabalho de Alto Desempenho (HPC - High-Performance Computing): Para tarefas que exigem grande poder computacional, como simulações científicas, modelagem financeira ou renderização de vídeo. O Azure oferece séries de VMs otimizadas para HPC.
Execução de Software Legado: Para softwares que dependem de um sistema operacional mais antigo ou de configurações muito específicas que não são suportadas por plataformas mais modernas.
Dito isso, caso você não precise exatamente fazer o gerenciamento de sistema operacional, talvez alternativas como Azure App Service ou Azure SQL Database sejam mais acessiveis e eficientes.
