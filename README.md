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
