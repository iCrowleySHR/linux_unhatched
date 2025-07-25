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


## 🔗 Comando `ln` – Entendendo e Criando Links

O comando `ln` é usado para **criar links** para arquivos ou diretórios no Linux.

### 🔹 Tipos de Links
- **Hard Link (link físico)**: Aponta diretamente para os dados do arquivo no disco. Só pode ser criado dentro do mesmo sistema de arquivos.
- **Symbolic Link (link simbólico ou "atalho")**: Aponta para o caminho de outro arquivo ou diretório. Pode cruzar sistemas de arquivos.

### 🔹 Sintaxe
```bash
ln arquivo_original link_fisico
ln -s destino link_simbolico
```

### 🔹 Exemplos
```bash
ln meu_script.sh backup_script.sh       # Hard link
ln -s /var/log/syslog log_syslog        # Link simbólico
```

### 🔹 Visualizar links
```bash
ls -l
```

Saída:
```bash
lrwxrwxrwx 1 usuario grupo  12 Jul 24 10:00 log_syslog -> /var/log/syslog
```

---

## 📦 Arquivando e Compactando Arquivos e Diretórios

Linux oferece utilitários para **arquivar** e **compactar** arquivos, otimizando espaço em disco.

### 🔹 Arquivar com `tar`
```bash
tar -cvf arquivo.tar pasta/       # Cria um arquivo tar
tar -xvf arquivo.tar              # Extrai arquivo tar
```

- `c` → criar
- `v` → verboso (detalhado)
- `f` → nome do arquivo

### 🔹 Compactar com `gzip` ou `bzip2`
```bash
gzip arquivo.txt     # Cria arquivo.txt.gz
bzip2 arquivo.txt    # Cria arquivo.txt.bz2
```

### 🔹 Descompactar
```bash
gunzip arquivo.txt.gz
bunzip2 arquivo.txt.bz2
```

### 🔹 Arquivar e compactar juntos
```bash
tar -czvf arquivo.tar.gz pasta/     # Usando gzip
tar -cjvf arquivo.tar.bz2 pasta/    # Usando bzip2
```

### 🔹 Descompactar `.tar.gz` e `.tar.bz2`
```bash
tar -xzvf arquivo.tar.gz
tar -xjvf arquivo.tar.bz2
```

---

## 🔍 Procurando por Arquivos

O comando `find` localiza arquivos e diretórios com base em critérios como nome, tipo, tamanho ou data.

### 🔹 Sintaxe
```bash
find [caminho] [condições]
```

### 🔹 Exemplos
```bash
find . -name "teste.txt"                  # Procura por nome
find /home -type d -name "projetos"       # Diretórios com nome "projetos"
find / -type f -size +10M                 # Arquivos maiores que 10 MB
find . -mtime -7                          # Arquivos modificados nos últimos 7 dias
find . -user nome_usuario                 # Arquivos pertencentes a um usuário
```

---

---

## 📖 Comando `cat`

O comando `cat` (concatenate) é usado para **exibir o conteúdo de arquivos** no terminal.

### 🔹 Sintaxe
```bash
cat [arquivo]
```

### 🔹 Exemplos
```bash
cat texto.txt                 # Exibe o conteúdo do arquivo
cat arquivo1 arquivo2         # Mostra ambos, um após o outro
cat > novo.txt                # Cria novo arquivo (CTRL+D para sair)
```

⚠️ Com arquivos muito grandes, `cat` pode rolar rápido demais. Nesse caso, use `less`.

---

## 📚 Comando `less`

O comando `less` permite **navegar por arquivos longos** de forma interativa, **página por página**.

### 🔹 Sintaxe
```bash
less [arquivo]
```

### 🔹 Navegação
- `barra de espaço` → avança uma página
- `seta para cima/baixo` → rola linha a linha
- `/palavra` → busca por palavra
- `q` → sai do visualizador

### 🔹 Exemplo
```bash
less /var/log/syslog
```

Ideal para ler logs ou arquivos extensos com controle.

---
---

## 🔢 Comando `sort`

O comando `sort` organiza o conteúdo de arquivos **em ordem alfabética ou numérica**.

