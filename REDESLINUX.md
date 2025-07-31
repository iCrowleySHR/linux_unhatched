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

