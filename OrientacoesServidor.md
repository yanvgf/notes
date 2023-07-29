# Orientações para utilizar os servidores do LITC

Para rodar os códigos nos servidores do LITC, há dois procedimentos diferentes:

## 1. Jupyter Notebooks

Caso meu código seja um Jupyter Notebook, eu preciso definir as portas que serão utilizadas
para hostear o notebook. Isso é feito automaticamente quando eu entro no servidor utilizando
o comando a seguir:

```litc59not```

Acessando o servidor por esse comando, eu ainda preciso criar um ambiente para rodar o meu notebook. Isso é feito com o comando a seguir:

```bash jupyter_online.sh```

Feito isso, já deve ser possível rodar os meus códigos no servidor.

Caso não seja possível, é bom verificar se eu tenho algum processo do _anaconda_ rodando no servidor. Posso ver os meus processos com o comando:

```htop```

No _htop_, eu posso ordenar os processos por nome de usuário apertando F5. Ao encontrar um processo rodando no meu nome, dou F9 e Enter para matá-lo.

**É fundamental sempre matar todos os processos do anaconda no meu nome sempre que terminar de usar o servidor**




## 2. Demais códigos

Para executar os demais códigos, eu acesso o servidor utilizando o comando:

```litc59```

**É fundamental sempre matar todos os processos do anaconda no meu nome sempre que terminar de usar o servidor**




## 3. Instalações

Para instalar bibliotecas etc., é fundamental que eu instale apenas para o meu user, por meio do
comando:

```pip install --user nome_pacote```




## 4. htop

No _htop_, é útil conhecer os seguintes comandos:

**F5**: organiza os processos baseado em algum critério (critérios podem ser vistos com F5 seguido de F6)
**I**: quando já foi dado F5, o I (maiúsculo) inverte a ordem do sort (fica descrescente)




## 5. conda

É muito recomendado utilizar um ambiente personalizado com as versões desejadas das bibliotecas e do Python. O conda permite gerenciar esses ambientes.

- Para criar um ambiente conda, usa-se:

```conda create --name nome_ambiente```

Se não for especificado a versão de python a se usar, será utilizada a versão mais recente.

**MUITO IMPORTANTE**: Para utilizar o Jupyter Notebook com o conda, é necessário **instalar o pacote nb_conda_kernels e o pacote ipykernel em todos os ambientes que se quiser usar o Jupyter**:

```conda install -n nome_ambiente nb_conda_kernels```
```conda install -n nome_ambiente ipykernel```

- Para ativar o ambiente, usa-se:

```conda activate nome_ambiente```

Toda vez que se desejar usar um determinado ambiente, é necessário utilizar o comando anterior. Antes de cada linha para input de comandos, deverá aparecer o nome do ambiente entre parênteses. Ex: (nome_ambiente) yanvgf@servidor: ...

- Para instalar um pacote:

```conda install nome_pacote```

Os demais comandos úteis do conda podem ser encontrados facilmente nos cheatsheets do conda.

**Importante**: Para utilizar o VSCode com o servidor no ambiente conda, é necessário **ativar o conda antes de dar bash no jupyter_online.sh**.

- Para criar um arquivo requirements.txt:

Uma boa prática de programação é criar um arquivo requirements.txt com todos os pacotes utilizados em uma implementação e suas versões para que outras pessoas possam replicar seus resultados. Para isso, faz-se:

```conda list -e > requirements.txt```

Isso lista todos os pacotes e suas versões (precisa ter o -e para as versões) e coloca essas informações no arquivo requirements.txt. Para instalar exatamente os mesmos pacotes que estão listados no arquivo, basta dar conda install nesse arquivo (as orientações para isso ficam na primeira linha do arquivo).




## 6. nohup

Muitas vezes, deseja-se deixar um programa rodando mesmo quando não estamos conectados ao servidor (por exemplo, rotinas que demoram muitas horas para rodar). 

Nesses casos, utiliza-se o comando ```nohup``` (_no hang up_), que permite deixar um código rodando sem a necessiade do usuário estar conectado ao servidor ou ao VSCode. 

O comando ```nohup``` deve ser utilizado antes dos comandos para executar os códigos que se deseja deixar rodando. No caso mais geral, quando se deseja rodar um jupyter notebook, utiliza-se:

```nohup bash jupyter_online.sh &``` 

para deixar um kernel do jupyter rodando mesmo quando você estiver offline. 

O "&" coloca o programa para rodar em segundo plano, de modo que o usuárui ainda consiga utilizar o terminal. Após executar este comando, será printado o número do processo referente a ele e uma mensagem indicando que a saída do programa será direcionada para um arquivo nohup.out. Aperta-se enter para voltar a usar o terminal.