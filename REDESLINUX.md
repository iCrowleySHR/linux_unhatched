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

