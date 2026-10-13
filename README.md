## O que é

- **Git:** Sistema de versionamento de projetos. Cada modificação/versão do projeto é chamada de commit.
- **GitHub:** Serviço de hospedagem online de repositórios git. Ele  é gratuito para projetos de código aberto e pago para projetos privados. É o maior serviço desse tipo no mundo, mas possui alternativas como o GitLab e BitBucket.

## Repositório remoto e local

Cada projeto no git é chamado de repositório de versionamento:

- **Repositório remoto**: cópia oficial do repositório que fica salva em um servidor (Ex: Github);
- **Repositório local**: cópia local do repositório principal, utilizada para fazer as alterações no projeto e depois enviar para o repositório remoto.

## Stage

O Stage é um área intermediária onde fica localizada os arquivos que serão considerados para a próxima versão (commit).

Antes de irem para o stage, essas mudanças ficam no Working directory e podem ser visualizadas através do comando `git status`. As alterações no projeto se dividem em três status:

- **modified:** um ou mais arquivos foram modificados.
- **untracked:** um novo arquivo foi criado e ainda não está listado.
- **deleted:** um ou mais arquivos foram deletados.

As modificações não são automaticamente consideradas para o próximo commit, pois o desenvolvedor pode preferir fazer o versionamento por partes. O stage permite considerar exatamente quais partes serão utilizadas na próxima versão.

## .gitignore

É o arquivo que indica para o git o que não deve ser salvo. Um projeto pode ter um .gitignore na pasta principal ou um para cada subpasta.

O que não deve ser salvo:

- Arquivos compilados;
- Arquivos de bibliotecas externas;
- Arquivos de configuração da IDE;
- Arquivos de configuração do sistema.

## Branch

No git uma branch é um workspace paralelo onde é possível realizar mudanças sem afetar o projeto principal. Esse workspace separado é uma cópia do principal para a partir dele fazer uma ramificação (daí o nome branch).

Essa função é utilizada para:

- Desenvolver novas funções
- Corrigir bugs
- Testar ideias

Com as branchs é possível trabalhar em diferente frentes em um projeto sem afetar diretamente o ramo principal e nem outras branchs. Quando concluída a tarefa uma branch pode ser mesclada (merge) com a branch main do projeto.

## Comandos git

### Configuração

- `git config --global user.name "name"` - define como seu nome que irá aparecer nos commits.
- `git config --global user.email "email do github"` - define o email padrão do github.
- `git config --global init.defaultbranch "main"` - define o o nome da branch padrão no repositorio local como main. Por padrão, o git utiliza nomenclatura master, mas para manter a padronização com o GitHub recomenda-se modificar para main.
- `git config list` - lista as configurações definidas pelo usuário.

### Iniciar repositório

- `git init` - criar um repositório git ou reinicializa um repositório existente.
- `git branch -M` - renomeia a branch atual. Usado para adequar o nomenclatura da branch principal que agora é ‘main’ .
- `git remote add origin git@github.com:usuario/repositorio.git` - comando utilizado para vincular repositório remoto ao repositório local. Necessário antes fazer a configuração da chave SSH caso não tenha configurado a conexão com o GitHub ainda.
- `git push -u` - Envia os commits e estabelece a relação entre a branch local com a branch remota. Utilizada no primeiro push.
- `git remote set-url origin git@github.com:usuario/repositorio.git` - Altera o repositório remoto configurado.

### Comandos gerais

- `git add .` - adiciona ao stage todos os arquivos modificados daquele repositório.
- `git commit -m` - cria um commit com as modificações adicionadas ao stage e atribui uma descrição a versão.
- `git status` - verifica a diferença entre a árvore de trabalho e o arquivo de index e lista todos os caminhos que foram modificados ou que não existem no index.
- `git push` - Envia os commit para o repositório remoto.
- `git clone git@githu.com:usuario/repositorio.git` - copia um repositório remoto disponível no GitHub para ao diretório onde o comando foi executado.
- `git log` - Mostra a lista dos commits de um repositório na ordem reversa em que foram adicionados. Sinaliza também até qual commit o repositório remoto está atualizado.
- `git log --oneline` - Mostra a lista dos commits de um repositório de maneira resumida.
- `git diff nome_arquivo` - Exibe no terminal qual foram as modificações realizadas em um arquivo em comparação com última versão.
- `git checkout codigo_commit` - permite restaturar temporariamente os arquivos do projeto ao estado de determinado commit.
- `git checkout HEAD~n` - restaura o projeto ao n commit anterior ao HEAD (último commit). Sendo n = 1 o penúltimo, n = 2 o antepenúltimo e assim por diante.
- `git commit` - o commit sem a mensagem faz abrir o editor de texto de terminal para digitar a mensagem do commit. No windows pode abri o Vim e no linux irá abrir o Nano.
- `git pull nome_remote nome_branch` - atualiza o repositório local em comparação com o remoto.
- `git push -f` - Envia os commit para o repositório remoto. Ele força o envio dos commits mesmo com conflitos e pode sobrescrever commits do repositório remoto que não poderão ser recuperados depois.

### Desfazer modificações não salvas

- `git reset` - retirar os arquivos do stage e retorna para a working tree.
- `git clean -df` - limpa os arquivos não rastreados pelo git. O -d permite remover também os diretórios não rastreados e o -f força a remoção.
- `git checkout -- .` - descarta todas as alterações feitas e restaura o projeto para o último commit.

### Desfazer commits

- `git reset --soft HEAD~1` - desfaz o último commit sem apagar as modificações feitas, lançando elas novamente na working tree.
- `git reset --hard HEAD~1` - desfaz o último commit e apaga todas as modificações.
- `git reset --hard codigo_commit` - volta o projeto ao estado de um dado commit. Todos os commits e alterações posteriores serão apagadas.

### Branch e merge

- `git branch` - lista todas as branch de um repositório.
- `git branch nome_branch` - cria uma nova branch com o nome informado.
- `git switch nome_branch` - permite trocar de branch.
- `git checkout nome_branch` - permite trocar de branch.
- `git checkout -b nome_branch` - cria uma nova branch e faz a troca da branch atual para a nova.
- `git branch -d nome_branch` - exclui a branch caso ela já tenha ocorrido o merge com a branch principal.
- `git branch -D nome_branch` - força a exclusão da branch caso ela não tenha ocorrido o merge com a branch principal.
- `git branch -m nome_antigo nome_novo` - renomeia uma branch.
- `git merge nome_branch` - mescla a branch informada na branch atual, incorporando suas alterações e preservando os commits originais. Se for possível fazer um fast-forward, o Git apenas avança o ponteiro da branch atual. Caso contrário, será criado um commit de merge, que conecta os históricos das duas branches.
- `git merge --squash nome_branch` - reúne todas as alterações da branch informada em uma única alteração preparada para commit na branch atual, sem incorporar os commits originais à linhagem dessa branch. Usado para manter limpo o histórico de commits após um merge. Necessário executar um git commit logo após.
- `git merge --no-ff nome_branch` - mescla a branch informada na branch atual, preservando seus commits originais. Impede o fast-forward, forçando a criação de um commit de merge, mesmo quando seria possível apenas avançar o ponteiro da branch atual.
- `git merge --abort` - serve para cancelar um merge em caso de erro, por exemplo, um conflito em algum arquivo durante o merge.