---

## 🌐 Ativando Servidor de Internet com Comandos Diretos (NAT)

Estes comandos transformam rapidamente uma máquina Linux com duas interfaces em um **gateway NAT**, compartilhando a internet da interface externa para a rede local.

---

### 📋 Comandos utilizados

```bash
modprobe iptable_nat
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
```

---

### 🔍 Explicação linha por linha

| Comando                                                    | Descrição                                                                 |
|------------------------------------------------------------|---------------------------------------------------------------------------|
| `modprobe iptable_nat`                                     | Carrega o módulo de NAT no kernel (útil em sistemas mais antigos)        |
| `echo 1 > /proc/sys/net/ipv4/ip_forward`                   | Habilita o encaminhamento de pacotes entre interfaces                     |
| `iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE`   | Aplica NAT para os pacotes que saem pela interface externa (`enp0s3`)    |

---

### ⚠️ Observações

- Esses comandos são **temporários** (válidos até o próximo reboot).
- Para torná-los **permanentes**, use:
  - `/etc/sysctl.conf` para o `ip_forward`
  - `iptables-persistent` ou `netfilter-persistent` para salvar as regras

---

### 💾 Tornar o encaminhamento permanente

```bash
sudo nano /etc/sysctl.conf
```

Descomente ou adicione:

```conf
net.ipv4.ip_forward = 1
```

Aplicar sem reiniciar:

```bash
sudo sysctl -p
```

---

### 💾 Salvar regra do iptables

```bash
sudo apt install iptables-persistent
sudo netfilter-persistent save
```

---

### ✅ Interface externa

Certifique-se de substituir `enp0s3` pela **interface de rede que tem acesso à internet**.

---

