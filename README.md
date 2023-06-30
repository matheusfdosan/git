# Como usar o GIT

O GIT é um controle de versão, com o git podemos controlar as versões de um projeto, o controle vai registrar as alterações em um ou mais arquivos. Qualquer alteração feita no projeto, é possível guardá-la e criar versões com cada mundança feita no código, o que chamamos de **commit**.

## Tipos de Controles de versão

### Sistemas Locais

Os sistemas locais de controle de versão referem-se a uma técnicas, como duplicação de diretórios e renomeação de arquivos para cada alteração feita. Ou seja, trabalhamos com diretórios e arquivos armazenados em nosso computador.

Por Exemplo:

| Diretório de arquivos  |
| ---------------------- |
| Projeto_versao1_0.proj |
| Projeto_versao2_1.proj |
| Projeto_versao3_0.proj |
| Projeto_versao3_1.proj |
| Projeto_versao3_2.proj |

Era muito popular antigamente, para o controle de versão. Porém, não há como trabalhar com outros desenvolvedores em outros sistemas, pois isto é **local** apenas dentro da máquina, não é possível compartilhar essas alterações.

### Sistemas Centralizados

Basicamente, um sistema centralizado usa um único servidor que contém todos os arquivos. Então, vários desenvolvedores irão usar os arquivos a partir desse servidor central. Exemplos de sistemas centralizado: CVS, Subversion e Perforce.

Com o sistema centralizado, podemos trabalhar com outras pessoas, além de, os administradores terem o controle de quem pode fazer o que.

Mas, pelo lado ruim, se o servidor centralizado cair, ou se não tiver acesso a internet, durante esse momento ninguém poderá colaborar ou salvar as alterações do projeto. Se o HD do banco de dados central for corrompido, o trabalho será perdido.

> Sempre que todo o projeto esteja apenas em um único lugar, há uma chance de se perder tudo.

### Sistemas distribuídos

O sistema distribuído, une os dois mundos de sistemas locais e centrais, ou seja, os arquivos ficam tanto localmente quanto externamente, em um servidor.

Exemplos de sistemas distribuídos: GIT, Mercurial, Bazaar ou Darcs.

Basicamente, o projeto estará guardado localmente, e terá um clone guardado remotamente (servidor), uma forma de backup, além disso, qualquer alteração feita no projeto local, pode ser enviado ao projeto remoto, e assim, vice-versa.

Essa maneira de se usar também facilita na hora de trabalhar com colaboradores, pois, todos terão o projeto localmente, e caso o servidor morrer, os colaboradores terão um estado mais recente dos arquivos.

## Instalando e configurando o git

