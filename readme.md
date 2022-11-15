# Curso de Git e Github

## Git

Sistema de controle de versão distribuído. Criado por Linux Torvald e mantido pela comunidade open source.

### Instalação

Já vem instalados nos sistemas Unix, mas caso não esteja instalado o processo de instalação é muito simples e está disponível nessa página abaixo:/

[Git](https://git-scm.com/)

### Configs Globais  - git config

Essa configuração é necessária apenas uma vez, o git usará essa informação independente de atualizações.

```jsx
git config --global user.name "Seu nome de Usuário"

git config --global user.email "seuemail@email.com"
```

Isso vai ser usado como uma assinatura em todos os seus commits e caso você queira utilizar uma configuração diferente em um determinado projeto ela prevalece à configuração global, basta utilizar os comandos novamente sem a flag —global dentro da raíz do diretório em que deseja realizar a configuração.

Para verificar as configurações você pode usar o comando :

```jsx
git config --list 
```

Através do git config, podemos realizar uma série de configurações.. inclusive definir um editor de texto padrao, que por default ele usa o vim. 

## Github

Serviço na web que armazena os códigos versionados que utilizam o Git para o versionamento.Atualmente também é uma rede social, e nesse ambiente podemos compartilhar o nosso código e interagir com a comunidade.

[GitHub: Let's build from here](https://github.com/)

### Ciclo de vida dos estados dos arquivos

![Untitled](Curso%20de%20Git%20e%20Github%2072cdcd01572e40c0b84c8c31e98dcf45/Untitled.png)

- Basicamante, quando o arquivo está sob o estado Untracked o git não sabe de sua existência, ou em algum momento ele foi deletado e o git o removeu do seu rastreio.
- Unmodified, esse estado guarda um arquivo que foi addicionado, mas não houve nenhuma alteração
- Modified, nesse estado está o arquivo que nele realizou-se alterações
- Staged é o estado em que você adiciona as alterações em um ambiente para em seguida elas sejam salvas em um commit.

## Inicializando um repositório local com o Git

Abra um terminal, caminhe até o diretório que deseja inicializar o versionamento e digite o comando:

```jsx
git init
```

O git vai criar um diretório chamado .git com subdirectórios de configurações do git e informações sobre o projeto, pra acessar e verificar digite:

```jsx
cd .git
```

Até esse momento o git não sabe quais arquivos você tem lá, para que o Git entenda quais arquivos devem ser vistos você deverá os preparar para o commit com o comando:

```jsx
git add nomeDoArquivo.md 

ou 

git add . >>>>Prepara todos os arquivos alterados para o commit
```

- Somente arquivos que estiverem no staged vão ser commitados

> *******Commit é um ponto que será gravado na história do projeto, ele é marcado por você em algum momento que deseje salvar as alterações. O git usa um hash para identificar e manter um histórico de commits no projeto, que podem depois de salvos serem manipulados , podendo voltar em algum ponto da linha do tempo do projeto.*******
> 

Um commit tem essa sintaxe:

```jsx
git commit -m "Mensagem que descreva o que foi realizado de alteração"
```

Para verificar o status dos arquivos digite o comando :

```jsx
git status
```

## Entendendo Logs

Para exibir um histórico de logs 

```jsx
git log
```

Estrutura de uma resposta de log

![Captura de tela de 2022-11-14 18-56-04.png](Curso%20de%20Git%20e%20Github%2072cdcd01572e40c0b84c8c31e98dcf45/Captura_de_tela_de_2022-11-14_18-56-04.png)

Onde ele relata:

- O Hash do commit
    - commit 2c24eec2be1dc70b845d231ad10a6bde058302d2 (HEAD -> master)
- O Author, com o username e o e-mail
- A data
- A mensagem do commit

### Opções adicionais

```jsx
git log --decorate
```

Devolve uma resposta contendo detalhes curtos, como em qual branch está e de qual ela descende.

```jsx
git log --author="NomeOUPartialName"
```

Faz um filtro através da palavra que for colocada entre as chaves procurando por nome que deem macth.

```jsx
git shortlog
```

Mortra uma resposta com os autores que editaram commits no projeto, quantos commits foram e quais as mensagens de commit.

```jsx
git shortlog -sn
```

Devolve somente o nome do autor e a quantidade de commits no projeto.

```jsx
git log --graph
```

Devolve um log com gráfico mostrando as ramificações das branchs e datalhes sobre os merges através das cores dos gráficos.

## Entendendo diffs

```jsx
git diff
```

Mostra as diferenças entre um arquivo rastreado e que foi modificado. Importante ser usando antes de mudanças de commit.

```jsx
git diff --name-only 
```

Mostra somente o nome dos arquivos que foram modificados.

## Desfazendo coisas 👻

```jsx
git checkout NomedoArquivo.js
```

Restaura o arquivo para a última versão, é como clicar no botão de descartar da aba do github no editor de código.

```jsx
git reset HEAD NomedoArquivo.js
```

Se por acaso adicionar alguma mudança ao stage e precisar tirar do stage. utilize o comando acima. Ele pede que dentro da minh aramificação, tire esse arquivo do stage por favor.

```jsx
git reset --soft HashdoCoomitQdesejaRetornar
```

Esse comando reseta o commit para o staged, e você pode alterar a mensagem de commit por exemplo.

- Lembrando de sempre pegar o hash do commit anterior ao que você não gostaria de ter adicionado as mudanças, você tem oportunidade de corrigir.

```jsx
git reset --mixed HashdoCoomitQdesejaRetornar
```

Esse comando reseta o código para um estado anterior ao staged, então você tem a opção de realizar alterações, verificar a diferença entre os arquivos com o comando diff, e ele ainda retorna midificado com as últimas alterações. Você pode alterar, adicionar ao staged e commitar novamente.

```jsx
git reset --hard a88b1b6193634bddcc6298c03b3375965f7f5397
```

Esse comando descarta todo o código das branchs que estão acima do hash da branch em que você especificou, também deleta os commits e altera o histórico, então pode ser que em algum merge seja necessário utilizar a flag —force. Use com cautela.

## Trabalhando com repositórios remotos no Github

**Crie uma conta no github**

[https://github.com/](https://github.com/) 

**Crie um novo repositório, o link abaixo redireciona para a url de  criação de um novo repo.**

[Build software better, together](https://github.com/new)

---

**Através de linha de comando o passo-a-passo é o seguinte:**

- Lembrando que o diretório de trabalho local precisa estar sendo rastreado com o git, ele levará as mudanças que já foram commitadas.

****************Crie uma branch**************** 

```jsx
git branch -M main
```

****************************Crie um repositório remoto com https****************************

```jsx
git remote add origin https://github.com/username/nome-do-repo.git
```

### Enviando seu código local para o repositório remoto

*************************************Envie as mudanças para o repositório remoto*************************************

```jsx
git push -u origin main
```

Verificando qual nome do endereço remoto 

```jsx
git remote
```

Para verificar qual url remota do seu projeto, digite:

```jsx
git remote -v
```

Para alterar o endereço remoto digite:

```jsx
git remote set-url origin novoEndereçoAqui
```

### Clonando repositórios remotos

Você está em uma máquina diferente e deseja trabalhar em algum projeto que está armazenado no github, você poderá utilizar o recurso de clonar o projeto pra sua máquina, os motivos podem ser quaisquer, mas você deseja ter aquele projeto em sua máquina.

****************************************************Na página do seu projeto, localizado geralmente do lado direito superior, tem um menu de opções com um botão escrito “<> code”.**************************************************** 

 ********************************************************************************************************

![Captura de tela de 2022-11-15 09-29-22.png](Curso%20de%20Git%20e%20Github%2072cdcd01572e40c0b84c8c31e98dcf45/Captura_de_tela_de_2022-11-15_09-29-22.png)

Nele você terá a opção de fazer um download do projeto, ou utilizar o recurso clone onde o git disponibiliza o download dos arquivos em linha de comando, tanto através do protocolo https como do ssh e até outras opções. Aqui agora, vamos usar o atalho para clonar um repositório para sua máquina local através do git clone. 

********************************************************************************************************Entre na pasta desejada, abra algum terminal de linha de comando, e digite:********************************************************************************************************

```jsx
git clone EndereçoDeURLAqui
```

E você terá todo o código que está armazenado na nuvem em sua máquina local, e poderá acessar o histórico e commits e tudo que estiver documentado no projeto.

### Utilizando o fork

Você vai utilizar o fork, quando você não tem permissão para enviar alterações de push no projeto, então o fork criará uma cópia do trabalho para o seu namespace e lá você poderá realizar alterações e a partir disso enviar uma solicitação de pull request. 

## Branches

Branches são ramificações. E o que são ramificações em um sistema de versionamento ? 

Vamos pensar em uma linha contínua, e imaginar que essa linha é o nosso projeto, vamos supor que chegou um ponto em que o projeto está online e publicado, pessoas estão usando algum serviço que vem dele, mas ao mesmo tempo precisamos trabalhar em correções e novos serviços para esse projeto, vamos imaginar que você precise trabalhar em algum bug ou nova funcionalidade sem alterar essa linha principal, então criamos ramificações a partir dessa linha principal, que nada mais é do que uma cópia completa do que tem projeto nessa linha principal mais as suas modificações futuras que podem um dia se unir novamente, trazendo esses covos recursos ou novas funcionalidades.

**************************************Para criar uma nova branch************************************** 

```jsx
git branch NameBranch
```

************************Para entrar na branch************************ 

```jsx
git checkout NameBranch
```

****************************************Para criar e entrar na branch - abreviação dos comandos acima****************************************

```jsx
git checkout -b nameBranch
```

****************************************************************************************Para ver em qual branch se está atualmente**************************************************************************************** 

```jsx
git branch 
```

**********************************Para listar todas as branches do projeto********************************** 

```jsx
git branch -a 

git branch --all
```

**************************************Deletando branches************************************** 

- Não sei ao certo, mas parece que o comando com a flag -D maiúscula exclui forçado.

```jsx
git branch -D nomeDaBranch 

git branch -d nomeDaBranch 
```

****************Para ver o último commit em cada branch**************** 

```jsx
git branch -v 
```

**********************************Branches que já foram mescladas no branch atual**********************************

- Se quiser especificar um branch, escreva o nome da branch ao final do comando

```jsx
git branch --merged
```

****************************************************************************Branches que ainda não foram mescladas no branch atual****************************************************************************

```jsx
git branch --no-merged
```

******************************************************************************************************************Ver qual branch local está rastreando de qual branch remota - —track******************************************************************************************************************

- Este comando não consulta servidores, ele consulta o que veio no cache desde o último git fetch

```jsx
git branch -vv
```

### União de branches - Merge && Rebase

Agora entrou um assunto um pouco confuso, vou demorar a sintetizar pra conseguir escrever aqui de fato de uma forma boa, mas é isso, aos poucos vem mais entendimento e nada que não possa ser alterado.

O comando gir fetch baixa as alterações que estão no servidor para sua máquina, sem alterar o seu diretório de trabalho.

```jsx
git fetch origin master 
```

O comando git merge une as alterações do branch remoto para o branch local, a partir de seu comando.

```jsx
git merge origin master 
```

O comando git pull é uma espécie de git fecth + git merge e ele trás as alterações do servidor remot e já altera o seu diretório de trabalho conforme essas alterações de onde estão sendo rastreadas.

```jsx
git pull origin master 
```