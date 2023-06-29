# Como configurar Git-Credential-Manager-Core no Linux

Este documento explica como instalar e configurar o Git Credential Manager Core no Linux. Ele também descreve o que é o Git Credential Manager Core e como ele pode ser útil para gerenciar e autenticar credenciais do Git e outros serviços relacionados a versionamento de código.

### Tópicos

- O que é o Git Credential Manager Core?
- Como instalar e configurar o Git Credential Manager?
    - Baixando e instalando o arquivo .DEB do Git Credential Manager Core
    - Configurando o Git Credential Manager
    - Realizando a autenticação com o GitHub
    - Explicação dos comandos
- Como eliminar credenciais do Git Credential Manager Core?

## O que é o Git-Credential-Manager-Core ?

O Git Credential Manager Core é uma implementação de código da Microsoft de código aberto que permite gerenciar e autenticar credenciais do Git e diversos tipos de serviços relacionados a versionamento de código.

Ele permite a autenticação por vários serviços de autenticação como : SSH,token de autenticação, confirmação de dois fatores, entre outros. Ele é útil para quando desejamos uma autenticação rápida para acesso aos nossos repositórios de código,como por exemplo no push para um repósitório ou clone para um repositório privado. Outra vantagem, é você não precisar ficar realizando essa autenticação diversas vezes, pois ele guarda a suas credencias de acesso  quando você faz a primeira autenticação assim quando você acessar um repositório, ele faz essa autenticação automaticamente, pois ele guarda suas credencias em cache de uma forma segura.

Em resumo, o Git-Credential-Manager é uma solução muito útil e segura para aqueles que querem simplificar e acelerar o processo de autenticação em serviços de versionamento de código, elimando complexidade e demora associadas.

## Como Instalar e Configurar o Git Credential Manager?

### 1. Baixe e Instale o arquivo .DEB do Git Credential Manager Core

Acesse esse link: https://github.com/git-ecosystem/git-credential-manager/releases/tag/v2.1.2

Em “ComoConfigurarGitCredentialManager” clique na opção com extensão .deb. Segue um print abaixo:

![Untitled](ComoConfigurarGitCredentialManager/Untitled.png)

![Untitled](ComoConfigurarGitCredentialManager/Untitled%201.png)

Depois de ter baixado o pacote.deb, com o terminal, vá até a pasta onde esta localizado o seu arquivo.

![Untitled](ComoConfigurarGitCredentialManager/Untitled%202.png)

Para instalar o pacote, estando no diretório do arquivo, execute o comando "dpkg -i nome_do_pacote.deb".

![Untitled](ComoConfigurarGitCredentialManager/Untitled%203.png)

Feito isso, execute o comando "git-credential-manager-core --version" para verificar se foi instalado corretamente. Abaixo está a saída esperada:

![Untitled](ComoConfigurarGitCredentialManager/Untitled%204.png)

### 2. Configurando o Git Credential Manager

Com o GCM (Git Credential Manager Core) instalado, vamos configurar o Git para usá-lo como gerenciador de credenciais padrão. Para isso, utilize o comando abaixo:

```jsx
git config --global credential.helper manager-core
```

