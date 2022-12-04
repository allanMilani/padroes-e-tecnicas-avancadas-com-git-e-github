# Padrões e técnicas avançadas com Git e Github

## Git Comando básicos

**Configurações Iniciais**

- git config --local user.name "Seu nome aqui"
- git config --local user.email "seu@email.aqui"

**Definições**

- HEAD
    - Estado atual do nosso código, ou seja, onde o Git os colocou
- Working tree
    - Local onde os arquivos realmente estão sendo armazenados e editados
- Index
    - Local onde o Git armazena o que será *commitado*, ou seja, o local entre a *working tree* e o repositório Git em si.

**Arquivos especiais do git**

- *.gitignore*
    - adicionando arquivos e pastas neste arquivo quando realizar commit os arquivos especificados não serão adicionados

**Git - Comandos**

- ***git init***
    - Inicializa um repositório
- ***git init - -bare***
    - indica que o repositório é puro não contendo cópias dos arquivos, e sim apenas suas alterações
- ***git status***
    - mostra informações sobre o estado do repositório
- ***git add <file ou .>***
    - adiciona um ou vários arquivos para serem monitorados pelo git
- ***git commit -m “[Sua mensagem]”***
    - adiciona um commit juntamente com uma mensagem descritiva
- ***git log***
    - histórico de tudo que ocorreu na git
- ***git log - -oneline***
    - exibe o histórico de forma resumida onde cada ação ocupa apenas uma linha
- ***git log - -p***
    - exibe o histórico de maneira mais completa, mostrando o local que sofreu alteração
- ***git log - - graph***
    - exibe o histórico por meio de linhas de branchs
- ***git remote***
    - lista todos os repositórios remotos conhecidos pelo projeto
- ***git remote add [nome] [caminho do repositório]***
    - adiciona um endereço remoto para o projeto
- ***git remote rename [nome atual] [novo nome]***
    - renomeia o repositório
- ***git clone [caminho do repositório]***
    - clona um repositório
- ***git push [nome do repositório] [branch]***
    - envia as alterações
- ***git pull [nome do repositório] [branch]***
    - trás as alterações para o projeto local
- ***git branch***
    - exibe todos as branchs criadas
- ***git branch [nome da branch]***
    - cria uma nova branch a partir do ramo que se está
- ***git checkout [nome da branch]***
    - acessa uma branch
- ***git checkout -b [nome da branch]***
    - cria uma branch já acessando-a
- ***git merge [nome da branch]***
    - unifica duas branchs criando um commit de merge
- ***git rebase [nome da branch]***
    - unifica duas branchs atualizando a branch atual e mantendo as alterações feitas nela como última coisa feita
- ***git reset HEAD***
    - volta um commit
- ***git revert [hash]***
    - desfaz um commit gerando um novo commit de reversão
- ***git stash***
    - salva os dados modificados temporariamente em forma de pilha
- ***git stash list***
    - lista todos os dados salvos em forma de hash
- ***git stash pop***
    - traz o ultimo dado salvo na pilha
- ***git stash apply [numero da stash]***
    - recupera um dados específico na lista
- ***git stash drop***
    - deleta o ultimo dado inserido
- ***git diff [commit1]...[commit2]***
    - exibe todas as diferenças entre commits
- ***git tag***
    - exibe a lista com as tags
- ***git tag -a [nome da tag] -m “[mensagem]”***
    - gera uma tag (marco, release) na aplicação

---

## GitFlow

- Algumas definições de gitflow da Atlassian

