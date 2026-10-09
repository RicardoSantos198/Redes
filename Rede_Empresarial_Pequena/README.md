🚀 <h1>Projeto de Infraestrutura de Rede — Inter-VLAN e DHCP</h1>

<p align="center"> <img src="https://img.shields.io/badge/Cisco-Packet%20Tracer-005691?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer"> <img src="https://img.shields.io/badge/Networking-VLANs%20%7C%20DHCP-orange?style=for-the-badge" alt="VLANs e DHCP"> <img src="https://img.shields.io/badge/Routing-Router--on--a--Stick-blue?style=for-the-badge" alt="Router-on-a-Stick"> <img src="https://img.shields.io/badge/Status-Concluído-brightgreen?style=for-the-badge" alt="Projeto concluído"> </p>

<p align="center"> <strong>🌐 Segmentação de rede corporativa, atribuição dinâmica de IP e comunicação entre VLANs.</strong> </p>

📌 <h2>Sobre o Projeto</h2>

Este projeto consiste na implementação de uma infraestrutura de rede corporativa utilizando o Cisco Packet Tracer, com o objetivo de aplicar, na prática, conceitos fundamentais de redes de computadores.

A infraestrutura foi projetada para segmentar dois departamentos — Administrativo e Financeiro — por meio de VLANs, permitindo a organização lógica da rede, a redução dos domínios de broadcast e a comunicação entre diferentes segmentos através do conceito de Router-on-a-Stick.

Além disso, foi configurado um serviço DHCP diretamente no roteador Cisco IOS para automatizar a distribuição de endereços IP aos computadores da rede.

💡 O projeto foi desenvolvido como parte da consolidação dos conhecimentos adquiridos nos cursos de redes da Alura, reforçando conceitos de switching, roteamento, endereçamento IPv4 e serviços de rede.

🎯 <h2>Objetivos</h2>
Implementar VLANs para segmentar os departamentos da empresa.
Configurar portas de acesso e links trunk com encapsulamento IEEE 802.1Q.
Implementar o roteamento entre VLANs utilizando Router-on-a-Stick.
Configurar pools DHCP para atribuição automática de endereços IP.
Definir gateways padrão e servidores DNS para as estações.
Validar a conectividade entre os computadores por meio de testes de comunicação.

🗺️ <h2>Topologia da Rede</h2>

A topologia é composta por 1 roteador principal, 1 switch Core, 2 switches de acesso e 6 computadores, distribuídos entre os departamentos Administrativo e Financeiro.

                   ┌───────────────────────┐
                   │  ROTEADOR PRINCIPAL   │
                   │   Router-on-a-Stick   │
                   └───────────┬───────────┘
                               │
                         802.1Q TRUNK
                               │
                   ┌───────────┴───────────┐
                   │       SW-CORE         │
                   └───────────┬───────────┘
                               │
                   ┌───────────┴───────────┐
                   │                       │
             802.1Q TRUNK            802.1Q TRUNK
                   │                       │
          ┌────────┴────────┐      ┌────────┴────────┐
          │     SW-ADM      │      │     SW-FIN      │
          └───┬────┬────┬───┘      └───┬────┬────┬───┘
              │    │    │              │    │    │
             PC1  PC2  PC3             PC4  PC5  PC6

          VLAN 10 — ADM             VLAN 20 — FIN
          192.168.10.0/24            192.168.20.0/24

🔌 <h2>Componentes da Infraestrutura</h2>

<ul> <li>🌐 <strong>Roteador Cisco (1)</strong> — Responsável pelo roteamento entre VLANs e pelo serviço DHCP.</li> <li>🔀 <strong>Switch Core (1)</strong> — Responsável pela agregação e distribuição dos links trunk.</li> <li>🔗 <strong>Switches de acesso (2)</strong> — Responsáveis pela conexão dos computadores aos respectivos departamentos.</li> <li>💻 <strong>Computadores (6)</strong> — Estações de trabalho utilizadas nos testes de conectividade e comunicação entre VLANs.</li> </ul>

📊 <h2>Plano de Endereçamento IP</h2>

A rede foi dividida em duas sub-redes IPv4, cada uma associada a uma VLAN e a um gateway específico.

Departamento	VLAN	Nome	Sub-rede	Gateway
Administrativo	10	ADM	192.168.10.0/24	192.168.10.1
Financeiro	20	FIN	192.168.20.0/24	192.168.20.1
📡 Configuração DHCP
Parâmetro	VLAN 10 — ADM	VLAN 20 — FIN
Rede	192.168.10.0/24	192.168.20.0/24
Gateway padrão	192.168.10.1	192.168.20.1
Faixa dinâmica	192.168.10.10–254	192.168.20.10–254
Máscara	255.255.255.0	255.255.255.0
DNS	8.8.8.8	8.8.8.8
Nota: Os endereços de 192.168.X.1 a 192.168.X.9 foram reservados para gateways e possíveis equipamentos de infraestrutura, por meio do comando ip dhcp excluded-address.
🛠️ Tecnologias e Conceitos Aplicados
Tecnologia	Aplicação no projeto
VLAN — IEEE 802.1Q	Segmentação lógica da rede em domínios de broadcast independentes
Trunking	Transporte de tráfego de múltiplas VLANs entre switches e roteador
Router-on-a-Stick	Roteamento entre VLANs utilizando subinterfaces em uma única interface física
DHCP	Distribuição automática de endereços IP e parâmetros de rede
IPv4 / CIDR	Planejamento e organização do endereçamento das sub-redes
Cisco IOS CLI	Configuração e verificação dos dispositivos de rede
Cisco Packet Tracer	Simulação e validação da infraestrutura
⚙️ Principais Configurações

