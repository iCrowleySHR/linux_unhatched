---

## 🌐 Comando `ip`

O comando `ip` é usado para **configurar, visualizar e gerenciar interfaces de rede**, IPs, rotas e links. Ele faz parte do pacote `iproute2` e **substitui o antigo `ifconfig`**.

---

### 🔹 Sintaxe
```bash
ip [objeto] [opções]
```

**Principais objetos:** `addr`, `link`, `route`, `neigh`, `rule`

---

### 🔹 Ver informações de rede

```bash
ip a                   # Lista endereços IP das interfaces (atalho para "ip addr")
ip addr show           # Mesmo que acima
ip addr show eth0      # Mostra IP apenas da interface eth0
```

---

### 🔹 Listar interfaces de rede

```bash
ip link                # Lista interfaces de rede
ip link show           # Igual ao comando acima
```

---

### 🔹 Ativar/desativar interface

```bash
sudo ip link set eth0 up      # Ativa a interface eth0
sudo ip link set eth0 down    # Desativa a interface eth0
```

---

### 🔹 Adicionar/Remover IP

```bash
sudo ip addr add 192.168.1.10/24 dev eth0       # Adiciona IP à interface
sudo ip addr del 192.168.1.10/24 dev eth0       # Remove IP da interface
```

---

### 🔹 Ver rotas

```bash
ip route              # Mostra tabela de roteamento
```

---

### 🔹 Adicionar rota estática

```bash
sudo ip route add 192.168.2.0/24 via 192.168.1.1
```

---

### 🔹 Ver vizinhança ARP (como `arp -a`)

```bash
ip neigh
```

---

### 🔹 Dica

Use `ip -c` para saída colorida:
```bash
ip -c a
```

---

### 🧠 Substituição de comandos antigos

| Antigo (`ifconfig`, `route`, etc) | Novo (`ip`)                        |
|----------------------------------|-----------------------------------|
| `ifconfig`                       | `ip addr`                         |
| `ifconfig eth0 up`               | `ip link set eth0 up`             |
| `route -n`                       | `ip route`                        |
| `arp -a`                         | `ip neigh`                        |

---


## 🌐 Configuração Manual de IP Estático (`/etc/network/interfaces`)

No Debian e derivados (como Ubuntu Server), é possível configurar a interface de rede manualmente pelo arquivo:

```bash
/etc/network/interfaces
```

---

### 🔹 Exemplo de configuração

```bash
auto enp0s3
iface enp0s3 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    network 192.168.1.0
    broadcast 192.168.1.255
    gateway 192.168.1.1
```

---

### 🔹 Explicação linha a linha

| Linha                         | Significado                                              |
|------------------------------|----------------------------------------------------------|
| `auto enp0s3`                | Interface será ativada automaticamente na inicialização |
| `iface enp0s3 inet static`   | Define que o IP será manual (estático)                  |
| `address 192.168.1.100`      | IP atribuído à máquina                                   |
| `netmask 255.255.255.0`      | Máscara de sub-rede (classe C padrão)                   |
| `network 192.168.1.0`        | Endereço da rede                                         |
| `broadcast 192.168.1.255`    | Endereço de broadcast da rede                           |
| `gateway 192.168.1.1`        | IP do gateway padrão (roteador)                         |

---

### 🔹 Ativar a configuração

Após editar o arquivo:

```bash
sudo systemctl restart networking
```

ou, dependendo do sistema:

```bash
sudo ifdown enp0s3 && sudo ifup enp0s3
```

---

### ⚠️ Dica

- Use `ip a` ou `ip addr` para verificar se a interface recebeu o IP.
- Em sistemas modernos (Ubuntu Desktop), o **Netplan** pode ser usado no lugar desse método.

---

## 📶 Comando `ping`

O comando `ping` é usado para **testar a conectividade de rede** entre o seu computador e outro dispositivo (host). Ele envia pacotes ICMP e mede o tempo de resposta.

---

### 🔹 Sintaxe
```bash
ping [opções] destino
```