### 🔹 Sintaxe
```bash
sort [opções] [arquivo]
```

### 🔹 Exemplos
```bash
sort nomes.txt                   # Ordem alfabética
sort -r nomes.txt                # Ordem reversa
sort -n numeros.txt              # Ordenação numérica
sort -u palavras.txt             # Remove duplicatas
```

### 🔹 Combinando com outros comandos
```bash
cat dados.txt | sort | uniq
```

---

## 📊 Comando `wc`

O comando `wc` (word count) exibe o número de **linhas, palavras e caracteres** em arquivos.

### 🔹 Sintaxe
```bash
wc [opções] [arquivo]
```

### 🔹 Opções comuns
- `-l` → Contar linhas
- `-w` → Contar palavras
- `-c` → Contar bytes
- `-m` → Contar caracteres

### 🔹 Exemplos
```bash
wc arquivo.txt                  # Linhas, palavras e bytes
wc -l arquivo.txt               # Apenas número de linhas
wc -w texto.txt                 # Apenas número de palavras
```

### 🔹 Combinando com outros comandos
```bash
cat arquivo.txt | wc -l         # Conta linhas da saída do cat
```

---


## 🔍 Comando `grep`

O comando `grep` é utilizado para **procurar padrões de texto** em arquivos ou na saída de outros comandos.

### 🔹 Sintaxe
```bash
grep [opções] "padrão" [arquivo]
```

### 🔹 Exemplos básicos
```bash
grep "erro" log.txt              # Busca a palavra "erro"
grep -i "linux" texto.txt       # Ignora maiúsculas/minúsculas
grep -n "senha" config.txt      # Mostra número da linha
grep -r "chave" /etc            # Busca recursivamente em diretórios
grep -v "ok" status.txt         # Exclui linhas com "ok"
```

---

### 🔹 Opções comuns

| Opção   | Descrição                                         |
|---------|---------------------------------------------------|
| `-i`    | Ignora maiúsculas/minúsculas                      |
| `-v`    | Inverte a busca (mostra linhas que **não** combinam) |
| `-n`    | Mostra número das linhas                          |
| `-r`    | Busca recursiva em diretórios                     |
| `-l`    | Mostra apenas os **nomes dos arquivos** que têm correspondência |
| `-c`    | Conta quantas linhas correspondem ao padrão       |
| `-w`    | Combina palavras inteiras                         |
| `-x`    | Combina linhas inteiras                           |
| `-A N`  | Mostra N linhas **após** a linha correspondente   |
| `-B N`  | Mostra N linhas **antes** da linha correspondente |
| `-C N`  | Mostra N linhas **antes e depois**                |
| `--color` | Destaca as correspondências com cor             |

---

### 🔹 Expressões regulares com `grep`

- `.` → qualquer caractere  
- `^` → início da linha  
- `$` → fim da linha  
- `[]` → conjunto de caracteres  
- `.*` → qualquer sequência  
- `\` → escape para caracteres especiais  

```bash
grep "^Erro" log.txt           # Linhas que começam com "Erro"
grep "fim$" log.txt            # Linhas que terminam com "fim"
grep "[0-9]" relatorio.txt     # Linhas com números
```

---

### 🔹 Combinando com outros comandos

```bash
dmesg | grep usb
ps aux | grep firefox
cat arquivo.txt | grep -i "palavra"
```

---


## 🧾 Comando `head`

O comando `head` exibe as **primeiras linhas de um arquivo** (padrão: 10 linhas).

### 🔹 Sintaxe
```bash
head [opções] [arquivo]
```

### 🔹 Exemplos
```bash
head arquivo.txt                # Mostra as 10 primeiras linhas
head -n 5 arquivo.txt           # Mostra as 5 primeiras linhas
```

---

## 📄 Comando `tail`

O comando `tail` exibe as **últimas linhas de um arquivo** (padrão: 10 linhas).

### 🔹 Sintaxe
```bash
tail [opções] [arquivo]
```

### 🔹 Exemplos
```bash
tail arquivo.txt                # Mostra as 10 últimas linhas
tail -n 20 arquivo.txt          # Mostra as 20 últimas linhas
tail -f log.txt                 # Acompanha em tempo real (logs)
```

---
