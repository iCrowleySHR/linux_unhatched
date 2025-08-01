### 🐬 Instalação do MariaDB

O **MariaDB** é um sistema de gerenciamento de banco de dados relacional compatível com o MySQL, muito utilizado em servidores Linux.

#### 🧰 Instalar o MariaDB

No Debian, Ubuntu e derivados:

```bash
sudo apt update
sudo apt install mariadb-server -y
```

No RHEL, Fedora, CentOS e derivados:

```bash
sudo dnf install mariadb-server -y
```

#### ▶️ Iniciar e habilitar o serviço

```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

#### 🔒 Configurar segurança inicial

Use o script de configuração segura para definir senha do root, remover usuários anônimos, etc.:

```bash
sudo mysql_secure_installation
```

Siga as instruções interativas para:

- Definir senha do usuário root
- Remover usuários anônimos
- Desabilitar login remoto do root
- Remover banco de dados de teste
- Recarregar as tabelas de privilégios

#### 💡 Acessar o MariaDB no terminal

```bash
sudo mariadb
```

Ou, se estiver com senha configurada para o root:

```bash
mysql -u root -p
```

#### 🧪 Verificar versão instalada

```bash
mariadb --version
```

---

> ✅ Pronto! O MariaDB está instalado e pronto para uso. Você pode agora criar bancos de dados, usuários e permissões conforme necessário.

