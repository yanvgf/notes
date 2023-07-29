# Orientações para utilizar o git no VSCode

## Login

- GitLab

Antes de qualquer coisa, é necessário se conectar à sua conta do GitLab no VSCode. Para tal, deve-se criar um token (Personal Access Token) e utilizá-lo para se conectar ao VSCode. A conexão ao VSCode sem o token não permite que algumas funcionalidades sejam acessadas em repositórios privados. Mais orientações em: https://www.golinuxcloud.com/set-up-gitlab-with-visual-studio-code/

- GitHub

O login no GitHub é mais fácil: basta clicar no ícone de perfil no canto inferior esquerdo do VSCode e clicar na opção de fazer login na sua conta do GitHub.

## Trabalhando com repositório remoto

Ao trabalhar com repositórios remotos, é necessário, inicialmente, definir um diretório local onde você vai trabalhar com os arquivos que serão compartilhados. Esse diretório será a raiz do seu repositório local, que pode ser iniciado com o comando
```
git init
```

Criado o repositório local, é necessário pareá-lo com um repositório remoto. Para tal, usa-se:
```
git remote add origin <URL_DO_REPOSITORIO_REMOTO>
```
Esse comando rastreia um novo repositório remoto, apelidado "origin". A localização desse repositório é informada pelo seu URL (que não é simplesmente o URL da página do GitLab ou GitHub, mas sim o URL copiado do local específico da página destinado a isso).

A partir desse instante, pode-se seguir diversos caminhos

**1. Atualizar repositório local**

Se você deseja deixar seu repositório local em dia com o repositório remoto, basta usar o comando
```
git pull origin <NOME_DA_BRANCH>
```
Esse comando modifica os seus arquivos locais que estão diferentes dos arquivos do repositório remoto. No casso, isso é feito nos arquivos da branch especificada. Ou seja, se há uma branch "yanvgf" (e essa branch deve existir tanto local quanto remotamente), as mudanças serão realizadas nos arquivos dessa branch.

**2. Atualizar repositório remoto**

Para atualizar o repositório remoto com as mudanças feitas localmente, segue-se os seguintes passos:

- Inicialmente, adiciona-se os arquivos que se deseja modificar no remoto na área de preparação (staging area ou index):
```
git add <ARQUIVO_1> <PASTA_2/ARQUIVO_2> ...
```
Também pode ser interessante utilizar a flag **-A** na frente do git add, o que faz com que todos os arquivos (que n~so são ignorados) sejam adicionados à área de preparação.

- Em seguida, após revisar os arquivos da área de preparação, faz-se o commit dos arquivos para o repositório local (ou seja, inicialmente você altera os arquivos e em seguida salva eles naquele novo estado no repositório local):
```
git commit -am "MENSAGEM DE COMMIT"
```
A flag **-am** (-a -m) commita todos os arquivos que estão na zona de preparação (-a) e adiciona uma mensagem a esse commit (-m), que deve ser uma descrição concisa das mudanças realizadas.

- Por fim, atualizado o repositório local, atualiza-se o repositório remoto com as mudanças feitas:
```
git push origin <NOME_DA_BRANCH>
```
Esse comando segue a mesma lógica do git pull.

A seguir, algumas imagens úteis para o entendimento dos principais comandos do git:

![img1](../Imagens/git-data-transport.png)

![img2](../Imagens/git-visual.png)

## .gitignore

Uma parte importante do git é o arquivo .gitignore. Ele armazena regex em suas linhas e impede que o git adicione aos repositórios locais/remotos os arquivos e diretórios que caem na regex. Esse arquivo não é criado automaticamente, então cria-se o mesmo com:
```
touch .gitignore
```
Isso deve ser feito no diretório raiz do repositório local.

Por exemplo, se eu quero que o git ignore todos os arquivos com terminação .ipynb, eu adiciono ao .gitignore a linha 
```
*.ipynb
```

Uma funcionalidade interessante é ignorar todos os arquivos, menos alguns específicos. Isso pode ser feito inicialmente colocando "*" no .gitignore, que faz todos os arquivos serem ignorados, e em seguida colocando "!" antes dos arquivos ou diretórios que não se quer ignorar. Por exemplo,
```
# Ignorar tudo
* 

# Permitir que arquivos dentro de subdiretórios sejam não-ignorados
!*/

# Não ignorar arquivos do tipo .ipynb
!*.ipynb

# Não ignorar arquivos dentro da pasta Arquivos
!Arquivos/*
```

## requirements.txt

Uma boa prática de programação é criar um arquivo requirements.txt com todos os pacotes utilizados em uma implementação e suas versões para que outras pessoas possam replicar seus resultados. Para isso, faz-se:

```
conda list -e > requirements.txt
```

Isso lista todos os pacotes e suas versões (precisa ter o -e para as versões) e coloca essas informações no arquivo requirements.txt. Para instalar exatamente os mesmos pacotes que estão listados no arquivo, basta dar conda install nesse arquivo (as orientações para isso ficam na primeira linha do arquivo).
