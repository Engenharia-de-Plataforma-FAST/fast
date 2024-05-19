# Principais comandos e alguns exemplos

## Inicializando o repositório local

### init 

Inicia um repositório novo (local ou remoto). Basicamente, cria um diretório `.git` no diretóiro onde foi rodado o comando, que contém as informações necessárias para o git funcionar.

```bash
git init
```
Rodar este comando em um reposítorio já trackeado nao deve alterar nada.

[Documentaçao](https://git-scm.com/docs/git-init)

### clone
Copia o código de um repositório para o local, trazendo o histórico de commits e branches.
Neste caso estamos clonando o repositório de Romulos: https://github.com/RomulosDS/MyStuff
```bash
git clone git@github.com:RomulosDS/MyStuff.git
```

[Documentaçao](https://git-scm.com/docs/git-clone) 

## Commitando Arquivos

Estes seriam os comandos normalmente utilizados para commitar:

```bash
git add <caminho-do-arquivo> # ou . para todos os arquivos mudados
git commit -m "<Mensagem de commit>" # criar um commit no repo local
# ---- opcional
git push # mandar as mudanças para o repositório remoto
```

## Criando uma nova branch

```bash
git checkout -b <nome-da-branch> # cria uma nova branch local
# git commit ......

# Para dar push no repositório remoto:
git push --set-upstream origin <nome-da-branch>
```

## Receber as mudanças do repositório remoto

```bash
git pull # trás as mudanças remotas para o local
```

## Merge de branches:

```bash
git checkout <destino> # muda para a branch de destino
git merge <origem> # merge da branch origem na destion
```
## Logs

```bash
git log # log normal, com todas as informaçoes de cada commit

git log --oneline --decorate --graph --all # git bem formatado
```

## Links úteis:

* https://github.com/joshnh/Git-Commands/blob/master/READMEpt.md
* [Documentaçao oficial desses e de outros comandos](https://git-scm.com/docs) 