[Gitflow Workflow | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

- DEVELOP
    - Branch de agregação, ou seja, onde ocorre o desenvolvimentos das funcionalidades
- MASTER
    - Branch que está em produção
- RELEASE
    - Branch de homologação
- HOTFIX
    - Branch de resolução de erros em produção
- Instalação do gitflow
    - https://github.com/nvie/gitflow

### Trabalhando com Git Flow

- Quando é feito o merge da release, o git flow realiza o merge da master e da develop

Inicializa o respositorio, especificando as branchs de dev e release, alem de prefixos de brach (feature, release, hotfix, support)

```yaml
git flow init
```

Cria uma branch baseada no prefixo

```yaml
git flow [PREFIXO] start [TITULO DA BRANCH]
```

Faz o merge das alterações na branch padrão e deleta a branch trabalhada

```yaml
git flow [PREFIXO] finish [TITULO DA BRANCH]
```

---

## Configurando repositório github

### Configurando github para conter assinaturas de commits

- No terminal (com o GPG instalado)
    - ***gpg --list-secret-key --keyid-form LONG*** (Lista as chaves criadas no sistema)
    - ************************************************************************gpg --full-generate-key (************************************************************************Gera uma chave************************************************************************)************************************************************************
        - Questão 1: 1 (RSA and RSA)
        - Questão 2: 4096
        - Questão 3: 1y (1 ano)
        - Questão 4: y
        - Questão 5: Nome no git
        - Questão 6: Email no git
        - Save
        - Senha para a chave
    - ************gpg --armor --export [ID DA CHAVE -Obtido rodando o primeiro comando e após o tipo da chave tera o id]**** (**Exibe a chave pelo id********)********
- No github
    - Acesse as configurações
    - SSH and GPG keys
    - New GPG key
    - Colar a chave publica que é exibida no terminal
- No terminal
    - ************git config --global user.signingkey [ID DA CHAVE]************
    - ***nano ~/.bash_profile***
        - adicione a linha *********************************************export GPG_TTY=$(tty)*********************************************
    - *********************************************git config --global commit.gpgsign true********************************************* [Habilita assinatura por padrão nos commits]
    - *********************************************git config --global tag.gpgSign true********************************************* [Habilita a assinatura por padrão nas tags]
- Adicionando mais de um email na chave (****************TERMINAL****************)
    - ***gpg --edit-key [ID DA CHAVE]***
    - No terminal que se abre
        - ***adduid***
        - ***uid [NUMERO DO USUARIO]***
        - ***trust***
            - Opção 5
        - ***save***

## PRs (Solicitação de merge) e Code Review

### Plugins VsCode

- GitHub Pull Requests an Issues

### Configurando branchs e permissões

No github

- Acesse: Configurações → Branchs
- Default branch = develop
- Branch protection
    - Branch name: nome da brranch ou padrões (feature/*)
    - Selecionar as regras da branch
    

***** Sobre proteção de branches e organizações*****

O processo de proteção de branches que restringe quem poderá realizar o 
push é uma funcionalidade que está disponível apenas para repositórios 
associados a uma organização no Github (o que é o mais comum quando 
trabalhamos com github em uma empresa).

Logo, se você não estiver vendo a opção: "Restrict who can push to 
matching branches" e quiser testar o recurso, crie uma organização no 
Github e crie um repositório associado a ela.

### Configurando template de PRs

[Creating a pull request template for your repository - GitHub Docs](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)

No local

- criar a pasta *.github*
- na pasta adicionar o modelo como PULL_REQUEST_TEMPLATE.md

### Codowners

[https://docs.github.com/pt/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners](https://docs.github.com/pt/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)

Explicita o dono de código, adicionando a automatização do revisor que é dono do código

- Na pasta .github
- Criar o arquivo CODEOWNERS.md
- Exemplo

```yaml
*.js @[NOME_DO_DONO OU GRUPO]
```

## Semantical Versioning e Conventional Commits

[Versionamento Semântico 2.0.0](https://semver.org/lang/pt-BR/)

MAJOR.MINOR.PATCH

MAJOR → Versão principal do sitema (API publica)

MINOR → Adicionando funcionalidades, mas compativel com a API

PATCH  → Bugs, ajustes 

Padronização de commits (existe um plugin no vscode)

[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)

Validados de commit

[commitlint - Lint commit messages](https://commitlint.js.org/#/)

Validador de Commit para integração continua

[Introduction](https://commitsar.aevea.ee/)

Criador de conventional commit via linhad e comando

[Commitizen](https://commitizen-tools.github.io/commitizen/)