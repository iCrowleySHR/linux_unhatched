# Linux Unhatched
The Cisco's course about on the OS Linux.

---
# Comando `ls`

O comando `ls` (list) é utilizado em sistemas Unix e Linux para listar o conteúdo de diretórios. Ele exibe arquivos e pastas presentes no diretório atual ou em um caminho especificado.

## Sintaxe

```bash
ls [opcoes] [caminho]
```

Se nenhum caminho for especificado, o `ls` exibirá o conteúdo do diretório atual.

## Opções Comuns

- `ls -l` → Exibe os arquivos em formato de lista detalhada.
- `ls -a` → Mostra arquivos ocultos (arquivos que começam com `.`).
- `ls -h` → Exibe tamanhos de arquivos em formato legível para humanos (usado com `-l`).
- `ls -r` → Lista os arquivos em ordem reversa.
- `ls -t` → Organiza os arquivos por data de modificação.
- `ls -R` → Lista o conteúdo de diretórios recursivamente.

# Comando `pwd`

O comando `pwd` (print working directory) é utilizado em sistemas Unix e Linux para exibir o caminho absoluto do diretório atual em que o usuário se encontra.

## Sintaxe

```bash
pwd
```

Esse comando não requer argumentos e retorna o caminho completo do diretório atual.

# Comando `su`

O comando `su`, é utilizado para usuário ter acesso ao shell como administrador, dando permissões que o shell comum não executa.
Esse comando vai pedir senha para concluir o que foi ordenado.

## Sintaxe

```bash
su
```

Para sair do shell de root, basta você utilizar esse comando:
```bash
exit
```

# Comando `sudo`

O comando `sudo` permite que um usuário execute um comando como outro usuário sem criar um novo shell. Em vez disso, para executar um comando com privilégios administrativos, use-o como um argumento para o comando `sudo`.

## Sintaxe

```bash
sudo [OPTIONS] comando
```
# Permissões no Linux

No Linux, as permissões controlam quem pode ler, escrever e executar arquivos e diretórios. Elas são representadas por três grupos: dono, grupo e outros. Cada grupo tem três tipos de permissões:

- **r (read):** Permissão de leitura
- **w (write):** Permissão de escrita
- **x (execute):** Permissão de execução

Para visualizar as permissões de um arquivo ou diretório, use:
```bash
ls -l
```

### Exemplo de saída do comando `ls -l`:
```bash
-rwxr-xr-- 1 usuario grupo 1024 Mar 16 12:00 script.sh
```
Explicação:
- `-rwxr-xr--` → Representação das permissões:
  - `-` → Arquivo comum (se fosse `d`, seria um diretório)
  - `rwx` → Permissões do dono (leitura, escrita e execução)
  - `r-x` → Permissões do grupo (leitura e execução, sem escrita)
  - `r--` → Permissões para outros (apenas leitura)
- `1` → Número de links para o arquivo
- `usuario` → Dono do arquivo
- `grupo` → Grupo ao qual o arquivo pertence
- `1024` → Tamanho do arquivo em bytes
- `Mar 16 12:00` → Data e hora da última modificação
- `script.sh` → Nome do arquivo

### Tabela de permissões no Linux

Cada permissão é representada por um número octal:

| Valor | Permissões | Significado |
|--------|------------|---------------------------|
| 0 | --- | Nenhuma permissão |
| 1 | --x | Somente execução |
| 2 | -w- | Somente escrita |
| 3 | -wx | Escrita e execução |
| 4 | r-- | Somente leitura |
| 5 | r-x | Leitura e execução |
| 6 | rw- | Leitura e escrita |
| 7 | rwx | Leitura, escrita e execução |

### Exemplos de permissões comuns:
- **777** → Todos têm **leitura, escrita e execução** (`rwxrwxrwx`).
- **755** → Dono tem **tudo**, grupo e outros têm **leitura e execução** (`rwxr-xr-x`).
- **644** → Dono tem **leitura e escrita**, grupo e outros têm apenas **leitura** (`rw-r--r--`).
- **600** → Somente o dono pode **ler e escrever** (`rw-------`).

Para modificar permissões, utilize o comando `chmod`:
```bash
chmod 755 arquivo
```
Isso concede permissões de leitura e execução para todos, e de escrita apenas para o dono.






