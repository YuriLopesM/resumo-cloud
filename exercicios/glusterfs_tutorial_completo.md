
# 🧰 Tutorial Completo: GlusterFS com Cluster Redundante + Configuração de Rede (Linux)

---

## 🎯 Objetivo

Criar uma matriz de armazenamento em cluster usando **GlusterFS**, com replicação de dados entre dois servidores. Isso fornece alta disponibilidade e funcionamento semelhante a RAID 1 pela rede.

---

## 🖥️ Identificação das Máquinas Virtuais

- `gluster0` – Servidor 1  
- `gluster1` – Servidor 2  
- `gluster2` – Cliente  

---

## 🧾 Etapa 1: Configuração do `/etc/hosts` em todas as VMs

```bash
sudo nano /etc/hosts
```

Adicione:

```
127.0.0.1       localhost
first_ip_address   gluster0.satc.net.br gluster0
second_ip_address  gluster1.satc.net.br gluster1
third_ip_address   gluster2.satc.net.br gluster2
```

---

## 📦 Etapa 2: Instalar repositório e atualizar pacotes (em todos os servidores)

```bash
sudo add-apt-repository ppa:gluster/glusterfs-7
sudo apt update
```

---

## 🔧 Etapa 3: Instalar e ativar o GlusterFS (gluster0 e gluster1)

```bash
sudo apt install glusterfs-server
sudo systemctl start glusterd.service
sudo systemctl enable glusterd.service
sudo systemctl status glusterd.service
```

---

## 🤝 Etapa 4: Conectar os nós ao cluster

No `gluster0`, execute:

```bash
sudo gluster peer probe gluster1
```

Verifique o status:

```bash
sudo gluster peer status
```

---

## 📂 Etapa 5: Criar volume de armazenamento replicado

1. Crie o diretório em ambos os servidores:

```bash
sudo mkdir /gluster-storage
```

2. Crie o volume do tipo réplica:

```bash
sudo gluster volume create volume1 replica 2 gluster0.satc.net.br:/gluster-storage gluster1.satc.net.br:/gluster-storage force
```

3. Inicie o volume:

```bash
sudo gluster volume start volume1
```

4. Verifique o status:

```bash
sudo gluster volume status
```

---

## 💻 Etapa 6: Configuração no Cliente (gluster2)

1. Instalar o cliente:

```bash
sudo apt install glusterfs-client
```

2. Criar ponto de montagem e montar o volume:

```bash
sudo mkdir /storage-pool
sudo mount -t glusterfs gluster0.satc.net.br:/volume1 /storage-pool
```

3. Verifique com:

```bash
df
```

4. Teste de gravação:

```bash
cd /storage-pool
sudo touch file_{0..9}.test
ls /gluster-storage
```

---

## 📊 Etapa 7: Comandos úteis do GlusterFS

Informações do volume:

```bash
sudo gluster volume info
```

Status dos nós:

```bash
sudo gluster peer status
```

Ativar análise de desempenho:

```bash
sudo gluster volume profile volume1 start
sudo gluster volume profile volume1 info
```

---

# 🌐 Configuração de Rede com ifupdown (em vez de Netplan)

## 🧹 Remover Netplan e NetworkManager

```bash
sudo apt install ifupdown
sudo apt purge network-manager netplan.io
sudo rm -rf /etc/netplan/*.yml
```

---

## ⚙️ Editar `/etc/network/interfaces`

```bash
sudo nano /etc/network/interfaces
```

Adicione o seguinte conteúdo:

```
auto lo
iface lo inet loopback

auto enp0s3
iface enp0s3 inet dhcp

auto enp0s8
iface enp0s8 inet static
address 192.168.36.1
netmask 255.255.255.0
```

> 🔎 Use `ip a` para descobrir os nomes reais das interfaces de rede e substitua `enp0s3` e `enp0s8`.

---

## 🔁 Reiniciar serviço de rede

```bash
sudo ifdown enp0s8 && sudo ifup enp0s8
```

---

## 📚 Referência Extra

Tutorial oficial do Netplan (caso prefira mantê-lo):  
🔗 https://netplan.readthedocs.io/en/stable/netplan-tutorial/

---

✅ **Pronto!** Agora você possui um cluster de armazenamento redundante com GlusterFS e rede configurada de forma estática e confiável.
