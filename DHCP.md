---

## 🌐 Servidor DHCP no Linux

O servidor **DHCP** (Dynamic Host Configuration Protocol) é responsável por **atribuir endereços IP automaticamente** para os dispositivos da rede.

---

### 🔹 Instalação do serviço

```bash
sudo apt-get install isc-dhcp-server
```

---

### 🔧 Arquivo de configuração

```bash
/etc/dhcp/dhcpd.conf
```

> ✳️ É **recomendado fazer um backup** antes de editar:

```bash
sudo cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.original
sudo nano /etc/dhcp/dhcpd.conf
```

---

## ▶️ Comandos para controlar o serviço

```bash
sudo systemctl status isc-dhcp-server     # Verifica status do serviço
sudo systemctl start isc-dhcp-server      # Inicia o servidor DHCP
sudo systemctl stop isc-dhcp-server       # Encerra o serviço
sudo systemctl restart isc-dhcp-server    # Reinicia o serviço
sudo systemctl enable isc-dhcp-server     # Habilita para iniciar com o sistema
sudo systemctl disable isc-dhcp-server    # Desabilita o serviço na inicialização
```

---

## 📄 Exemplo de configuração básica (`dhcpd.conf`)

```conf
# Tempo padrão e máximo do lease (tempo que o IP será válido)
default-lease-time 600;
max-lease-time 7200;

# Configuração da sub-rede
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  option subnet-mask 255.255.255.0;
  option domain-name-servers 8.8.8.8, 1.1.1.1;
  option domain-name "meurede.local";
}
```

---

### 🔍 Explicação rápida

| Linha                          | Significado                                         |
|-------------------------------|-----------------------------------------------------|
| `default-lease-time`          | Tempo padrão de concessão de IP (em segundos)       |
| `max-lease-time`              | Tempo máximo permitido para manter o IP             |
| `subnet` + `netmask`          | Define a sub-rede atendida                          |
| `range`                       | Faixa de IPs que serão distribuídos                 |
| `option routers`              | Gateway padrão da rede                              |
| `option domain-name-servers` | Servidores DNS atribuídos aos clientes              |
| `option domain-name`          | Nome de domínio fornecido                           |

---

### ⚠️ Após editar, reinicie o serviço:

```bash
sudo systemctl restart isc-dhcp-server
```

---
---

## 📌 Reserva de Endereço IP no Servidor DHCP

A **reserva de IP** garante que um dispositivo específico **sempre receba o mesmo IP**, baseado no **endereço MAC** da sua placa de rede.

---

### 🔧 Adicionando reserva no `dhcpd.conf`

Exemplo prático de como reservar um IP para um dispositivo:

```conf
host impressora {
  hardware ethernet 00:11:22:33:44:55;
  fixed-address 192.168.1.150;
}
```

---

### 🔍 Explicação

| Linha                             | Significado                                           |
|----------------------------------|-------------------------------------------------------|
| `host impressora`                | Nome simbólico da reserva (pode ser qualquer nome)   |
| `hardware ethernet`              | Endereço MAC da máquina/dispositivo                  |
| `fixed-address`                  | IP que será reservado para este MAC                  |

---

### 🔁 Exemplo completo dentro de uma sub-rede

```conf
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  option domain-name-servers 8.8.8.8, 1.1.1.1;

  host servidor {
    hardware ethernet AA:BB:CC:DD:EE:FF;
    fixed-address 192.168.1.10;
  }

  host impressora {
    hardware ethernet 00:11:22:33:44:55;
    fixed-address 192.168.1.150;
  }
}
```

---

### 🔐 Dica

- O IP reservado **não precisa estar dentro do `range`**, mas deve estar **dentro da sub-rede**.
- Evite conflitos com IPs estáticos manuais ou outras reservas.

---

### 🔄 Após modificar o arquivo

```bash
sudo systemctl restart isc-dhcp-server
```

E verifique o status:
```bash
sudo systemctl status isc-dhcp-server
```

---

### 📋 Descobrir o MAC Address

Para identificar o MAC do dispositivo, você pode usar:

```bash
ip link                 # No Linux
getmac                  # No Windows
```

Ou ver no roteador/switch se o cliente já conectou alguma vez.

---
