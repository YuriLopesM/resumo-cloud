## Resumo - Cloud Computing

### Data Center (Norma TIA-942)

#### 📌 Conceitos Básicos

- Local projetado para abrigar servidores, equipamentos de rede e infraestrutura de TI.
- TIA-942: norma que define os requisitos mínimos de infraestrutura para Data Centers. Define requisitos mínimos (energia, resfriamento, cabeamento, etc.)

#### 🧱 Estrutura e Topologia

- Áreas
  - EF (Entrance Room): conexão com operadoras externas.
  - MDA (Main Distribution Area): núcleo da rede; switches e roteadores centrais.
  - HDA (Horizontal Distribution Area): conexão entre o MDA e os equipamentos.
  - ZDA (Zone Distribution Area): ponto intermediário, sem equipamentos ativos.
  - EDA (Equipment Distribution Area): onde ficam os servidores.
  - CA (Caixa de Acesso): ponto entre rede externa e o data center.
- Topologia: cabeamento horizontal e backbone, com cross-connects.

#### 🧿 Classificação TIER

| TIER     | Descrição                 | Tempo de Indisponibilidade/ano      |
|----------|---------------------------|-------------------------------------|
| TIER I   | Sem redundância           | até 28.8h de indisponibilidade/ano. |
| TIER II  | Componentes redundantes   | até 22h/ano.                        |
| TIER III | Auto sustentável          | até 1.6h/ano.                       |
| TIER IV  | Tolerância total a falhas | até 0.4h/ano.                       |

#### 🔌 Requisitos Técnicos

##### ❄️Refrigeração

- Temperatura ideal: 18°C a 27°C.
- Umidade relativa: 40% a 55%.
- Utiliza-se o conceito de corredores quentes e frios para otimizar o fluxo de ar.
- Sistemas de HVAC devem ser redundantes e ativos 24/7.

##### 💡 Iluminação

- mínimo de 500 lux no plano horizontal e 200 lux no plano vertical.
- A iluminação não deve ser alimentada pelos mesmos circuitos dos equipamentos de TI.

##### 🔌 Energia e Segurança

- Uso de UPS, geradores e circuitos dedicados.
- Controle de acesso rigoroso, sensores, portas com autenticação.
- Prevenção contra incêndio seguindo a norma NFPA 75.

### On-Premise vs Cloud Servers

#### 📦 On-Premise

- Servidores físicos na empresa.
- Alto custo inicial (infraestrutura, manutenção, energia).
- TI local responsável por tudo (backup, energia, segurança).

#### ☁️ Cloud Servers

- Infraestrutura sob demanda via internet.
- Custos diluídos em mensalidades.
- Redução de tarefas para o time de TI.
- Modelos: SaaS, PaaS, IaaS.

#### ⚠️ Comparações Importantes

| Critério	     | On-Premise                | Cloud                        |
|----------------|---------------------------|------------------------------|
| Custo Inicial  | Alto	                     | Baixo                        |
| Manutenção	   | Interna	                 | Responsabilidade do provedor |
| Escalabilidade | Limitada                  | Flexível e sob demanda       |
| Backup	       | Manual, local	           | Incluso no serviço           |
| Energia	       | Engenharia elétrica local | Gestão pelo provedor         |
| RPO/RTO	       | Gerido pela TI            | Definido em SLA              |

- RPO (Recovery Point Objective): o quanto de dados você pode perder.
- RTO (Recovery Time Objective): quanto tempo você pode ficar fora do ar.

### Processos e Sistemas Operacionais

#### 🔄 Conceitos-Chave

- Monotarefa: 1 processo por vez.
- Multitarefa: múltiplos processos (com preempção).
- Processo: contêiner com recursos.
- Thread: linha de execução dentro de um processo.

#### 🤹 Concorrência vs Paralelismo

- Concorrência: tarefas se revezam no mesmo núcleo.
- Paralelismo: execução simultânea em vários núcleos.

#### 💡 Programação

- Síncrono: espera término da tarefa (ex: PHP).
- Assíncrono: alternância de execução (ex: Go).

#### 💾 Memória

- Primária (RAM, cache): volátil e rápida.
- Secundária (HD, SSD): não-volátil e permanente.
- Memória virtual (SWAP): usada quando a RAM se esgota.

### Sistemas de Arquivos Locais

#### 📁 Conceitos Gerais

- Abstraem dados em arquivos e diretórios.
- Devem: guardar grande volume, sobreviver ao processo e permitir acesso concorrente.

#### 🛠 Componentes

- Arquivo: sequência de bytes + atributos.
- Diretório: mapeia nomes para identificadores.
- i-nodes, MBR, Superbloco: estruturas internas.

#### 📂 Exemplos de Sistemas de Arquivo

| Nome	    | Característica Principal                                |
|-----------|---------------------------------------------------------|
| `ext4`	  | Grande capacidade, journaling, retrocompatível          |
| `NTFS`	  | Windows, nomes longos, recuperação fácil                |
| `FAT32`	  | Simples, compatível, limita tamanho                     |
| `NFS`	    | Acesso remoto como local (Unix/Linux)                   |
| `ZFS`	    | Integridade, escalabilidade, verificação automática     |
| `procfs`	| Acesso a processos via sistema de arquivos (Unix/Linux) |


#### 🧩 LVM e SWAPkc

- LVM: permite redimensionamento de partições sem reinicializar o sistema.
- SWAP: espaço do disco usado como RAM extra.

### Sistemas de Arquivos Distribuídos (SAD)

#### 🌐 O que são?

Permitem acessar arquivos armazenados remotamente como se fossem locais.

#### 🧩 Características

- Arquitetura Cliente/Servidor.
- Compartilhamento remoto e concorrente.
- Objetivos: Transparência, escalabilidade, replicação, tolerância a falhas.

#### 🧰 Serviços

- Serviço de nomes: localização de arquivos.
- Serviço de diretórios: estrutura hierárquica.
- Serviço de arquivos: leitura, escrita, bloqueio, etc.

#### 🛠 Exemplos

- NFS (Network File System): Unix/Linux, cliente-servidor simples.
- HDFS (Hadoop File System): escalável, usado em big data.
- GlusterFS, Ceph, GFS: alta disponibilidade, performance e escalabilidade.