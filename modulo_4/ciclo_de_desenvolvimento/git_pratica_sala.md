# Prática - Git e Controle de Versão

## O que deve ser feito?

1. Criar um repositório local
2. Crie um commit adicionando o arquivo test.py nesse repositório numa branch a parte
3. Volte para a main e adicione um arquivo app.py (commit)
4. Traga as mudanças da main para sua branch criada no passo 2
5. Adicione outro arquivo another_test.py nessa branch e commit
6. Traga as mudanças feitas na branch criada para a main


##  Resolução [Spoiler]

### Configuração Inicial:

Certifique-se de ter o Git instalado em sua máquina.
Configure seu nome de usuário e endereço de e-mail no Git.

```bash
git config --global user.name "Fulano da Silva"
git config --global user.email fulanodasilva.git@gmail.com
```

### Criação do Repositório:

Crie um diretório para o projeto e navegue até ele pelo terminal.

Inicialize um repositório Git.

```bash
git init
```

### Adicionando arquivos em uma branch separada

Crie um arquivo chamado test.py e adicione algum conteúdo a ele.

Criação de uma Branch:

```bash
git checkout -b feature/teste
```

Commit o arquivo recem criado na Nova Branch:

```bash
git add .
git commit -m "Adiciona app.py e test.py".
# ou
git commit -a -m "Adiciona app.py test.py"
```

### Adicionando arquivos no main

Volta à Branch Principal:

```bash
git checkout main
```

Crie e adicione conteúdo ao arquivo app.py na branch principal.
Faça um commit das alterações.

### Merge main -> branch

Volte à branch feature/teste usando o comando

```bash
git checkout feature/teste
```
Realize o merge da branch principal na branch de funcionalidade usando o comando

```bash
git merge main
```

Resolva possíveis conflitos, se houver.

## Adiciona mais arquivos na branch

Adicione mais códigos ao arquivo another_test.py na branch de funcionalidade.
Faça um commit das alterações.

## Merge branch -> main

Volte à branch principal e faça o merge final da funcionalidade.

```bash
git checkout main
git merge feature/teste
```

Observe a estrutura do seu repositório, incluindo commits e branches