- `destino`: pode ser um endereço IP ou domínio (ex: `8.8.8.8` ou `google.com`)

---

### 🔹 Exemplos

```bash
ping google.com              # Testa conexão com o Google
ping 8.8.8.8                 # Testa conexão com servidor DNS do Google
ping -c 4 github.com         # Envia apenas 4 pacotes
```

---

### 🔹 Opções úteis

| Opção      | Descrição                                   |
|------------|---------------------------------------------|
| `-c N`     | Envia apenas N pacotes                      |
| `-i SEG`   | Intervalo de tempo entre pacotes            |
| `-s TAM`   | Define o tamanho do pacote em bytes         |
| `-t TEMPO` | Define o TTL (Time To Live) dos pacotes     |
| `-q`       | Modo silencioso (apenas resumo no final)    |

---

### 🔹 Exemplo com intervalo e tamanho

```bash
ping -c 5 -i 2 -s 128 8.8.8.8
```
> Envia 5 pacotes de 128 bytes com intervalo de 2 segundos.

---

### 🔹 Interpretando a saída

```bash
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=20.3 ms
```

| Campo       | Significado                          |
|-------------|--------------------------------------|
| `64 bytes`  | Tamanho do pacote                    |
| `icmp_seq`  | Número sequencial do pacote ICMP     |
| `ttl`       | Tempo de vida (número de saltos)     |
| `time`      | Tempo de resposta (latência)         |

---

### 🔐 Dica

Se `ping` não estiver instalado:
```bash
sudo apt install iputils-ping        # Debian/Ubuntu
sudo yum install iputils             # RHEL/CentOS
```

---

## 🌐 Como Trocar o DNS no Linux

Trocar o DNS (Domain Name System) pode melhorar a velocidade de navegação ou evitar bloqueios regionais. A configuração depende do sistema e gerenciador de rede usado.

---

## 🔧 Método 1: Editando `/etc/resolv.conf`

> ⚠️ Funciona em sistemas simples ou servidores sem gerenciador de rede.

### 🔹 Passo a passo

```bash
sudo nano /etc/resolv.conf
```

### 🔹 Exemplo de conteúdo:

```bash
nameserver 8.8.8.8
nameserver 1.1.1.1
```

> Onde:
> - `8.8.8.8` = Google DNS
> - `1.1.1.1` = Cloudflare DNS

### 🔸 Observação:
Esse arquivo pode ser sobrescrito por serviços como `NetworkManager` ou `systemd-resolved`.

---

## 🔧 Método 2: Para sistemas com NetworkManager (mais comum)

### 🔹 Configurar DNS permanentemente

```bash
nmcli con show                      # Lista conexões de rede
nmcli con mod "nome-da-conexao" ipv4.dns "8.8.8.8 1.1.1.1"
nmcli con mod "nome-da-conexao" ipv4.ignore-auto-dns yes
nmcli con up "nome-da-conexao"     # Reinicia a conexão
```

### 🔹 Exemplo completo:

```bash
nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8 1.1.1.1"
nmcli con mod "Wired connection 1" ipv4.ignore-auto-dns yes
nmcli con up "Wired connection 1"
```

---

## 🔧 Método 3: Usando Netplan (Ubuntu Server)

Se estiver usando Netplan (Ubuntu 18.04+, sem NetworkManager):

### 🔹 Editar o arquivo de configuração YAML

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```

### 🔹 Exemplo:

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

### 🔹 Aplicar as mudanças:

```bash
sudo netplan apply
```

---

## 🔍 Verificar DNS atual

```bash
cat /etc/resolv.conf
```

ou

```bash
nmcli dev show | grep DNS
```

---

### ✅ DNS recomendados

| Provedor     | Endereços                    |
|--------------|------------------------------|
| Google       | `8.8.8.8`, `8.8.4.4`          |
| Cloudflare   | `1.1.1.1`, `1.0.0.1`          |
| OpenDNS      | `208.67.222.222`, `208.67.220.220` |

---

