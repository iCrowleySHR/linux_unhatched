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

## 🔍 Comando `nslookup`

O comando `nslookup` (Name Server Lookup) é usado para **consultar registros DNS** de domínios, como endereços IP, servidores de e-mail (MX), entre outros.

---

### 🔹 Sintaxe
```bash
nslookup [opções] [domínio ou IP]
```

---

### 🔹 Exemplos básicos

```bash
nslookup google.com              # Retorna o IP do domínio
nslookup 8.8.8.8                 # Retorna o domínio associado ao IP (PTR)
```

---

### 🔹 Consultar usando um servidor DNS específico

```bash
nslookup google.com 1.1.1.1     # Consulta usando o DNS da Cloudflare
```

---

### 🔹 Modo interativo

Você pode digitar apenas:
```bash
nslookup
```
E depois usar comandos no prompt interativo, como:

```text
> set type=MX
> gmail.com
```

---

### 🔹 Tipos de consulta suportados

| Tipo        | Descrição                         |
|-------------|-----------------------------------|
| `A`         | Endereço IPv4 do domínio          |
| `AAAA`      | Endereço IPv6                     |
| `MX`        | Servidores de e-mail              |
| `NS`        | Servidores de nome do domínio     |
| `CNAME`     | Nome canônico (alias)             |
| `PTR`       | Inverso (IP → nome)               |
| `SOA`       | Início da autoridade DNS          |

---

### 🔹 Exemplo: buscar registros MX

```bash
nslookup -type=MX gmail.com
```

---

### 🔐 Dica

Se `nslookup` não estiver instalado:
```bash
sudo apt install dnsutils       # Debian/Ubuntu
sudo yum install bind-utils     # RHEL/CentOS
```

---

### 🆚 Alternativas

| Comando     | Função similar            |
|-------------|---------------------------|
| `dig`       | Consulta DNS avançada     |
| `host`      | Consulta simples e direta |

---

## 🔗 Comando `ss`

O comando `ss` (socket statistics) é usado para **listar conexões de rede ativas, portas em uso, escuta de serviços**, entre outras informações. É uma alternativa moderna e mais rápida ao antigo `netstat`.

---

### 🔹 Sintaxe
```bash
ss [opções]
```

---

### 🔹 Exemplos comuns

```bash
ss -tuln                   # Lista portas TCP/UDP em escuta (listen)
ss -s                      # Mostra estatísticas de sockets
ss -tn                     # Lista conexões TCP estabelecidas (com IPs)
ss -tuna                  # TCP/UDP + IPv4/IPv6 + nomes e IPs
```

---

### 🔹 Explicação das opções principais

| Opção   | Descrição                               |
|---------|-------------------------------------------|
| `-t`    | Conexões TCP                             |
| `-u`    | Conexões UDP                             |
| `-l`    | Mostra apenas sockets em escuta (listening) |
| `-n`    | Não resolve nomes de domínio/serviços     |
| `-p`    | Mostra o processo/programa que usa a porta |
| `-a`    | Mostra todas as conexões (inclusive escuta) |
| `-s`    | Mostra resumo estatístico (como `netstat -s`) |

---

### 🔹 Ver porta e programa associado

```bash
sudo ss -tulnp
```

> Mostra portas de rede em escuta, com PID e nome do processo.

---

### 🔹 Filtrar por porta ou endereço

```bash
ss -tuln sport = :80              # Ver conexões na porta 80
ss -tn dst 192.168.0.1            # Conexões com destino ao IP informado
```

---

### 🧠 Dica

Use `ss` com `grep` para refinar resultados:

```bash
ss -tuln | grep 443
```

---

### 🆚 Comparativo: `ss` vs `netstat`

| Função               | `ss`         | `netstat`    |
|----------------------|--------------|--------------|
| Velocidade           | Mais rápido  | Mais lento   |
| Detalhamento         | Mais completo| Menos detalhado |
| Futuro               | Recomendado  | Obsoleto     |

---

### 🔐 Instalação (se necessário)

```bash
sudo apt install iproute2        # Debian/Ubuntu
sudo yum install iproute         # Red Hat/CentOS
```

---

## 🌍 Comando `traceroute`

O comando `traceroute` é usado para **mapear o caminho que os pacotes percorrem até um destino** (domínio ou IP), mostrando cada salto (roteador) e o tempo de resposta.

---

### 🔹 Sintaxe
```bash
traceroute [opções] destino
```

---

### 🔹 Exemplo básico

```bash
traceroute google.com
```

> Mostra todos os roteadores entre sua máquina e o site do Google.

---

### 🔹 Interpretação da saída

```text
1  192.168.0.1    1.123 ms  0.873 ms  0.799 ms
2  10.1.1.1       2.503 ms  2.447 ms  2.410 ms
3  8.8.8.8        20.122 ms 19.899 ms 20.045 ms
```

| Coluna               | Significado                         |
|----------------------|-------------------------------------|
| Número               | Ordem do salto (hop)                |
| IP ou domínio        | Endereço do roteador no caminho     |
| Tempos em ms         | Tempo de resposta de cada tentativa |

---

### 🔹 Opções úteis

| Opção         | Descrição                                       |
|---------------|-------------------------------------------------|
| `-n`          | Não resolve nomes de domínio (mostra só IPs)    |
| `-m N`        | Define número máximo de saltos (padrão: 30)     |
| `-w SEG`      | Define tempo de espera por resposta (timeout)   |
| `-q N`        | Número de tentativas por salto (padrão: 3)      |
| `-I`          | Usa ICMP (como o `ping`) no lugar de UDP        |

---

### 🔹 Exemplo com IPs e 10 saltos

```bash
traceroute -n -m 10 8.8.8.8
```

---

### 🔐 Instalação (se necessário)

```bash
sudo apt install traceroute       # Debian/Ubuntu
sudo yum install traceroute       # Red Hat/CentOS
```

> O comando pode ser chamado de `tracert` em alguns sistemas (como no Windows).

---

### 🧠 Dica

Se `traceroute` estiver bloqueado ou filtrado por firewall, tente:

```bash
traceroute -T google.com       # Usa TCP em vez de UDP
```

---