Os exemplos abaixo representam os principais comandos utilizados na configuração dos dispositivos.

1. Criando a VLAN 10 — Administrativo
enable
configure terminal

vlan 10
 name ADM
exit

2. Configurando as portas de acesso

Exemplo de configuração das portas destinadas aos computadores do departamento Administrativo:

interface range fastEthernet 0/2-4
 switchport mode access
 switchport access vlan 10
exit


No switch do departamento Financeiro, aplica-se a mesma lógica, utilizando a VLAN 20.

vlan 20
 name FIN
exit

interface range fastEthernet 0/2-4
 switchport mode access
 switchport access vlan 20
exit

3. Configurando uma porta trunk

Exemplo de configuração da conexão entre um switch de acesso e o switch Core:

interface fastEthernet 0/1
 switchport mode trunk
exit


As portas que interligam os switches e o roteador devem ser configuradas de acordo com a topologia, permitindo o transporte das VLANs necessárias.

4. Configurando o Router-on-a-Stick

Primeiro, habilite a interface física que conecta o roteador ao switch Core:

interface gigabitEthernet 0/0
 no shutdown
exit


Em seguida, configure a subinterface correspondente à VLAN 10:

interface gigabitEthernet 0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
exit


E a subinterface da VLAN 20:

interface gigabitEthernet 0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
exit


Cada subinterface funciona como gateway da respectiva VLAN, possibilitando o roteamento entre as duas redes.

5. Configurando os pools DHCP

Pool DHCP — Administrativo

ip dhcp excluded-address 192.168.10.1 192.168.10.9

ip dhcp pool POOL-ADM
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8
exit


Pool DHCP — Financeiro

ip dhcp excluded-address 192.168.20.1 192.168.20.9

ip dhcp pool POOL-FIN
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 dns-server 8.8.8.8
exit


Com essa configuração, os computadores podem obter automaticamente um endereço IP disponível, a máscara de sub-rede, o gateway padrão e o endereço do servidor DNS.

✅ Validação e Testes

Após a configuração dos dispositivos, foram realizados testes para verificar o funcionamento da infraestrutura.

Atribuição dinâmica de IP: os seis computadores receberam configurações de rede por meio do DHCP.
Verificação de trunking: o comando show interfaces trunk foi utilizado no switch Core para verificar os enlaces trunk.
Conectividade na mesma VLAN: testes de comunicação entre computadores do mesmo departamento.
Conectividade Inter-VLAN: testes de ping entre computadores das redes 192.168.10.0/24 e 192.168.20.0/24.
Gateway padrão: verificação da comunicação das estações com os gateways configurados nas subinterfaces do roteador.
🔍 Comandos de verificação

Verificar as VLANs:

show vlan brief


Verificar os enlaces trunk:

show interfaces trunk


Verificar as interfaces do roteador:

show ip interface brief


Verificar os endereços distribuídos pelo DHCP:

show ip dhcp binding


Verificar os pools DHCP:

show ip dhcp pool


Testar a conectividade entre departamentos:

ping 192.168.20.X

Substitua X pelo endereço IP real do computador de destino no departamento Financeiro. O teste inverso também pode ser realizado a partir de um computador da VLAN 20 para um endereço da VLAN 10.

Resultado: a validação do projeto indicou funcionamento do DHCP e comunicação entre as VLANs no ambiente simulado.

📚 Aprendizados

O desenvolvimento deste projeto permitiu consolidar conhecimentos importantes para a área de infraestrutura e redes de computadores, incluindo:

Segmentação de redes com VLANs.
Configuração de portas de acesso e enlaces trunk.
Roteamento entre redes utilizando subinterfaces.
Configuração de serviços DHCP em roteadores Cisco.
Planejamento de endereçamento IPv4.
Diagnóstico e validação de conectividade com comandos de rede.
Organização de uma topologia corporativa em ambiente de simulação.

Projeto desenvolvido para fins de aprendizado e prática em infraestrutura de redes, com foco em segmentação, roteamento e serviços de rede utilizando tecnologias Cisco.

🔗 GitHub: RicardoSantos198

<p align="center"> 💻 <strong>Aprendendo na prática, construindo conhecimento e evoluindo na área de redes!</strong> 🚀 </p>