Depois disso, configuraremos qual serviço usaremos para guardar e recuperar as credenciais. Existem diversos serviços que realizam essa função, como o GPG (GNU Privacy Guard), Credential Cache, Plaintext files e [freedesktop.org](http://freedesktop.org/) Secret Service API, entre outros. Cada um tem suas peculiaridades e formas diferentes de gerenciamento de credenciais. No entanto, por motivos didáticos e para facilitar, usaremos o [freedesktop.org](http://freedesktop.org/) Secret Service API, que possibilita autenticação via interface gráfica e é mais ágil. Para utilizá-lo, basta executar o comando abaixo:

```bash
git config --global credential.credentialStore secretservice
```

Para aplicar as configurações, utilize o comando abaixo:

```bash
git-credential-manager configure
```

O último passo da configuração é inserir seu nome de usuário e e-mail do Github para que o autor seja exibido no commit. Isso é muito simples! Insira os dois comandos abaixo:

```bash
git config --global user.name SEU_USERNAME_GITHUB

git config --global user.email SEU_EMAIL_GITHUB
```

 ****

**⚠️ SE VOCÊ NÃO FIZER ISSO, CONSEGUIRÁ FAZER COMMIT NORMALMENTE, MAS APARECERÁ COMO AUTOR DE OUTRA PESSOA!**

## 3. Realizando a autenticação com o GitHub

Depois disso, basta executar o comando Git em algum repositório em que você esteja desenvolvendo. Na primeira vez, será exibida esta tela:

![Untitled](ComoConfigurarGitCredentialManager/Untitled%205.png)

Basta selecionar a opção "Sign in with your browser" e você será direcionado para a tela do seu navegador, onde poderá entrar na sua conta do GitHub. Caso você ainda não esteja autenticado, será necessário fazer login. Caso contrário, você será redirecionado automaticamente e verá a seguinte tela:

![Untitled](ComoConfigurarGitCredentialManager/Untitled%206.png)

Pronto, se olhar no seu terminal irá perceber que o comando que vocẽ fez no repositório foi feito com sucesso.

![Untitled](ComoConfigurarGitCredentialManager/Untitled%207.png)

 

Pronto! O próximo comando que você executar não precisará passar pela autenticação, já que suas credenciais estão salvas na sua máquina.

**EXPLICAÇÃO DOS COMANDOS**

`git-credential-manager-core --version`: Esse comando verifica se o Git Credential Manager Core (GCM Core) foi instalado corretamente exibindo a versão do GCM Core instalada.

`git config --global credential.helper manager-core`: Esse comando configura o GCM Core como o gerenciador de credenciais padrão do Git.

`git config --global credential.credentialStore secretservice`: Esse comando configura o serviço "secretservice" como o método de armazenamento e recuperação de credenciais do Git. O serviço "secretservice" refere-se à freedesktop.org Secret Service API, que é usada para armazenar e recuperar segredos, como senhas, de forma segura em sistemas Linux.

`git-credential-manager configure`: Esse comando é usado para aplicar as configurações do GCM Core. Ele pode ser usado para fornecer informações adicionais ou ajustar as configurações do GCM Core.

`git config --global user.name SEU_USERNAME_GITHUB`: Esse comando configura o nome de usuário do GitHub que será usado como autor nos commits do Git. Substitua "SEU_USERNAME_GITHUB" pelo seu nome de usuário do GitHub.

`git config --global user.email SEU_EMAIL_GITHUB`: Esse comando configura o e-mail associado à sua conta do GitHub que será usado como autor nos commits do Git. Substitua "SEU_EMAIL_GITHUB" pelo seu e-mail do GitHub.

## BONUS 💥

### Como eliminar credenciais do Git Credential Manager Core?

Para eliminar credenciais em Distribuições que usam com ambiente de trabalho o GNOME, basta usar o comando “seahorse” no terminal e sera exibido essa tela:

![Untitled](ComoConfigurarGitCredentialManager/Untitled%208.png)

Para remover sua senha do GitHub, selecione a credencial do GitHub e clique duas vezes nela. Em seguida, selecione a opção "excluir senha" embaixo de "detalhes" e confirme a exclusão.

![Untitled](ComoConfigurarGitCredentialManager/Untitled%209.png)

![Untitled](ComoConfigurarGitCredentialManager/Untitled%2010.png)

Para finalizar, limpe as informações do nome de usuário e do email que foram cadastrados para o autor do commit, utilizando os comandos abaixo:

```bash
git config --global --unset user.name

git config --global --unset user.email 
```

Feito isso, não haverá mais credenciais de usuário cadastradas no sistema.

> By PedroRocs - *“A criação não foi um acidente, mas uma intenção.”*
>