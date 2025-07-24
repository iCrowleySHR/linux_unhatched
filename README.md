# Linux Unhatched
Curso da Cisco sobre o sistema operacional Linux.

---

## 📂 Comando `ls`

O comando `ls` (list) é utilizado em sistemas Unix/Linux para **listar o conteúdo de diretórios**.

### 🔹 Sintaxe
```bash
ls [opções] [caminho]
```

Se nenhum caminho for especificado, o `ls` exibirá o conteúdo do diretório atual.

### 🔹 Opções comuns
- `ls -l` → Exibe os arquivos em formato de lista detalhada.
- `ls -a` → Mostra arquivos ocultos (que começam com `.`).
- `ls -h` → Exibe tamanhos de arquivos em formato legível (usar com `-l`).
- `ls -r` → Lista os arquivos em ordem reversa.
- `ls -t` → Organiza por data de modificação.
- `ls -R` → Lista o conteúdo de diretórios recursivamente.

---

## 📌 Comando `pwd`

Exibe o **caminho absoluto** do diretório atual.

### 🔹 Sintaxe
```bash
pwd
```

---

## 🔐 Comando `su`

Troca para o usuário root (ou outro usuário), iniciando um novo shell com permissões elevadas.

### 🔹 Sintaxe
```bash
su
```

Será solicitada a senha do usuário. Para sair do shell de root:
```bash
exit
```

---

## 🔐 Comando `sudo`

Permite executar comandos como outro usuário (normalmente o root), **sem mudar de shell**.

### 🔹 Sintaxe
```bash
sudo [opções] comando
```

---

## 🔒 Permissões no Linux

As permissões controlam quem pode **ler**, **escrever** e **executar** arquivos e diretórios.

### 🔹 Grupos de usuários
- **Dono (user)** – proprietário do arquivo
- **Grupo (group)** – usuários do mesmo grupo
- **Outros (others)** – qualquer outro usuário

### 🔹 Tipos de permissão
- `r` (read) → Leitura
- `w` (write) → Escrita
- `x` (execute) → Execução

### 🔹 Ver permissões com:
```bash
ls -l
```

### 🔹 Exemplo de saída:
```bash
-rwxr-xr-- 1 usuario grupo 1024 Mar 16 12:00 script.sh
```

**Explicação:**
- `-` → Arquivo comum (`d` seria diretório)
- `rwx` → Permissões do dono: leitura, escrita e execução
- `r-x` → Permissões do grupo: leitura e execução
- `r--` → Permissões para outros: somente leitura

---

## 📊 Tabela de Permissões

| Valor | Permissões | Significado               |
|-------|------------|---------------------------|
| 0     | ---        | Nenhuma permissão         |
| 1     | --x        | Somente execução          |
| 2     | -w-        | Somente escrita           |
| 3     | -wx        | Escrita e execução        |
| 4     | r--        | Somente leitura           |
| 5     | r-x        | Leitura e execução        |
| 6     | rw-        | Leitura e escrita         |
| 7     | rwx        | Leitura, escrita, execução|

### 🔹 Exemplos comuns
- `777` → Todos com leitura, escrita e execução (`rwxrwxrwx`)
- `755` → Dono com tudo; grupo e outros com leitura e execução (`rwxr-xr-x`)
- `644` → Dono com leitura e escrita; grupo e outros só leitura (`rw-r--r--`)
- `600` → Somente o dono pode ler e escrever (`rw-------`)

### 🔹 Modificar permissões:
```bash
chmod 755 arquivo
```

---

## 📁 Criar Diretórios

Cria novos diretórios com o comando `mkdir`.

### 🔹 Sintaxe:
```bash
mkdir [nome_do_diretorio]
```

### 🔹 Exemplos:
```bash
mkdir projetos
mkdir -p pasta1/pasta2/pasta3
```

---

## 🗑️ Remover Arquivos e Diretórios

### 🔹 Remover arquivos:
```bash
rm arquivo.txt
```

### 🔹 Remover diretórios vazios:
```bash
rmdir nome_do_diretorio
```

### 🔹 Remover diretórios com conteúdo:
```bash
rm -r nome_do_diretorio
```

⚠️ Use com cuidado:
```bash
rm -rf pasta/
```

---

## ✏️ Renomear e Mover Arquivos ou Diretórios

O comando `mv` serve para **mover** ou **renomear**.

### 🔹 Sintaxe:
```bash
mv origem destino
```

### 🔹 Exemplos:
```bash
mv arquivo.txt novo_arquivo.txt
mv arquivo.txt /home/usuario/docs/
mv pasta1 nova_pasta
```

---

## 📄 Copiar Arquivos e Diretórios

O comando `cp` é utilizado para **copiar arquivos e pastas**.

### 🔹 Copiar arquivo:
```bash
cp arquivo.txt copia.txt
```

### 🔹 Copiar para outro diretório:
```bash
cp arquivo.txt /home/usuario/docs/
```

### 🔹 Copiar diretório com conteúdo:
```bash
cp -r pasta_origem pasta_destino
```

---
