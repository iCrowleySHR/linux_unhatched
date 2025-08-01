---

## 🌐 Servidor Web Apache2

O **Apache2** é um servidor HTTP de código aberto usado para **hospedar sites e aplicações web** em sistemas Linux.

---

### 🔹 Instalação

```bash
sudo apt update
sudo apt install apache2
```

---

### ▶️ Comandos para gerenciar o serviço

```bash
sudo systemctl status apache2     # Verifica o status do serviço
sudo systemctl start apache2      # Inicia o serviço
sudo systemctl stop apache2       # Encerra o serviço
sudo systemctl restart apache2    # Reinicia o serviço
sudo systemctl enable apache2     # Habilita o serviço na inicialização
```

---

### 📁 Estrutura de diretórios padrão

| Caminho                          | Função                                               |
|----------------------------------|------------------------------------------------------|
| `/var/www/html/`                 | Diretório padrão dos sites                           |
| `/etc/apache2/apache2.conf`      | Arquivo de configuração principal do Apache         |
| `/etc/apache2/sites-available/`  | Onde ficam os arquivos de configuração dos sites    |
| `/etc/apache2/sites-enabled/`    | Onde ficam os sites ativos (links simbólicos)       |
| `/etc/apache2/ports.conf`        | Porta padrão do Apache (por padrão, 80 e 443)       |
| `/var/log/apache2/`              | Diretório onde ficam os arquivos de log             |

---

### 🌐 Acessar o servidor

Após instalar e iniciar, acesse via navegador:
```
http://localhost
```
Ou, de outro computador na rede:
```
http://IP_DO_SERVIDOR
```

---

### ✏️ Criar página personalizada

Edite o arquivo padrão:
```bash
sudo nano /var/www/html/index.html
```

---

### 🔧 Criando um Virtual Host

1. Crie a pasta do novo site:
```bash
sudo mkdir -p /var/www/meusite.com.br/public_html
```

2. Defina permissões:
```bash
sudo chown -R $USER:$USER /var/www/meusite.com.br
sudo chmod -R 755 /var/www
```

3. Crie o arquivo HTML de teste:
```bash
echo "<h1>Olá, Apache!</h1>" > /var/www/meusite.com.br/public_html/index.html
```

4. Crie o Virtual Host:
```bash
sudo nano /etc/apache2/sites-available/meusite.com.br.conf
```

Conteúdo do arquivo:

```apache
<VirtualHost *:80>
    ServerAdmin webmaster@meusite.com.br
    ServerName meusite.com.br
    ServerAlias www.meusite.com.br
    DocumentRoot /var/www/meusite.com.br/public_html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

5. Ative o novo site e reinicie o Apache:

```bash
sudo a2ensite meusite.com.br.conf
sudo systemctl reload apache2
```

---

### ⚠️ Habilitar o `mod_rewrite` (para URLs amigáveis)

```bash
sudo a2enmod rewrite
sudo systemctl restart apache2
```

---

### 🔐 Permissões básicas

```bash
sudo chown -R www-data:www-data /var/www
sudo chmod -R 755 /var/www
```

---

### 🧪 Testar configuração

```bash
sudo apache2ctl configtest
```

---

### 💡 Arquivos úteis

| Arquivo                          | Descrição                          |
|----------------------------------|------------------------------------|
| `/etc/apache2/envvars`           | Variáveis de ambiente               |
| `/var/log/apache2/error.log`     | Log de erros do Apache              |
| `/var/log/apache2/access.log`    | Log de acessos                      |

---