A partir desse [link](https://git-scm.com/downloads), baixe o Git. Depois de instalá-lo, vamos fazer as configurações.

Abra o **Git Bash**, um terminal do GIT, e digite os comandos:

- `git config --global user.name "Your Name"`
- `git config --global user.email "Your Email"`

Esses comandos atribuem variáveis de configuração como o nome e email de usuário. Isso é importante porque em cada commit essa informação será utilizada, e é carimbada de forma imutável nos commits que você começa a criar. Com o comando `git config --list`, é possível ver as configurações.

## Git help

Então, no terminal, quando digitamos `git help`, trará uma lista de comandos do Git, portanto, caso tenha esquecido algum comando, é possível digitar, `git help [comando]`, que o Git abrirá o manual de como usar tal comando.

## Iniciando um repositório

Para iniciar um projeto com GIT, vamos criar uma diretório, nessa diretório ficará todos os arquivos do projeto, depois vamos abrir o terminal e entrar na diretório que criamos, depois digitamos:

```bash
$ git init
```

O comando acima irá iniciar o nosso repositório GIT, ele cria uma pasta oculta nomeada de **.git**. Essa pasta guardará todo o histórico do projeto, todos os pontos na história, linhas do tempo, configurações e etc.

> Essa é uma pasta muito importante, não deve ser apagada, se não todos os pontos na história, linhas do tempo, configurações do projeto serão apagados.

### Primeiro commit

Depois de ter feito alguma alteração no projeto, seja criando um arquivo, editando ou removendo, o GIT já indentificou que há alguma modificação no projeto, e daí, podemos criar um ponto na história do projeto ou mais conhecido como **commit**:

```bash
$ git add .
```

Primeiramente, precisamos adicionar as mudanças para a área de preparação ou **staging area**. No comando acima, o ponto serve para referênciar que queremos adicionar todas mundanças para a staging area. Mas também é possível especificar qual arquivo ou pasta que pode ser adicionada:

```bash
$ git add [arquivo]
$ git add [pasta]

$ git add index.html script.js
# Adicionando dois arquivos de uma vez
$ git add ./styles index.html
# Adicionando uma pasta e um arquivo
$ git add *.css
# Adiciona todos os arquivos que tenham a extensão css
```

Caso tenha adicionado um arquivo ou pasta que não era para adicionar, é possível removê-lo utilizando o seguinte comando:

- `git rm -chached [arquivo/pasta]`

Podemos ver quais arquivos foram ou não foram adicionados com o comando: `git status` (usando antes do adicionar para a staging area)

E se quisermos ver as modificações mais detalhadamente, antes de adicionarmos para a staging area, usamos o `git diff`, que mostrará as mundaças feitas em cada arquivo.

Estando todas as mundanças preparadas, apenas criamos um ponto na história com o comando:

```bash
$ git commit -m "initial commit"
```

Nesse comando, o `-m` é um atalho para _message_, seguido do nome do commit entre aspas. Pois todo ponto na história precisa ter alguma descrição.

Podemos usar o comando `git commit -am "message"`, que vai adicionar todas as mundanção no _staging area_ e vai fazer o commit em seguida, uma maneira mais eficiente de se fazer commits.

Esse processo de `git add` e `git commit`, é um processo muito importante na hora de trabalhar em um repositório.

## Git log

Com o comando `git log`, podemos ter acesso a todos os commits do projeto. Por exemplo:

```
commit dc83b3419db255620c770bb87388837b17f3732a (HEAD -> master)
Author: Nome do Usuário <emaildousuario@email.com>
Date: Wed Jun 21 16:14:25 2023 -0300

  nome do commit
```

Todo commit tem uma hash um conjunto de 40 dígitos únicos, o que chamamos de SHA (Secure Hash Algorithm), o que torna o GIT mais seguro. Veremos isso mais para frente.

`(HEAD -> master)` A HEAD sempre vai apontar em qual linha do tempo (branch) nós estamos trabalhando, então, este commit foi feito na branch master.

Depois tem algumas informações como, nome e email do autor, data e hora do commit e o nome.

Contudo, também podemos fazer com que essas informação sejam menores, com a flag `--oneline` (uma linha):

```bash
$ git log --oneline
```

Vai mostrar os commits mais compactados:

```bash
b7ec2a7 (HEAD -> master) my techs
f253f4a my description
37b3841 initial commit
```

E também, tem como fazer uma pesquisa de commits:

- `git log --n 5`, pega os 5 últimos commits

- `git log --since=2023-10-01`, pega só os commits posteriores da data 01/Out/2023 (since = desde)

- `git log --until=2023-10-01`, pega os commits anteriores da data 01/Out/2023 (until = até)

- `git log --author=Matheus`, pega os commits filtrando pelo autor (isso vale se estiver trabalhando com outros desenvolvedores)

- `git log --grep="initial"`, utiliza expressão regular para buscar qualquer commit que tenha "initial" no nome.

## Git diff

Usamos o `git diff` para ver as modificações de forma mais detalhada. Mostrando as linhas deletadas e adicionadas em cada arquivo modificado.

Portanto, sabemos que o comando `git diff` mostra apenas as modificações que estão fora da staging area, ou seja, o que está no _working directory_. Mas também é possível ver as modificações dos arquivos que estão dentro da staging area, com o comando: `git diff --staged` ou `git diff --cached`.

E também, há um jeito mais simples de ver as alterações de forma ainda mais detalhada, mostrando apenas o que foi modificado no arquivo. Utilizando o comando: `git diff --color-words`.

## Git show

- `git show 2f9cd2`

O _git show_ mostra todas as alterações feitas em cada commit, passamos a hash para o comando e ele mostra todas as modificações feitas. E também funciona com a flag `--color-words`.

Mas também, podemos especificar o que queremos que o comando mostre:

```bash
$ git show f2g4t6 -- src/views/index.hbs
$ git show df3v58 -- public/*
# Mostra todas as modificações dessa pasta
$ git show ct34y6 -- README.md
```

## Conceitos

### Estágios do arquivo

Há três estados do arquivo dentro do git, o primeiro é quando nós iniciamos o repositório com `git init` ou `git clone` (caso queiramos copiar os arquivos de outro repositório), após isso, o git inicia um repositório local, fazendo com que nossos arquivos fiquem no diretório de trabalho (**Working Directory**). O segundo estado, é quando nós fazemos a adição dos arquivos para a staging area (**Staging Area**). E por fim, o terceiro estado é quando damos a confirmação (**commit**), criando um ponto na história.

> Resumindo, primeiro, há a criação do respositório, segundo, depois das mundanças feitas no repositório, mandamos essas alterações para a staging area, e por fim, criamos um ponto na história.

### Git Workflow

O workflow do git, basicamente, é o processo de criação e armazenamento de commits em uma branch.

Podemos criar commits que ficam guardados dentro da branch, que armazenará todos os commits em ordem cronológica. Logo, é possível voltar nos commits, para fazer alguma mundança ou outra coisa.

Vamos fazer uma analogia: pense na história de uma pessoa, essa história chamaremos de branch, e vamos pensar em cada ano que a pessoa viveu é um commit, contudo, o git é como se fosse uma máquina do tempo, permitindo voltar nos anos passados.

### Hash SHA-1

A cada commit que criamos, o git vai gerar uma **hash**, que converte os dados da nossa operação em um número, o que garante a integridade dos nossos dados. Essa hash é uma linha de 40 caracteres hexadecimais.

No caso do GIT, é utilizada a `Hash SHA1`, que significa secure hash algorithm (algoritmo de hash seguro), que embaralha determinado arquivo, imagem ou texto para que seja gerado um conjunto de caracteres identificadores, caracteres esses que possuem 40 dígitos hexadecimais.

Esses quarenta dígitos são sempre únicos. Se você pegar um texto enorme e passar ele por esse algoritmo, ele vai gerar esse conjunto de caracteres, se você alterar uma vírgula que seja desse texto, já será gerado outro conjunto.

Exemplo:

Criaremos uma pasta com um arquivo `texto.txt` dentro e abriremos essa pasta no bash e vamos digitar:

```bash
$ openssl sha1 texto.txt
```

Depois de pressionar Enter, mostrará isso:

```txt
SHA1(texto.txt) = *de6cd632324dc7b17290d5e62a2c4b96292422d5*
```

Aqui há um sistema SHA1, que contém 40 caracteres. Ao fazermos um commit para o github, geralmente nos é gerado um desses. Se nós fizermos alguma alteração nesse arquivo ou na pasta, um outro SHA1 é criado.

### HEAD

A **HEAD** é um ponteiro que indica a branch que estamos trabalhando. E por padrão, quando digitamos `git log` no bash, para vermos todos os commits feitos no projeto, podemos ver `(HEAD -> master)` ao lado da Hash, apontando o commit mais recente, ou seja, a **HEAD** além de apontar para a branch atual, também aponta para o último commit feito.

Isso é importante, pois quando estiver trabalhando com outros commits, e digitamos `git log`, vemos o commit em que estamos trabalhando.

## Tirando arquivos do Staging area

Caso tenha algum arquivo que esta no staging area, e deseja removê-lo, é possível utilizar o comando:

- `git restore --staged [nome do arquivo]`

```bash
$ git restore --staged README.md
$ git restore --staged index.html scripts/navbar.js
$ git restore --staged . # Tira todos os arquivos
```

Há também um outro código que faz a mesma coisa, um código antigo que também funciona:

- `git reset HEAD [nome do arquivo]`

## Desfazendo alterações com o GIT

Podemos voltar alterações que fizemos no código com o comando:

- `git restore [nome do arquivo]`

```bash
$ git restore index.html
$ git restore scripts/button.js styles/button.css
$ git restore . # Restaura tudo
```

Quando um arquivo é alterado, o git reconhece essa alteração, além de aparecer em vermelho, no **git status**. Portanto, para desfazer essa alteração, digite o comando acima, e o arquivo voltará como erra antes da alteração.

## Corrigindo a mensagem do último commit

Podemos fazer diversas correções, como renomear um commit:

```bash
$ git commit --amend -m "Mudar a mensagem"
# amend = corrigir, remendar
```

> Claro que, cada alteração feita no commit a sua HASH irá mudar.

## Recuperando arquivos de outros commits

- `git checkout HASH -- nomedoarquivo`

Basicamente, esse comando pode trazer arquivos de outros commits para o commit atual. É necessário o uso do `git log` antes, para podermos pegar os primeiros caracteres da HASH, e após isso, rodamos o comando. Por exemplo:

```bash
$ git checkout afac4a3 -- README.md
$ git checkout gf51302 -- styles/button.css
$ git checkout kcdca4c -- index.html
```

> Um detalhe, é que caso haja um arquivo com o mesmo nome e formato, esse arquivo será substituído por inteiro.

## Gitignore

é um arquivo utilizado para ignorar outros arquivos e pastas do nosso projeto, apenas abrimos o arquivo, e colocamos o nome do arquivo, pasta ou caminho. Um exemplo, quando iniciamos um projeto com Node.js, a pasta **node_modules** é muito grande, mas não precisa estar dentro de um ponto na história, então ela pode ser ignorada.

> Resumindo, se algum arquivo ou pasta estiver no _gitignore_, não aparecerá no _Working directory_
