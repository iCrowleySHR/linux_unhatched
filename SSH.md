### 🔐 Acesso remoto com SSH

O **SSH (Secure Shell)** permite acessar um servidor Linux de forma remota e segura via terminal.

#### 🧰 Requisitos

- O servidor deve ter o **serviço SSH** instalado e em execução.
- É necessário saber o **IP** ou **nome do host**, e ter um **usuário com acesso**.

---

#### 📦 Instalar o OpenSSH (caso necessário)

No servidor:

```bash
sudo apt update
sudo apt install openssh-server -y
```

Inicie e habilite o serviço:

```bash
sudo systemctl enable --now ssh
```

Verifique o status:

```bash
sudo systemctl status ssh
```

---

#### 💻 Conectar via SSH

Do computador cliente (Linux, macOS, ou Windows com terminal compatível):

```bash
ssh usuario@ip_do_servidor
```

Exemplo:

```bash
ssh gustavo@192.168.1.100
```

---

#### 🔑 Usar porta diferente (se configurado)

```bash
ssh -p 2222 usuario@ip_do_servidor
```

---

#### 📁 Copiar arquivos com `scp`

Copiar um arquivo do seu PC para o servidor:

```bash
scp arquivo.txt usuario@ip:/caminho/do/destino
```

Copiar do servidor para o seu PC:

```bash
scp usuario@ip:/caminho/arquivo.txt .
```

---

#### 🔐 Acesso com chave SSH (mais seguro)

1. Gerar par de chaves no cliente:

```bash
ssh-keygen -t rsa -b 4096
```

2. Copiar a chave pública para o servidor:

```bash
ssh-copy-id usuario@ip_do_servidor
```

3. A partir daí, não será mais necessário digitar a senha.

---

#### 🔓 2. Permitir login root via SSH (opcional e não recomendado em ambientes públicos)

> ⚠️ Use com cautela — habilitar o root via SSH pode ser um risco de segurança.

Edite o arquivo de configuração do SSH:

```bash
sudo nano /etc/ssh/sshd_config
```

Altere ou adicione as seguintes linhas:

```
PermitRootLogin yes
PasswordAuthentication yes
```

> 🚫 Se quiser permitir **apenas com chave SSH**, use:
> ```
> PermitRootLogin prohibit-password
> ```

---

#### 🔄 3. Reiniciar o serviço SSH

```bash
sudo systemctl restart ssh
```

---

#### 💻 4. Conectar como root via SSH

```bash
ssh root@ip_do_servidor
```

---
