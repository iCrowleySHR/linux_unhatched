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

### 🧱 Comandos SQL básicos no MariaDB

Após acessar o MariaDB via terminal com:

```bash
sudo mariadb
```

ou

```bash
mysql -u root -p
```

Você pode executar os comandos abaixo diretamente no prompt (`MariaDB [(none)]>`):

---

#### 📦 Criar um banco de dados

```sql
CREATE DATABASE nome_do_banco;
```

---

#### 👤 Criar um usuário com senha

```sql
CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'senha123';
```

---

#### 🔐 Conceder permissões ao usuário

Dar acesso total ao banco de dados:

```sql
GRANT ALL PRIVILEGES ON nome_do_banco.* TO 'usuario'@'localhost';
```

> Após criar permissões, execute:
```sql
FLUSH PRIVILEGES;
```

---

#### 📄 Criar uma tabela

```sql
USE nome_do_banco;

CREATE TABLE clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    data_cadastro DATE
);
```

---

#### ➕ Inserir dados

```sql
INSERT INTO clientes (nome, email, data_cadastro)
VALUES ('João Silva', 'joao@email.com', CURDATE());
```

---

#### 📄 Listar bancos e tabelas

```sql
SHOW DATABASES;
SHOW TABLES;
```

---

#### 🗑️ Apagar banco, tabela ou usuário

```sql
DROP DATABASE nome_do_banco;
DROP TABLE nome_da_tabela;
DROP USER 'usuario'@'localhost';
```

---

> ✅ Pronto! Com esses comandos você já consegue criar e gerenciar bancos e tabelas no MariaDB.
