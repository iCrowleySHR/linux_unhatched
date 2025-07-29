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


## ✏️ Comando `nano`

O `nano` é um **editor de texto simples e interativo** no terminal, usado para criar e editar arquivos diretamente pela linha de comando.

### 🔹 Sintaxe
```bash
nano [arquivo]
```

### 🔹 Exemplos
```bash
nano texto.txt              # Abre (ou cria) o arquivo texto.txt
nano /etc/hosts             # Edita um arquivo de configuração (precisa de sudo)
```

---

### 🔹 Atalhos úteis dentro do `nano`

| Atalho            | Ação                                |
|------------------|--------------------------------------|
| `CTRL + O`       | Salvar (gravar) o arquivo            |
| `CTRL + X`       | Sair do editor                       |
| `CTRL + G`       | Ajuda                               |
| `CTRL + K`       | Cortar linha                        |
| `CTRL + U`       | Colar linha                         |
| `CTRL + W`       | Procurar no texto                    |
| `CTRL + \`       | Substituir texto                     |
| `CTRL + C`       | Mostrar posição do cursor            |
| `ALT + U`        | Desfazer última ação (versões mais recentes) |

⚠️ O `nano` salva automaticamente o arquivo com `CTRL + O`. Ele pedirá confirmação do nome antes de salvar.

---

### 🔹 Dica
Se o arquivo precisar de permissões de root:
```bash
sudo nano /etc/hosts
```
---

## 🧠 Comando `ps`

O comando `ps` exibe informações sobre os **processos em execução** no sistema.

### 🔹 Sintaxe
```bash
ps [opções]
```

### 🔹 Exemplos
```bash
ps                      # Mostra processos do terminal atual
ps -e                   # Lista todos os processos do sistema
ps -ef                  # Formato completo com detalhes
ps aux                 # Exibe todos os processos em formato BSD
ps -u usuario           # Filtra por usuário
```

### 🔹 Explicação dos campos comuns
- `PID` → ID do processo  
- `TTY` → Terminal associado  
- `TIME` → Tempo de CPU usado  
- `CMD` → Comando que iniciou o processo

---

## 🔎 Comando `pgrep`

O `pgrep` é usado para **procurar o PID de processos** com base no nome.

### 🔹 Sintaxe
```bash
pgrep [opções] nome
```

### 🔹 Exemplos
```bash
pgrep firefox             # Mostra PIDs do processo "firefox"
pgrep -l ssh              # Mostra PIDs com nomes (l = list)
pgrep -u usuario          # Filtra por usuário
```

---

## 🌳 Comando `pstree`

Exibe os processos em execução como uma **árvore hierárquica**, mostrando quais processos foram iniciados por outros.

### 🔹 Sintaxe
```bash
pstree [opções]
```

### 🔹 Exemplos
```bash
pstree                   # Mostra a árvore de processos
pstree -p                # Mostra PIDs
pstree -u                # Mostra usuários dos processos
pstree nome              # Filtra por nome do processo
```

---

## 🔗 Operador Pipe (`|`)

O **pipe** (`|`) é usado para **encaminhar a saída de um comando como entrada para outro comando**, permitindo criar fluxos de processamento no terminal.

### 🔹 Sintaxe
```bash
comando1 | comando2
```

### 🔹 Exemplos
```bash
ps aux | grep apache          # Procura por "apache" nos processos
cat arquivo.txt | sort        # Ordena o conteúdo do arquivo
dmesg | less                  # Pagina a saída do dmesg
ls -l | wc -l                 # Conta quantas linhas (arquivos) há
```

O pipe é uma das funcionalidades mais poderosas do shell, permitindo **combinar comandos para criar filtros e relatórios personalizados**.

---


## 💀 Comando `kill`

O comando `kill` envia **sinais a processos**, geralmente para encerrá-los.

### 🔹 Sintaxe
```bash
kill [sinal] PID
```

### 🔹 Exemplos
```bash
kill 1234                  # Envia o sinal padrão (TERM) ao processo 1234
kill -9 1234               # Envia o sinal SIGKILL (encerra imediatamente)
kill -15 1234              # Envia o sinal SIGTERM (encerra educadamente)
```

### 🔹 Sinais comuns
| Sinal | Nome     | Ação                        |
|-------|----------|-----------------------------|
| `1`   | SIGHUP   | Reinicia o processo         |
| `9`   | SIGKILL  | Encerra imediatamente       |
| `15`  | SIGTERM  | Encerra normalmente (padrão)|

---

## 🔫 Comando `pkill`

O comando `pkill` termina processos **com base no nome**, sem precisar do PID.

### 🔹 Sintaxe
```bash
pkill [opções] nome
```

### 🔹 Exemplos
```bash
pkill firefox             # Encerra todos os processos "firefox"
pkill -u usuario          # Encerra processos do usuário especificado
pkill -f "comando longo"  # Combina com a linha de comando completa
```

---

## ⚰️ Comando `killall`

O comando `killall` encerra **todos os processos com um nome exato**.

### 🔹 Sintaxe
```bash
killall [opções] nome
```

### 🔹 Exemplos
```bash
killall firefox           # Encerra todos os processos "firefox"
killall -u usuario        # Encerra todos os processos de um usuário
killall -q nome           # Silencioso (não exibe erro se não encontrar)
```

---

### 🔐 Importante:
- Encerrar processos críticos pode travar o sistema.
- Pode ser necessário usar `sudo` para encerrar processos de outros usuários.

---

## ⚙️ Comando `systemctl`

O comando `systemctl` é utilizado para **gerenciar serviços, unidades e o estado do sistema** no Linux que utiliza o `systemd` (como Ubuntu, Debian, Fedora e derivados).

### 🔹 Sintaxe
```bash
systemctl [opção] [serviço]
```

---

### 🔹 Comandos mais comuns

| Comando                         | Ação                                           |
|----------------------------------|------------------------------------------------|
| `systemctl status`              | Mostra o status geral do `systemd`            |
| `systemctl status nome.service` | Mostra o status de um serviço específico       |
| `systemctl start nome.service`  | Inicia o serviço                               |
| `systemctl stop nome.service`   | Para o serviço                                 |
| `systemctl restart nome.service`| Reinicia o serviço                             |
| `systemctl reload nome.service` | Recarrega as configurações sem reiniciar       |
| `systemctl enable nome.service` | Ativa o serviço para iniciar com o sistema     |
| `systemctl disable nome.service`| Desativa o serviço no boot                     |
| `systemctl is-active nome.service` | Verifica se o serviço está ativo           |
| `systemctl list-units --type=service` | Lista todos os serviços carregados       |

---

### 🔹 Exemplos
```bash
systemctl status apache2.service          # Ver status do Apache
systemctl start apache2.service           # Inicia o Apache
systemctl stop apache2.service            # Para o Apache
systemctl restart sshd.service            # Reinicia o SSH
systemctl enable nginx.service            # Ativa o Nginx na inicialização
systemctl disable bluetooth.service       # Desativa o Bluetooth no boot
```

---

### 🔹 Dica
Para rodar a maioria desses comandos, é necessário usar `sudo`:
```bash
sudo systemctl restart nome.service
```

---

## 🧩 Foreground e Background no Terminal

No Linux, comandos podem ser executados em **foreground** (primeiro plano) ou **background** (segundo plano).

---

### 🔹 Foreground (primeiro plano)

É o modo padrão: o terminal **fica ocupado** até o comando terminar.

```bash
firefox                # Executa em foreground (bloqueia o terminal)
```

---

### 🔹 Background (segundo plano)

Executa o processo em segundo plano, **liberando o terminal** para outros comandos.

```bash
firefox &              # Inicia o Firefox em background
```

A saída mostra o número do job e o PID:
```bash
[1] 12345
```

---

## 📊 Comando `top`

O `top` mostra **processos em tempo real**, consumo de CPU, RAM e uso do sistema.

### 🔹 Sintaxe
```bash
top
```

### 🔹 Navegação
- `q` → sair
- `P` → ordenar por uso de CPU
- `M` → ordenar por uso de memória
- `k` → matar processo (inserir PID)
- `h` → ajuda

### 🔹 Exemplo
```bash
top
```

Ideal para **monitorar o desempenho do sistema** em tempo real.

---

## 🧠 Comando `free`

Mostra o **uso da memória RAM e SWAP**.

### 🔹 Sintaxe
```bash
free [opções]
```

### 🔹 Opções comuns
- `-h` → Exibe tamanhos legíveis (MB, GB)
- `-m` → Mostra em megabytes
- `-g` → Mostra em gigabytes

### 🔹 Exemplo
```bash
free -h
```

Saída mostra:
- Memória total
- Memória usada
- Memória livre
- Buffer/cache
- SWAP

---

## 💻 Comando `uname`

Mostra **informações sobre o sistema operacional e kernel**.

### 🔹 Sintaxe
```bash
uname [opções]
```

### 🔹 Opções úteis
- `-a` → Todas as informações
- `-r` → Versão do kernel
- `-s` → Nome do sistema
- `-m` → Arquitetura da máquina

### 🔹 Exemplo
```bash
uname -a
```

Saída inclui: nome do SO, hostname, versão do kernel, data de compilação e arquitetura.

---

## ⏱️ Comando `uptime`

Exibe **há quanto tempo o sistema está ligado**, usuários ativos e carga do sistema.

### 🔹 Sintaxe
```bash
uptime
```

### 🔹 Exemplo
```bash
uptime
```

Saída exemplo:
```
15:32:11 up 3 days,  4:12,  2 users,  load average: 0.15, 0.20, 0.25
```

- `up` → tempo desde o último boot
- `users` → número de usuários logados
- `load average` → carga média do sistema (1, 5 e 15 min)

---

## 💾 Comando `df`

O comando `df` mostra o **uso de espaço em disco por partição**.

### 🔹 Sintaxe
```bash
df [opções]
```

### 🔹 Opções úteis
- `-h` → Tamanhos legíveis (MB, GB)
- `-T` → Mostra tipo de sistema de arquivos
- `-x tipo` → Exclui tipos (ex: `tmpfs`)

### 🔹 Exemplo
```bash
df -h
```

Saída mostra:
- Sistema de arquivos
- Tamanho total
- Usado
- Disponível
- Ponto de montagem

---

## 📦 Comando `apt-get`

O comando `apt-get` é usado para **gerenciar pacotes** em distribuições baseadas no Debian, como **Ubuntu, Kali, Mint**, entre outras.
Não precisa de SUDO caso você esteja como root.

### 🔹 Sintaxe
```bash
sudo apt-get [opção] [pacote]
```

### 🔹 Principais comandos

| Comando                        | Ação                                                        |
|-------------------------------|-------------------------------------------------------------|
| `sudo apt-get update`         | Atualiza a lista de pacotes disponíveis (não instala nada)  |
| `sudo apt-get upgrade`        | Atualiza todos os pacotes instalados para as versões mais recentes |
| `sudo apt-get install nome`   | Instala um pacote                                            |
| `sudo apt-get remove nome`    | Remove um pacote (mantém configurações)                     |
| `sudo apt-get purge nome`     | Remove um pacote e suas configurações                       |
| `sudo apt-get autoremove`     | Remove pacotes instalados automaticamente e não utilizados  |
| `sudo apt-get clean`          | Limpa arquivos de cache                                      |
| `sudo apt-get dist-upgrade`   | Atualiza pacotes e gerencia dependências (avançado)         |

---

### 🔹 Exemplos
```bash
sudo apt-get update
sudo apt-get install curl
sudo apt-get remove gimp
sudo apt-get upgrade
sudo apt-get autoremove
```

---

### 🔹 Dica
Para quem prefere uma interface mais moderna e amigável:
```bash
sudo apt install nome
```

Esse comando (`apt`) é mais recente e recomendado para uso interativo. Já `apt-get` é ideal para scripts e automações.


---

## 📦 Comando `apt`

O comando `apt` é utilizado para **gerenciar pacotes** em sistemas baseados em **Debian**, como Ubuntu.

> ⚠️ `apt` é uma interface simplificada que combina funções de comandos mais antigos como `apt-get` e `apt-cache`.

---

### 🔹 Sintaxe
```bash
apt [opção] [pacote]
```

---

### 🔹 Comandos comuns

| Comando                          | Ação                                        |
|----------------------------------|---------------------------------------------|
| `sudo apt update`               | Atualiza a lista de pacotes disponíveis     |
| `sudo apt upgrade`              | Atualiza todos os pacotes instalados        |
| `sudo apt install nome`         | Instala um pacote                           |
| `sudo apt remove nome`          | Remove um pacote                            |
| `sudo apt purge nome`           | Remove pacote e arquivos de configuração    |
| `sudo apt autoremove`           | Remove dependências não utilizadas          |
| `sudo apt search termo`         | Busca pacotes com o termo informado         |
| `apt show nome`                 | Mostra informações sobre um pacote          |
| `apt list --installed`          | Lista pacotes instalados                    |

---

### 🔹 Exemplos

```bash
sudo apt update                      # Atualiza o repositório
sudo apt install vim                 # Instala o editor Vim
sudo apt remove firefox              # Remove o Firefox
sudo apt autoremove                  # Remove pacotes desnecessários
sudo apt search python               # Busca pacotes relacionados ao Python
```

---

### 🔹 Dica

- Sempre use `sudo` com `apt` para garantir permissões adequadas.
- Combine `update` e `upgrade` para manter o sistema atualizado:



## 📦 Comando `yum`

O `yum` (Yellowdog Updater Modified) é um **gerenciador de pacotes** usado em sistemas Linux baseados em **RPM** (Red Hat, CentOS, Fedora).

Ele permite instalar, atualizar, remover e pesquisar pacotes a partir de repositórios online.

### 🔹 Sintaxe
```bash
yum [opção] [pacote]
```

---

### 🔹 Comandos comuns

| Comando                            | Ação                                          |
|-----------------------------------|-----------------------------------------------|
| `yum install nome`                | Instala um pacote                             |
| `yum remove nome`                 | Remove um pacote                              |
| `yum update`                      | Atualiza todos os pacotes                     |
| `yum update nome`                 | Atualiza apenas o pacote especificado         |
| `yum search palavra`              | Busca pacotes relacionados à palavra-chave    |
| `yum info nome`                   | Exibe informações sobre um pacote             |
| `yum list installed`              | Lista pacotes instalados                      |
| `yum list available`              | Lista pacotes disponíveis                     |
| `yum clean all`                   | Limpa cache local do YUM                      |

---

### 🔹 Exemplos

```bash
yum install httpd                    # Instala o servidor Apache
yum remove nano                      # Remove o editor nano
yum update                          # Atualiza todos os pacotes
yum search mysql                    # Procura por pacotes relacionados ao MySQL
yum info nginx                      # Exibe informações do pacote Nginx
```

---

### 🔐 Dica
Você pode precisar usar `sudo`:
```bash
sudo yum install nome_do_pacote
```

---

### 🔁 Substituição pelo `dnf`

Em distribuições mais recentes como Fedora, o `yum` foi substituído por `dnf`:
```bash
dnf install nome_do_pacote
```

---

## 🔌 Desligar e Reiniciar o Sistema

No Linux, você pode desligar ou reiniciar o sistema usando comandos simples no terminal. Normalmente, é necessário ter permissões de superusuário (`sudo`).

---

### 🔹 Comando `shutdown`

Desliga ou reinicia o sistema com opções personalizadas.

#### 🔸 Sintaxe
```bash
shutdown [opções] [tempo] [mensagem]
```

#### 🔸 Exemplos
```bash
sudo shutdown now                # Desliga imediatamente
sudo shutdown -h now             # Desliga (halt) imediatamente
sudo shutdown -r now             # Reinicia imediatamente
sudo shutdown +10 "Salvando arquivos..."  # Desliga em 10 minutos com aviso
```

---

### 🔹 Comando `poweroff`

Desliga o sistema imediatamente.
```bash
sudo poweroff
```

---

### 🔹 Comando `reboot`

Reinicia o sistema.
```bash
sudo reboot
```

---

### 🔹 Comando `halt`

Interrompe o sistema (sem desligar a energia em alguns casos).
```bash
sudo halt
```

---

### 🕒 Cancelar desligamento agendado

Se um desligamento estiver agendado com `shutdown +tempo`, você pode cancelá-lo:
```bash
sudo shutdown -c
```

---

## 👤 Gerenciamento de Usuários no Linux

Esses comandos são usados para **criar, modificar, excluir e definir senhas de usuários**. Normalmente exigem permissões de superusuário (`sudo`).

---

## 🔑 Comando `passwd`

Altera a **senha de um usuário**.

### 🔹 Sintaxe
```bash
passwd [usuário]
```

### 🔹 Exemplos
```bash
passwd                        # Altera a senha do usuário atual
sudo passwd gustavo           # Altera a senha do usuário "gustavo"
```

Você será solicitado a digitar e confirmar a nova senha.

---

## ➕ Comando `useradd`

Cria um **novo usuário no sistema**.

### 🔹 Sintaxe
```bash
useradd [opções] nome_usuario
```

### 🔹 Exemplos
```bash
sudo useradd joao                       # Cria o usuário "joao"
sudo useradd -m maria                   # Cria o usuário "maria" com diretório home
sudo useradd -m -s /bin/bash ana        # Cria com shell bash
```

### 🔹 Opções comuns
- `-m` → Cria diretório `/home/nome`
- `-s` → Define o shell padrão
- `-d` → Define o diretório home
- `-G` → Adiciona o usuário a grupos extras

---
---

## ➕ Comando `adduser`

O comando `adduser` é uma **ferramenta interativa para adicionar usuários** ao sistema. Ele é mais amigável do que `useradd`, pois cria automaticamente o diretório home, define permissões padrão e solicita senha.

> ⚠️ Em muitas distribuições, `adduser` é um **script que usa `useradd` por trás**, mas com mais facilidades.

---

### 🔹 Sintaxe
```bash
adduser nome_do_usuario
```

---

### 🔹 Exemplo
```bash
sudo adduser joao
```

O sistema perguntará:
- Nova senha
- Confirmação da senha
- Nome completo (opcional)
- Informações adicionais (opcional)

---

### 🔹 Comportamento do `adduser`
- Cria o diretório `/home/joao`
- Define permissões padrão
- Copia arquivos padrão de `/etc/skel`
- Solicita senha
- Cria grupo com o mesmo nome do usuário

---

### 🔹 Adicionar a grupos (ex: sudo)

```bash
sudo adduser joao sudo
```

> Adiciona o usuário "joao" ao grupo `sudo`, permitindo acesso administrativo.

---

### 🔹 Dica

- Em sistemas baseados em Debian/Ubuntu, use `adduser` para uma criação mais simplificada.
- Em sistemas baseados em RHEL (Red Hat/CentOS), geralmente apenas `useradd` está disponível por padrão.

---


## 👥 Comando `groupadd`

O comando `groupadd` é usado para **criar novos grupos de usuários** no sistema Linux.

---

### 🔹 Sintaxe
```bash
groupadd [opções] nome_do_grupo
```

---

### 🔹 Exemplos

```bash
sudo groupadd desenvolvedores         # Cria um grupo chamado "desenvolvedores"
sudo groupadd -g 1005 suporte         # Cria o grupo "suporte" com GID específico
```

---

### 🔹 Opções comuns

| Opção    | Descrição                                  |
|----------|--------------------------------------------|
| `-g`     | Define o GID (Group ID) do grupo           |
| `-f`     | Não gera erro se o grupo já existir        |
| `-K`     | Define configurações específicas temporárias|

---

### 🔹 Verificar grupos existentes

```bash
cat /etc/group             # Lista todos os grupos do sistema
```

---

### 🔹 Adicionar um usuário a um grupo

```bash
sudo usermod -aG grupo usuario
```

Exemplo:
```bash
sudo usermod -aG desenvolvedores joao
```

---

### 🔐 Dica

- Para aplicar grupos recém atribuídos, o usuário pode precisar sair e entrar novamente na sessão ou usar:
```bash
newgrp nome_do_grupo
```

---


## 🧾 Comando `usermod`

Modifica um **usuário existente**.

### 🔹 Sintaxe
```bash
usermod [opções] nome_usuario
```

### 🔹 Exemplos
```bash
sudo usermod -s /bin/zsh joao           # Muda o shell padrão para zsh
sudo usermod -aG sudo joao              # Adiciona "joao" ao grupo sudo
sudo usermod -d /novo/home joao         # Muda o diretório home
```

### 🔹 Opções comuns
- `-s` → Mudar o shell padrão
- `-d` → Mudar diretório home
- `-G` → Grupos adicionais
- `-a` → Acrescenta (usar com `-G`)

⚠️ Ao usar `-G`, sempre combine com `-a` para **não remover os grupos existentes**.

---

## ❌ Comando `userdel`

Remove um **usuário do sistema**.

### 🔹 Sintaxe
```bash
userdel [opções] nome_usuario
```

### 🔹 Exemplos
```bash
sudo userdel joao                     # Remove o usuário (sem apagar /home)
sudo userdel -r maria                 # Remove o usuário e seu diretório home
```

### 🔹 Opção
- `-r` → Remove o diretório home e arquivos do usuário

⚠️ Use com cuidado, especialmente com `-r`, pois os arquivos do usuário serão apagados.

---

## ✍️ Editor de Texto `vi` (ou `vim`)

O `vi` é um dos editores de texto mais antigos e poderosos no Linux. O `vim` (Vi IMproved) é uma versão aprimorada, geralmente já instalada nos sistemas.

---

### 🔹 Abrir arquivo com `vi`

```bash
vi nome_do_arquivo
```

---

### 🔹 Modos do `vi`

| Modo         | Função                                         |
|--------------|------------------------------------------------|
| **Normal**   | Navegação e comandos (modo padrão ao abrir)    |
| **Inserção** | Digitar e editar texto                         |
| **Visual**   | Selecionar texto                               |
| **Linha de comando** | Executar comandos como salvar e sair |

---

### 🔹 Comandos principais

#### ▶️ Entrar no modo de inserção
(No modo normal, pressione uma das teclas abaixo)

| Comando | Ação                         |
|---------|------------------------------|
| `i`     | Inserir antes do cursor      |
| `a`     | Inserir após o cursor        |
| `o`     | Nova linha abaixo            |
| `O`     | Nova linha acima             |

---

#### 💾 Salvar e sair (modo comando)
(Pressione `ESC` para sair da inserção, depois digite:)

| Comando    | Ação                        |
|------------|-----------------------------|
| `:w`       | Salva o arquivo             |
| `:q`       | Sai (só se não houver alterações) |
| `:q!`      | Sai sem salvar              |
| `:wq` ou `ZZ` | Salva e sai             |

---

#### 🔍 Navegação no modo normal

| Tecla      | Ação                         |
|------------|------------------------------|
| `h`, `j`, `k`, `l` | Esquerda, baixo, cima, direita |
| `0` / `^`  | Início da linha              |
| `$`        | Fim da linha                 |
| `G`        | Vai para o fim do arquivo    |
| `gg`       | Vai para o início do arquivo |
| `:` + número | Vai para linha específica (`:10`) |

---

#### ✂️ Edição e manipulação

| Comando | Ação                          |
|---------|-------------------------------|
| `dd`    | Apaga (corta) linha           |
| `yy`    | Copia linha                   |
| `p`     | Cola abaixo do cursor         |
| `x`     | Apaga caractere               |
| `u`     | Desfaz                        |
| `Ctrl + r` | Refaz                     |

---

### 🧠 Dica

Para iniciantes, o `vim` pode ajudar com mensagens e realce:
```bash
vim nome_do_arquivo
```

Se não tiver o `vim`, instale com:
```bash
sudo apt install vim       # Debian/Ubuntu
sudo yum install vim       # RHEL/CentOS
```

---

## 📜 Comando `history`

O comando `history` exibe uma **lista dos comandos digitados anteriormente** no terminal, com numeração sequencial.

### 🔹 Sintaxe
```bash
history [número]
```

---

### 🔹 Exemplos

```bash
history               # Mostra todo o histórico do terminal
history 20            # Mostra os últimos 20 comandos
```

---

### 🔹 Reutilizar comandos do histórico

| Comando             | Ação                                        |
|---------------------|---------------------------------------------|
| `!n`               | Executa o comando de número `n`             |
| `!!`               | Executa o último comando novamente          |
| `!palavra`         | Executa o último comando que começa com "palavra" |
| `!sudo`            | Executa o último comando iniciado com "sudo" |

---

### 🔹 Apagar o histórico

```bash
history -c           # Limpa todo o histórico da sessão atual
```

> ⚠️ Isso não apaga o arquivo `.bash_history` no disco.

---

### 🔹 Arquivo de histórico

- O histórico é salvo em:
```bash
~/.bash_history       # Para usuários usando bash
```

- Para salvar o histórico manualmente:
```bash
history -w
```

---

### 🔐 Dica de segurança

Evite digitar senhas diretamente em comandos, pois elas podem ficar salvas no histórico.

---

## 📄 Comando `touch`

O comando `touch` é utilizado para **criar arquivos vazios** ou **atualizar a data e hora de modificação** de arquivos existentes.

### 🔹 Sintaxe
```bash
touch [opções] nome_do_arquivo
```

---

### 🔹 Exemplos

```bash
touch novo_arquivo.txt            # Cria um arquivo vazio
touch arquivo1.txt arquivo2.txt   # Cria vários arquivos de uma vez
touch ~/documentos/nota.txt       # Cria em um caminho específico
```

Se o arquivo já existir, o `touch` apenas **atualiza o timestamp de modificação** (data e hora).

---

### 🔹 Opções úteis

| Opção     | Descrição                                    |
|-----------|----------------------------------------------|
| `-c`      | Não cria arquivo se ele não existir          |
| `-t` [[AAAAMMDDhhmm]] | Define uma data/hora específica |
| `-a`      | Atualiza apenas o tempo de acesso            |
| `-m`      | Atualiza apenas o tempo de modificação       |

---

### 🔹 Exemplo com data/hora personalizada

```bash
touch -t 202507251200 meu_arquivo.txt
```
> Define a data de modificação como 25/07/2025 às 12:00.

---

### 🔹 Dica

O `touch` é muito usado para:
- Criar arquivos rapidamente para testes
- Atualizar timestamps em scripts
- Garantir que um arquivo exista antes de escrever nele

---
---

## 🌐 Comando `wget`

O `wget` é um utilitário de linha de comando usado para **baixar arquivos da internet** via HTTP, HTTPS ou FTP.

---

### 🔹 Sintaxe
```bash
wget [opções] URL
```

---

### 🔹 Exemplos

```bash
wget https://exemplo.com/arquivo.zip              # Baixa o arquivo
wget -O novo_nome.zip https://exemplo.com/zip     # Salva com nome personalizado
wget -c https://exemplo.com/video.mp4             # Continua download interrompido
wget -P /home/usuario/downloads URL               # Salva em um diretório específico
```

---

### 🔹 Opções úteis

| Opção         | Descrição                                        |
|---------------|--------------------------------------------------|
| `-O nome`     | Salva o arquivo com nome personalizado           |
| `-c`          | Continua download interrompido                   |
| `-P caminho`  | Define o diretório onde o arquivo será salvo     |
| `--limit-rate=200k` | Limita velocidade de download              |
| `-r`          | Faz download recursivo (para sites)              |
| `--no-check-certificate` | Ignora erro de certificado SSL       |

---

### 🔹 Exemplo avançado: baixar site
```bash
wget -r -np -k http://exemplo.com
```
- `-r` → Recursivo  
- `-np` → Não sobe para diretórios pai  
- `-k` → Converte links para navegação offline

---

### 🔐 Dica

Se `wget` não estiver instalado:
```bash
sudo apt install wget       # Debian/Ubuntu
sudo yum install wget       # Red Hat/CentOS
```

---


## 👽 Comando `alien`

O comando `alien` é utilizado para **converter pacotes entre diferentes formatos**, como `.rpm` (Red Hat) e `.deb` (Debian/Ubuntu).

---

### 🔹 Sintaxe
```bash
sudo alien [opções] pacote
```

---

### 🔹 Exemplos

```bash
sudo alien pacote.rpm                     # Converte .rpm para .deb
sudo alien -d pacote.rpm                  # Converte para .deb explicitamente
sudo alien -r pacote.deb                  # Converte .deb para .rpm
sudo alien -k pacote.rpm                  # Mantém o número da versão original
sudo alien -i pacote.rpm                  # Converte e instala o pacote
```

---

### 🔹 Opções úteis

| Opção    | Descrição                                        |
|----------|--------------------------------------------------|
| `-d`     | Gera um pacote `.deb`                            |
| `-r`     | Gera um pacote `.rpm`                            |
| `-k`     | Mantém a versão original                         |
| `-i`     | Instala o pacote após conversão                  |
| `--scripts` | Mantém scripts de pós-instalação (com cuidado) |

---

### 🔹 Instalação do `alien`

Se não estiver instalado:
```bash
sudo apt install alien         # Debian/Ubuntu
```

---

### ⚠️ Atenção

- Nem todos os pacotes convertidos funcionam perfeitamente.
- Teste primeiro em ambientes não críticos.
- Sempre prefira pacotes nativos da sua distribuição.

---

## 🔍 Comando `locate`

O `locate` é um comando usado para buscar arquivos e diretórios de forma rápida no sistema Linux. Ele consulta um **banco de dados indexado** com os caminhos dos arquivos, o que torna a busca quase instantânea.

#### 🧪 Uso básico

```bash
locate nome_do_arquivo
```

#### ⚠️ Observação

Se o `locate` não encontrar arquivos recém-criados, atualize o banco de dados com:

```bash
sudo updatedb
```

#### 💡 Exemplo

```bash
locate nginx.conf
```
---

## 💽 Comando `fdisk`

O `fdisk` é um utilitário de linha de comando usado para **criar, visualizar, modificar ou excluir partições** em discos no Linux.

> ⚠️ É uma ferramenta poderosa que requer permissões de superusuário e pode apagar dados se usada incorretamente.

#### 🧪 Ver partições de um disco

```bash
sudo fdisk -l
```

Exibe a tabela de partições de todos os discos detectados pelo sistema.

#### 💡 Editar partições de um disco específico

```bash
sudo fdisk /dev/sdX
```

Substitua `sdX` pelo identificador do disco (ex: `sda`, `sdb`).

Dentro do modo interativo, alguns comandos úteis são:
- `m`: ajuda
- `p`: listar partições
- `d`: deletar partição
- `n`: nova partição
- `w`: escrever alterações no disco

> 🛑 Atenção: Alterações só são salvas após usar o comando `w`.

---

## 🧾 Comando `mkfs`

O `mkfs` (make filesystem) é usado para **formatar uma partição** ou disco com um sistema de arquivos no Linux.

> ⚠️ Cuidado: Este comando **apaga todos os dados** da partição selecionada.

#### 🧪 Uso básico

```bash
sudo mkfs -t tipo /dev/sdXn
```

- `-t tipo`: especifica o tipo de sistema de arquivos (ex: `ext4`, `vfat`, `ntfs`, etc.)
- `/dev/sdXn`: representa a partição (ex: `/dev/sda1`, `/dev/sdb2`)

#### 💡 Exemplos

Formatar uma partição como `ext4`:

```bash
sudo mkfs -t ext4 /dev/sdb1
```

Formatar uma partição como FAT32 (útil para pendrives):

```bash
sudo mkfs.vfat -F 32 /dev/sdb1
```

> 🛑 Atenção: Certifique-se de usar o caminho correto da partição para não apagar dados importantes.
