
## 📁 SAMBA | Servidor de Arquivos no Linux

O **Samba** permite o compartilhamento de arquivos entre Linux e máquinas Windows na mesma rede, usando o protocolo SMB/CIFS.

---

### 🔧 Instalação dos pacotes

```bash
sudo apt-get install samba smbclient cifs-utils
```

---

### 🧪 Verificar serviços ativos

Para checar se o Samba (e outros serviços) estão ativos no sistema:

```bash
service --status-all
```

---

### ▶️ Gerenciar o serviço do Samba

```bash
sudo service smbd status      # Verifica o status do serviço
sudo service smbd start       # Inicia o serviço
sudo service smbd stop        # Encerra o serviço
sudo service smbd restart     # Reinicia o serviço
```

> ⚠️ Note que o correto é `smbd`, não `smdb`.

---

### 🛠️ Arquivo de configuração do Samba

```bash
/etc/samba/smb.conf
```

- **Recomendado**: manter o original como backup:
```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.original
```

- Crie ou edite seu próprio arquivo:
```bash
sudo nano /etc/samba/smb.conf
```

---

## 📄 Exemplo de configuração `smb.conf`

```ini
[global]
workgroup = WORKGROUP
log file = /var/log/samba/log.sm
syslog = 0
server role = standalone
map to guest = bad user

[dados]
path = /dados
available = yes
browseable = yes
writable = yes
guest ok = yes
```

---

### 🔍 Explicação das diretivas

#### `[global]`
Configurações gerais do servidor Samba.

| Diretiva              | Significado                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `workgroup`           | Nome do grupo de trabalho (usado por máquinas Windows)                      |
| `log file`            | Local onde os logs do Samba serão salvos                                   |
| `syslog`              | Define o nível de log que será enviado ao `syslog` do sistema               |
| `server role`         | Define o papel do servidor (`standalone`, `domain controller`, etc.)       |
| `map to guest`        | Converte logins inválidos em acesso como convidado (`bad user` ativa isso) |

#### `[dados]`
Define um compartilhamento chamado `dados`.

| Diretiva        | Significado                                                        |
|-----------------|---------------------------------------------------------------------|
| `path`          | Caminho para a pasta compartilhada                                 |
| `available`     | Torna o compartilhamento disponível (`yes` ou `no`)                |
| `browseable`    | Permite que o compartilhamento seja visível na rede                |
| `writable`      | Permite escrita na pasta compartilhada                             |
| `guest ok`      | Permite acesso sem autenticação (modo convidado)                   |

---

### 📂 Criar a pasta compartilhada

```bash
sudo mkdir -p /dados
sudo chmod 777 /dados
```

---

### 🔄 Reiniciar o serviço para aplicar

```bash
sudo service smbd restart
```

---

## ⚙️ Configurações adicionais para o `smb.conf`

Além das configurações básicas de `[global]` e dos compartilhamentos, o Samba permite várias customizações úteis.

---

### 🔹 Segurança e autenticação

```ini
security = user              # Requer autenticação com usuário e senha Samba
encrypt passwords = yes      # Ativa senhas criptografadas
guest account = nobody       # Define o usuário usado para acessos como "guest"
invalid users = root         # Impede o usuário root de acessar via Samba
```

---

### 🔹 Controle de acesso

```ini
valid users = joao, maria         # Apenas esses usuários podem acessar
invalid users = root, hacker      # Bloqueia usuários específicos
read only = no                    # Permite escrita (equivale a writable = yes)
write list = joao, maria          # Apenas esses usuários podem escrever
```

---

### 🔹 Compartilhamento somente leitura

```ini
read only = yes
browseable = yes
```

---

### 🔹 Controle de permissões

```ini
create mask = 0775           # Permissões padrão para arquivos criados
directory mask = 0775        # Permissões padrão para diretórios criados
force user = nobody          # Todos os arquivos serão "dono" deste usuário
force group = users          # Todos os arquivos pertencerão a este grupo
```

---

### 🔹 Limitar por IP

```ini
hosts allow = 192.168.1.0/24     # Permite somente a rede local
hosts deny = 0.0.0.0/0           # Bloqueia todas as outras redes
```

---

### 🔹 Compartilhamento de impressoras (exemplo)

```ini
[printers]
comment = Todas as impressoras
path = /var/spool/samba
browseable = no
guest ok = yes
writable = no
printable = yes
```

---

### 🔹 Log personalizado

```ini
log file = /var/log/samba/%m.log     # Cria um log para cada máquina
max log size = 1000                  # Tamanho máximo do log (em KB)
```

---

### 🔹 Performance

```ini
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
```

---

### 🔹 Ocultar arquivos

```ini
hide dot files = yes                 # Oculta arquivos que começam com "."
veto files = /*.tmp/*.bak/*.~*/     # Bloqueia acesso a certos arquivos
```

---

### 🔹 Exemplo completo de um compartilhamento protegido

```ini
[projetos]
path = /srv/projetos
read only = no
browseable = yes
valid users = @dev
create mask = 0660
directory mask = 0770
force group = dev
```

---

## 🧠 Dicas úteis

- Teste o arquivo após alterações:
```bash
testparm
```

- Recarregue o serviço:
```bash
sudo service smbd restart
```

- Para criar usuário Samba:
```bash
sudo smbpasswd -a nome
```

---
