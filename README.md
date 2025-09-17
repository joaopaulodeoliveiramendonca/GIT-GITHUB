# GIT-GITHUB
Trilha completa em Git e GitHub. Do zero ao avançado: fundamentos do controle de versão, comandos Git essenciais, branchs, merges, rebase, Git workflows, colaboração no GitHub, Pull Requests, integração contínua e melhores práticas. Todo código comentado para aprendizado prático.

# Instalar o Git

- Baixe o Git do [[site oficial]{.underline}](https://git-scm.com/).

- Siga as instruções de instalação para o seu sistema operacional.

## O que é controle de versão?

Controle de versão é um **sistema que registra as alterações feitas em
um arquivo ou conjunto de arquivos ao longo do tempo**. Ele permite que
você **volte para versões anteriores**, **compare alterações e colabore
com outras pessoas de forma eficaz**.

### Conceitos básicos

- **Repositório (repo)**: Local onde o código e o histórico de
  > alterações são armazenados.

- **Commit**: Cada alteração registrada no repositório, uma espécie de
  > \"foto\" do código em um ponto específico.

- **Branch**: Ramificação que permite o desenvolvimento paralelo. O Git
  > cria uma linha de desenvolvimento, permitindo múltiplas versões do
  > código.

## Comandos iniciais

```bash
git init
```

- git init: Inicializa um novo repositório Git local.

- git status: Verifica o status atual do repositório, mostrando
  > alterações feitas, arquivos não rastreados, etc.

- git add \<arquivo\>: Adiciona alterações ao índice (staging area) para
  > preparação do commit.

- git commit -m \"Mensagem do commit\": Registra as alterações no
  > repositório local.

## Criar seu primeiro repositório local

1.  Abra o terminal/linha de comando.

2.  Navegue até o diretório onde você deseja criar o repositório.

3.  Execute **git init** para iniciar o repositório.

4.  Crie ou modifique um arquivo, por exemplo, um arquivo **README.md**.

5.  Execute **git add README.md** para adicionar o arquivo ao estágio.

6.  Faça o commit com git commit -m \"Primeiro commit\".

# Trabalhando com GitHub

## Criar uma conta no GitHub

- Acesse [[GitHub]{.underline}](https://github.com/) e crie uma conta.

- Escolha um nome de usuário único e uma senha forte.

- Verifique seu e-mail para ativar a conta.

### Instalar e configurar o GitHub CLI ou usar HTTPS/SSH

- **Usando GitHub CLI (GitHub Command Line Interface)**:

  1.  Baixe e instale o GitHub CLI.

Configure o GitHub CLI no terminal com:

| **gh auth login** |
|-------------------|

2.  Escolha o GitHub.com e o método de autenticação (HTTPS ou SSH).

- **Ou configure SSH diretamente**:

  1.  Gere uma chave SSH com **ssh-keygen**.

  2.  Adicione a chave SSH ao GitHub em **Settings \> SSH and GPG keys
      > \> New SSH key**.

- **HTTPS**: Caso não queira usar SSH, pode configurar o GitHub para
  > usar HTTPS com sua senha/token.

## Configurar o login do Git com GitHub

Abra o terminal e configure seu nome de usuário e e-mail para vincular o
Git ao seu GitHub:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>git config --global user.name "Seu Nome"<br />
git config --global user.email "seuemail@example.com"</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

- Essa configuração será usada para associar suas alterações aos commits
  > feitos no repositório GitHub.

## Criar um repositório no GitHub

- No GitHub, clique em **New** no painel principal ou em **+ \> New
  > repository**.

- Preencha os campos:

  - **Nome do repositório**.

  - **Descrição** (opcional).

  - Escolha entre **Public** ou **Private**.

  - Não marque a opção de criar o arquivo **README.md**, pois já fizemos
    > isso localmente.

## Conectar o repositório local com o GitHub

No terminal, dentro do diretório do seu repositório local, adicione o
repositório remoto:

| git remote add origin https://github.com/\... |
|-----------------------------------------------|

Para enviar seu código local para o GitHub, use o comando:

| **git push -u origin main** |
|-----------------------------|

Caso o repositório já tenha sido inicializado com um **README.md**, você
pode fazer o comando **git pull** antes para sincronizar os arquivos e
evitar conflitos.

| git pull origin main |
|----------------------|

## Entendendo a diferença entre repositório local e remoto

- **Repositório Local**: O repositório que você criou no seu computador.

- **Repositório Remoto (GitHub)**: O repositório na nuvem, onde seu
  > código é armazenado e compartilhado.

# Branches e Colaboração

## Criar e trocar branches

No Git, **branches** permitem trabalhar em diferentes versões do código
simultaneamente.

Para criar uma nova branch, use:

| **git branch nome-da-branch** |
|-------------------------------|

Para mudar para essa branch:

| git checkout nome-da-branch |
|-----------------------------|

Alternativamente, você pode criar e mudar de branch com um único
comando:

| git checkout -b nome-da-branch |
|--------------------------------|

## Comitar mudanças em branches diferentes

- Faça alterações na sua branch.

Adicione e faça o commit das mudanças normalmente.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>git add &lt;arquivo&gt;<br />
git commit -m "Mensagem do commit"</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

- Isso vai garantir que as alterações sejam registradas na branch em que
  > você está trabalhando.

Para voltar a um commit anterior no Git, você pode usar alguns comandos
diferentes, dependendo de como deseja manipular seu histórico de
commits. Aqui estão algumas opções:

### Voltar para um commit anterior sem perder as mudanças locais

Se você quer voltar para um commit anterior e preservar suas alterações
locais, você pode usar o comando git checkout ou git switch:

#### **Usando git checkout:**

git checkout \<commit_hash\>

Ou, se você deseja voltar para um commit anterior:

git checkout HEAD\~1

Isso irá alterar o HEAD para o commit anterior. Se quiser voltar para
dois commits anteriores, use HEAD\~2, e assim por diante.

#### **Usando git switch:**

git switch \--detach \<commit_hash\>

Isso também vai fazer você sair para um \"detached HEAD\" e permitir que
você explore ou altere o commit, sem afetar o branch atual.

### 2. Voltar para um commit anterior e criar uma nova branch {#voltar-para-um-commit-anterior-e-criar-uma-nova-branch}

Se você deseja voltar para um commit anterior e começar uma nova branch
a partir desse ponto, você pode usar o seguinte comando:

git checkout -b \<nome_da_nova_branch\> \<commit_hash\>

### 3. Voltar para um commit anterior e fazer um reset (perdendo as mudanças locais) {#voltar-para-um-commit-anterior-e-fazer-um-reset-perdendo-as-mudanças-locais}

Se você quer voltar para um commit anterior e **descartar** todas as
mudanças que foram feitas após esse commit, você pode usar o comando git
reset.

#### **Para um reset suave (mantém as mudanças no diretório de trabalho):**

git reset \--soft \<commit_hash\>

#### **Para um reset misto (mantém as mudanças no diretório de trabalho, mas desfaz o staged area):**

git reset \--mixed \<commit_hash\>

#### **Para um reset hard (descarta todas as mudanças):**

git reset \--hard \<commit_hash\>

Isso vai **limpar** todas as alterações no seu diretório de trabalho,
retornando o repositório para o estado do commit fornecido.

### 4. Voltar para um commit anterior e fazer um revert {#voltar-para-um-commit-anterior-e-fazer-um-revert}

Se você quer \"desfazer\" um commit sem alterar o histórico do
repositório, você pode usar o comando git revert. Isso cria um novo
commit que desfaz as alterações do commit anterior, mas preserva o
histórico:

git revert \<commit_hash\>

### 5. Voltar para um commit anterior com o git reflog {#voltar-para-um-commit-anterior-com-o-git-reflog}

Se você fez uma alteração recente (como um reset ou checkout) e quer
voltar ao estado anterior, pode usar o git reflog para ver todas as
mudanças recentes no seu HEAD e retornar a um ponto anterior.

Veja o histórico de ações do seu HEAD:  
  
git reflog

1.  

Para voltar a um commit anterior mostrado no reflog:  
  
git checkout \<reflog_commit_hash\>

2.  

Esses são os métodos mais comuns para voltar a um commit anterior.
Dependendo da situação, escolha o comando que melhor se adapta ao seu
caso!

## Mergers: Integrando branches

- Quando você terminar de trabalhar em uma branch, pode querer combinar
  > (merge) suas alterações com outra branch, normalmente a **main**.

Primeiro, mude para a branch principal:

| git checkout main |
|-------------------|

Em seguida, faça o merge da sua branch de trabalho:

| git merge nome-da-branch |
|--------------------------|

## Resolver conflitos de merge

- Às vezes, ao fazer o merge, o Git pode encontrar conflitos (por
  > exemplo, quando duas pessoas editam o mesmo arquivo).

O Git irá marcar o arquivo com um conflito. Você precisará abrir o
arquivo, resolver o conflito e, então, adicionar e fazer o commit
novamente:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>git add &lt;arquivo&gt;<br />
git commit -m "Resolvendo conflito"</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

## Clonar repositórios existentes

Para clonar um repositório do GitHub para o seu computador:

| git clone https://github.com/seunomeusuario/nomedorepositorio.git |
|-------------------------------------------------------------------|

- Isso cria uma cópia completa do repositório remoto em seu computador.

## Trabalhando em colaboração

Para baixar (ou \"puxar\") alterações do repositório remoto:

| git pull origin main |
|----------------------|

- Isso traz as últimas mudanças do repositório remoto para o seu
  > repositório local.

# Fluxos de Trabalho no GitHub

## Criar Pull Requests (PRs) no GitHub

- **Pull Requests (PRs)** são usados para pedir que suas alterações em
  > uma branch sejam mescladas na branch principal ou em outra branch.

- Para criar um PR:

  1.  No GitHub, vá para o repositório onde você fez alterações.

  2.  Clique na opção **Pull Requests** e depois em **New Pull
      > Request**.

  3.  Escolha a branch que você trabalhou (ex. nome-da-branch) e compare
      > com a branch principal (main).

  4.  Adicione um título e uma descrição para o PR.

  5.  Clique em **Create Pull Request**.

## Revisar e comentar PRs

- Quando um PR é criado, outras pessoas podem revisar o código e
  > adicionar comentários.

- Eles podem sugerir mudanças ou aprovar as alterações.

- Para adicionar um comentário em um PR:

  1.  Clique no PR no GitHub.

  2.  Vá para a linha de código que deseja comentar e clique no ícone de
      > comentário.

  3.  Escreva seu comentário e clique em **Add review comment**.

## Aprovar ou rejeitar um PR

Quando você revisar um PR, você pode aprová-lo ou rejeitá-lo:

- **Approve**: Se você estiver satisfeito com o código, clique em
  > **Approve** e depois em **Merge pull request**.

- **Request changes**: Se você precisar de ajustes, escolha **Request
  > changes**.

## Issues no GitHub

- **Issues** são usadas para registrar bugs, tarefas ou sugestões no
  > repositório.

- Para criar uma Issue:

  1.  Vá até a aba **Issues** do repositório.

  2.  Clique em **New Issue**.

  3.  Dê um título e uma descrição para o problema ou tarefa.

## Trabalhando com Labels e Milestones

- **Labels** são usados para categorizar Issues (ex: bug, enhancement,
  > help wanted).

- **Milestones** ajudam a agrupar Issues relacionadas a uma entrega ou
  > versão específica do projeto.

- Para adicionar labels e milestones, basta editar a Issue e selecionar
  > as opções desejadas.

## Criar tags e releases

- As **tags** marcam pontos específicos na história do repositório, como
  > versões de software.

Para criar uma tag:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>git tag -a v1.0 -m "Versão 1.0"<br />
git push origin v1.0</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

- Você pode criar releases no GitHub diretamente na seção de
  > **Releases**, o que ajuda a disponibilizar versões do seu código
  > para os outros.

#### **5.1 Reescrevendo o histórico com git rebase e git cherry-pick** {#reescrevendo-o-histórico-com-git-rebase-e-git-cherry-pick}

- **git rebase**: Este comando permite reescrever o histórico de commits
  > de uma branch.

  - Ele é útil para **limpar o histórico** antes de enviar seu código
    > para o repositório remoto, combinando commits ou reorganizando-os.

Exemplo básico de rebase:  
  
git checkout feature-branch

git rebase main

- 

- Isso pega os commits da feature-branch e os coloca após os commits da
  > main.

<!-- -->

- **git cherry-pick**: Permite pegar um commit específico de outra
  > branch e aplicá-lo na branch atual.

Exemplo:  
  
git cherry-pick \<hash-do-commit\>

- 

#### **5.2 Reset e Revert** {#reset-e-revert}

- **git reset**: Usado para **desfazer commits**.

**\--hard**: Remove as alterações do diretório de trabalho e do
índice.  
  
git reset \--hard HEAD\~1

- (Isso desfaz o último commit e todas as mudanças associadas a ele).

<!-- -->

- **git revert**: Cria um **novo commit** que desfaz as alterações de um
  > commit anterior, sem alterar o histórico.

Exemplo:  
  
git revert \<hash-do-commit\>

- 

#### **5.3 Usando o git stash** {#usando-o-git-stash}

- **git stash**: Permite guardar alterações temporárias para que você
  > possa mudar de branch sem perder seu trabalho atual.

Para guardar alterações:  
  
git stash

- 

Para recuperar as alterações guardadas:  
  
git stash apply

- 

Se você tiver várias alterações guardadas, pode listar com:  
  
git stash list

- 

#### **5.4 Git Hooks** {#git-hooks}

- **Git hooks** são scripts que o Git executa em eventos específicos,
  > como antes de um commit ou merge.

- **Pré-commit hook**: Pode ser configurado para rodar testes ou linters
  > antes de permitir o commit.

- Exemplo de configuração de um hook pré-commit:

  1.  No diretório .git/hooks/, edite o arquivo pre-commit.sample.

  2.  Renomeie para pre-commit e adicione o script que você deseja
      > rodar.

**GitHub Avançado**

#### **6.1 GitHub Actions** {#github-actions}

- **GitHub Actions** são usadas para automatizar fluxos de trabalho
  > diretamente no GitHub, como rodar testes, construir o projeto ou
  > realizar deploys automáticos.

- Para começar a usar:

  - Vá até o seu repositório no GitHub.

  - Clique na aba **Actions** e escolha um modelo ou crie o seu próprio.

- Exemplo de um workflow simples que roda testes:

Crie um arquivo no repositório em .github/workflows/test.yml:  
  
name: Run Tests

on: \[push\]

jobs:

test:

runs-on: ubuntu-latest

steps:

\- uses: actions/checkout@v2

\- name: Set up Node.js

uses: actions/setup-node@v2

with:

node-version: \'14\'

\- name: Install dependencies

run: npm install

\- name: Run tests

run: npm test

- 

<!-- -->

- Isso fará com que, toda vez que você enviar um push para o
  > repositório, o GitHub Actions execute os testes automaticamente.

#### **6.2 GitHub Projects** {#github-projects}

- **GitHub Projects** é uma ferramenta de gestão de projetos que
  > organiza Issues e Pull Requests em quadros tipo Kanban.

- Para criar um novo projeto:

  1.  Vá até a aba **Projects** no seu repositório.

  2.  Clique em **New Project** e escolha entre um **Project board** ou
      > **Project classic**.

  3.  Organize suas tarefas arrastando Issues e PRs para diferentes
      > colunas (ex: **To Do**, **In Progress**, **Done**).

#### **6.3 GitHub Packages** {#github-packages}

- **GitHub Packages** permite que você publique e armazene pacotes de
  > software (como bibliotecas, containers Docker, etc) diretamente no
  > GitHub.

- Para publicar um pacote:

  1.  Crie um arquivo .github/workflows/publish.yml no seu repositório.

  2.  Adicione um fluxo de trabalho para publicar o pacote. Exemplo de
      > configuração para publicar um pacote NPM:

name: Publish Package

on:

push:

branches:

\- main

jobs:

publish:

runs-on: ubuntu-latest

steps:

\- uses: actions/checkout@v2

\- name: Publish package to GitHub

run: \|

npm publish \--access public

- 

#### **6.4 Segurança no GitHub** {#segurança-no-github}

- **Tokens de Acesso Pessoal (PATs)**: São usados para autenticar seu
  > acesso ao GitHub via HTTPS. É altamente recomendado usar tokens no
  > lugar de senhas.

  1.  Para criar um token, vá em **Settings \> Developer settings \>
      > Personal access tokens** no GitHub.

- **Branch Protection Rules**: Impede que mudanças sejam feitas
  > diretamente na branch principal (ex: main).

  1.  Vá para **Settings \> Branches**.

  2.  Em **Branch protection rules**, adicione uma regra para proteger a
      > branch principal.

  3.  Defina regras, como exigir aprovação de pull requests, status de
      > CI, etc.

### **Boas Práticas**

#### **7.1 Escrever mensagens de commit claras** {#escrever-mensagens-de-commit-claras}

- Mensagens de commit são essenciais para um histórico de código
  > compreensível.

- **Estrutura recomendada**:

  1.  **Título curto**: Resuma a mudança em 50 caracteres ou menos.

  2.  **Corpo do commit** (opcional): Detalhe o motivo da mudança, por
      > que ela foi feita e o que foi alterado. Deve ter menos de 72
      > caracteres por linha.

**Exemplo**:  
  
git commit -m \"Corrige erro no cálculo de preço\"

Se for necessário um corpo de mensagem:  
  
git commit -m \"Corrige erro no cálculo de preço\" -m \"Esse erro
ocorria quando a função de cálculo não considerava descontos
acumulados.\"

- 

#### **7.2 Adotar convenções de branch** {#adotar-convenções-de-branch}

- Definir uma convenção de nomes para branches facilita a organização e
  > a colaboração.

- **Exemplos de convenções**:

  - **feature/**: Para novas funcionalidades (ex:
    > feature/adicionar-login).

  - **bugfix/**: Para correções de bugs (ex:
    > bugfix/corrigir-erros-formulario).

  - **hotfix/**: Para correções urgentes (ex: hotfix/corrigir-api).

#### **7.3 Criar e configurar o arquivo .gitignore** {#criar-e-configurar-o-arquivo-.gitignore}

- O arquivo .gitignore informa ao Git quais arquivos ou pastas não devem
  > ser rastreados.

Exemplo de um .gitignore para um projeto Node.js:  
  
node_modules/

\*.log

.env

- Para criar um .gitignore, basta criar um arquivo chamado .gitignore na
  > raiz do repositório e adicionar as pastas ou arquivos que você
  > deseja ignorar.

#### **7.4 Entender o .gitattributes** {#entender-o-.gitattributes}

- O arquivo .gitattributes é usado para configurar como o Git lida com
  > certos tipos de arquivos, como finais de linha ou codificação.

Exemplo para configurar o Git para tratar arquivos .txt com end_of_line
= lf:  
  
\*.txt text eol=lf

- 

#### **7.5 Adotar um fluxo de trabalho** {#adotar-um-fluxo-de-trabalho}

- **GitFlow**: Um fluxo de trabalho popular que usa as branches main,
  > develop, feature/, release/, e hotfix/.

- **Trunk-based Development**: Onde todos os desenvolvedores trabalham
  > em uma única branch (normalmente a main), com commits frequentes
  > para evitar divergências grandes.

#### **7.6 Documentação no repositório** {#documentação-no-repositório}

- Sempre documente o seu repositório com um **README.md** explicando:

  - O que é o projeto.

  - Como configurar e rodar o projeto.

  - Como contribuir (se aplicável).

**Exemplo básico de README.md**:  
  
\# Nome do Projeto

Descrição breve do projeto.

\## Como rodar o projeto:

1\. Clone o repositório.

2\. Instale as dependências com \`npm install\`.

3\. Rode o projeto com \`npm start\`.

### 

###  **Revisão e Projeto Final** {#revisão-e-projeto-final}

#### **8.1 Criar um Projeto no GitHub** {#criar-um-projeto-no-github}

- Escolha um projeto que você queira desenvolver e crie um repositório
  > para ele no GitHub.

- **Configuração do repositório**:

  1.  Crie um README.md para documentar o projeto.

  2.  Crie um arquivo .gitignore para ignorar arquivos que não devem ser
      > rastreados.

  3.  Crie a estrutura inicial do projeto com arquivos básicos (por
      > exemplo, se for um projeto em Node.js, inicie com package.json).

#### **8.2 Usar branches, PRs, Issues e Actions** {#usar-branches-prs-issues-e-actions}

- Comece a trabalhar em uma **feature** criando uma branch específica
  > (feature/nome-da-feature).

- **Crie Issues** para registrar as tarefas ou bugs do projeto.

- **Submeta Pull Requests** para revisar seu código com outras pessoas
  > (ou se auto-revisar).

- **GitHub Actions**: Se o projeto for mais complexo, configure um
  > workflow simples para rodar testes sempre que um push for feito no
  > repositório.

#### **8.3 Colaborar com outras pessoas** {#colaborar-com-outras-pessoas}

- Se possível, colabore com outra pessoa em seu projeto ou crie uma
  > conta alternativa para simular a colaboração.

- Faça mudanças em uma branch, submeta um PR e peça para seu
  > \"colaborador\" revisar e aprovar.

- Caso haja conflitos de merge, resolva-os e finalize o merge.

#### **8.4 Trabalhar com Tags e Releases** {#trabalhar-com-tags-e-releases}

Após completar uma versão significativa do projeto, crie uma **tag**
para marcar o ponto específico no tempo:

git tag -a v1.0 -m \"Versão 1.0\"

git push origin v1.0

- 

- Crie uma **Release** no GitHub com a tag e adicione notas de versão.

#### **8.5 Documentação e Licenciamento** {#documentação-e-licenciamento}

- **README.md**: Faça uma documentação completa do projeto, explicando
  > como configurá-lo, usá-lo e contribuir.

- **LICENSE**: Se o projeto for open source, adicione um arquivo de
  > licença adequado, como o MIT License.

