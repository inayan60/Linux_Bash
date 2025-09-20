# Índice

| Capítulo | Descrição | Comandos |
|----------|-----------|----------|
| [Comandos Essenciais](#comandos-essenciais-para-analista-linux) | Resumo de navegação, análise e processos | [Navegação e Listagem](#navegacao), [Visualização e Análise](#visualizacao), [Análise de Processos](#analise) |
| [Capítulo 1](#capitulo-1) | Navegação e Listagem | [ls](#ls), [cd](#cd), [pwd](#pwd) |
| [Capítulo 2](#capitulo-2) | Manipulação de Diretórios | [mkdir](#mkdir), [rmdir](#rmdir) |
| [Capítulo 3](#capitulo-3) | Manipulação de Arquivos | [rm](#rm), [cp](#cp), [mv](#mv), [touch](#touch) |
| [Capítulo 4](#capitulo-4) | Visualização de Arquivos | [cat](#cat), [less](#less), [head](#head), [tail](#tail) |
| [Capítulo 5](#capitulo-5) | Busca e Localização | [find](#find), [grep](#grep), [which](#which), [locate](#locate) |
| [Capítulo 6](#capitulo-6) | Permissões e Propriedades | [chmod](#chmod), [chown](#chown), [chgrp](#chgrp) |
| [Capítulo 7](#capitulo-7) | Informações do Sistema | [df](#df), [du](#du), [ps](#ps), [top](#top) |
| [Capítulo 8](#capitulo-8) | Diferenças entre Distribuições | – |
| [Capítulo 9](#capitulo-9) | Variáveis e Histórico | – |






## Comandos e Combinações Essenciais para um Analista Linux

<details>
<summary>Clique para expandir as combinações essenciais</summary>


### Navegação e Análise Rápida
<a id="navegacao"></a>
  * **`ls -lha`**: Uma das combinações mais importantes. Lista arquivos e diretórios com detalhes (`-l`), em formato legível para humanos (`-h`), e inclui arquivos ocultos (`-a`). Ideal para uma visão geral instantânea de qualquer diretório.
  * **`cd -`**: Volta rapidamente para o diretório de onde você veio. Extremamente útil para alternar entre dois locais.
  * **`find . -type f -mtime -7`**: Encontra todos os arquivos (`-type f`) modificados nos últimos 7 dias (`-mtime -7`) a partir do diretório atual (`.`). Perfeito para auditoria e investigações recentes.


### Visualização e Análise de Logs
<a id="visualizacao"></a>
  * **`tail -f /var/log/syslog`**: Acompanha em tempo real as últimas linhas de um arquivo de log. Essencial para monitorar o que está acontecendo no sistema enquanto um serviço está rodando.
  * **`cat arquivo.log | grep "ERRO"`**: Usa o `cat` para exibir o conteúdo do log e, Qatravés de um pipe (`|`), filtra as linhas que contêm a palavra "ERRO". A combinação `cat | grep` é a base da análise de logs.
  * **`grep -iR "configuração" /etc/`**: Busca a palavra "configuração" (`-i` ignora maiúsculas/minúsculas) de forma recursiva (`-R`) em todos os arquivos dentro do diretório `/etc/`.
  * **`du -sh *`**: Mostra o tamanho total (`-s`) de cada subdiretório e arquivo no formato legível para humanos (`-h`). Ótimo para identificar rapidamente quais diretórios estão consumindo mais espaço em disco.

<a id="analise"></a>
### Análise de Processos

  * **`ps aux | grep nome_do_serviço`**: Lista todos os processos (`aux`) e filtra para encontrar o processo de um serviço específico.
  * **`top -u nome_do_usuario`**: Monitora o uso de recursos (CPU, memória) apenas para os processos de um usuário específico.

</details>

-----

<a id="capitulo-1"></a>

## Capítulo 1: Navegação e Listagem

<details>
<summary>Clique para expandir o conteúdo sobre ls, cd e pwd</summary>
<a id="ls"></a>
  
### ls

  * **O que é**: O comando `ls` (list) é um dos mais fundamentais. Ele é usado para listar arquivos e diretórios.

#### **Ls básico**

-----

Lista arquivos e diretórios do diretório atual:

```bash
ls
```

Lista incluindo arquivos ocultos:

```bash
ls -a
```

Lista em formato longo com detalhes:

```bash
ls -l
```

#### **Combinações mais usadas**

-----

Lista tudo com detalhes (incluindo ocultos):

```bash
ls -la
```

Lista com tamanhos legíveis:

```bash
ls -lh
```

Lista ordenando por data de modificação:

```bash
ls -lt
```

Lista recursivamente em subdiretórios:

```bash
ls -R
```

#### **Opções do ls**

**-a ou --all**
Mostra todos os arquivos, incluindo os ocultos (que começam com ponto):

```bash
ls -a
```

**-l (formato longo)**
Exibe informações detalhadas: permissões, proprietário, grupo, tamanho, data de modificação.

```bash
ls -l
```

**-h ou --human-readable**
Com a opção `-l`, mostra tamanhos de arquivos em formato legível (ex: K, M, G).

```bash
ls -lh
```

**-t**
Ordena a listagem por data e hora de modificação, mostrando os mais recentes primeiro.

```bash
ls -t
```

**-r ou --reverse**
Inverte a ordem da listagem.

```bash
ls -r
```

**-S**
Ordena os arquivos por tamanho, do maior para o menor.

```bash
ls -S
```

**-R ou --recursive**
Lista recursivamente o conteúdo de todos os subdiretórios.

```bash
ls -R
```

**-d ou --directory**
Lista apenas o diretório em si, e não o seu conteúdo. Útil com curingas.

```bash
ls -d */
```

**--color**
Adiciona cores à saída do comando, facilitando a diferenciação entre tipos de arquivos (geralmente já ativo por padrão).

```bash
ls --color=always
```

-----
<a id="cd"></a>
### cd

  * **O que é**: O comando `cd` (change directory) é usado para mudar o diretório de trabalho atual.

#### **cd básico**

-----

Vai para o diretório home do usuário:

```bash
cd
```

Vai para um diretório específico:

```bash
cd /caminho/para/diretorio
```

Volta um diretório acima:

```bash
cd ..
```

Volta ao diretório anterior:

```bash
cd -
```

#### **Opções do cd**

**-L (padrão)**
Segue links simbólicos.

```bash
cd -L /caminho/com/link
```

**-P**
Usa a estrutura física do sistema de arquivos, ignorando e resolvendo links simbólicos para o caminho real.

```bash
cd -P /caminho/com/link
```

#### **Navegação com variáveis**

-----

Vai para o diretório home (mesmo que `cd` sozinho):

```bash
cd $HOME
```

Usa o diretório anterior armazenado:

```bash
cd $OLDPWD
```

-----
<a id="pwd"></a>
### pwd

  * **O que é**: O comando `pwd` (print working directory) exibe o caminho completo do seu diretório de trabalho atual.

#### **pwd básico**

-----

Mostra o diretório atual:

```bash
pwd
```

#### **Opções do pwd**

**-L (padrão)**
Mostra o caminho lógico, ou seja, com links simbólicos.

```bash
pwd -L
```

**-P**
Mostra o caminho físico, resolvendo os links simbólicos para o caminho real.

```bash
pwd -P
```

</details>

-----

<a id="capitulo-2"></a>

## Capítulo 2: Manipulação de Diretórios

<details>
<summary>Clique para expandir o conteúdo sobre mkdir e rmdir</summary>
  
<a id="mkdir"></a>
### mkdir

  * **O que é**: O comando `mkdir` (make directory) é usado para criar novos diretórios.

#### **mkdir básico**

-----

Cria um diretório simples:

```bash
mkdir nome-do-diretorio
```

Cria múltiplos diretórios:

```bash
mkdir dir1 dir2 dir3
```

#### **Opções do mkdir**

**-p ou --parents**
Cria os diretórios pais necessários no caminho, caso eles não existam.

```bash
mkdir -p caminho/completo/para/diretorio
```

**-v ou --verbose**
Mostra uma mensagem para cada diretório que é criado, confirmando a ação.

```bash
mkdir -v novo-diretorio
```

**-m ou --mode**
Define as permissões do diretório no momento da criação.

```bash
mkdir -m 755 diretorio-com-permissoes
```

#### **Combinações úteis**

-----

Cria uma estrutura de diretórios completa com mensagens de confirmação:

```bash
mkdir -pv projetos/2024/janeiro
```

Cria um diretório com permissões restritas (apenas para o proprietário):

```bash
mkdir -pm 700 diretorio-privado
```

-----
<a id="rmdir"></a>
### rmdir

  * **O que é**: O comando `rmdir` (remove directory) é usado para remover diretórios, mas **apenas se estiverem vazios**. Se o diretório contiver arquivos ou subdiretórios, o comando falhará.

#### **rmdir básico**

-----

Remove um diretório vazio:

```bash
rmdir nome-do-diretorio
```

Remove múltiplos diretórios vazios:

```bash
rmdir dir1 dir2 dir3
```

#### **Opções do rmdir**

**-p ou --parents**
Remove o diretório e seus pais, se eles ficarem vazios após a remoção.

```bash
rmdir -p caminho/completo/diretorio
```

**-v ou --verbose**
Mostra uma mensagem para cada diretório removido.

```bash
rmdir -v diretorio-vazio
```

</details>

-----

<a id="capitulo-3"></a>

## Capítulo 3: Manipulação de Arquivos

<details>
<summary>Clique para expandir o conteúdo sobre rm, cp, mv e touch</summary>

<a id="rm"></a>
### rm

  * **O que é**: O comando `rm` (remove) é usado para remover arquivos e diretórios de forma permanente. Use com cuidado, pois a remoção é irreversível.

#### **Rm básico**

-----

Remove um arquivo:

```bash
rm arquivo.txt
```

Remove múltiplos arquivos:

```bash
rm arquivo1.txt arquivo2.txt
```

#### **Opções do rm**

**-f ou --force**
Remove arquivos sem pedir confirmação e ignora erros se o arquivo não existir.

```bash
rm -f arquivo-que-pode-nao-existir.txt
```

**-i**
Pergunta antes de remover cada arquivo, o que serve como uma medida de segurança.

```bash
rm -i arquivo-importante.txt
```

**-r ou -R ou --recursive**
Remove diretórios e todo o seu conteúdo, incluindo subdiretórios e arquivos.

```bash
rm -r diretorio-completo
```

**-v ou --verbose**
Mostra o nome de cada arquivo que está sendo removido.

```bash
rm -v arquivo.txt
```

#### **Combinações perigosas mas úteis**

-----

Remove um diretório e seu conteúdo sem perguntar. **Esta é uma combinação perigosa e deve ser usada com extrema cautela.**

```bash
rm -rf diretorio
```

Remove um diretório com confirmação e detalhes.

```bash
rm -rv diretorio
```

Remove forçado com detalhes.

```bash
rm -fv arquivo*
```

-----
<a id="cp"></a>
### cp

  * **O que é**: O comando `cp` (copy) é usado para copiar arquivos e diretórios.

#### **cp básico**

-----

Copia um arquivo para outro local:

```bash
cp arquivo.txt /destino/
```

Copia um arquivo com um novo nome:

```bash
cp arquivo.txt novo-nome.txt
```

Copia múltiplos arquivos para um diretório:

```bash
cp arquivo1.txt arquivo2.txt /destino/
```

#### **Opções do cp**

**-r ou -R ou --recursive**
Copia diretórios e seus conteúdos recursivamente.

```bash
cp -r diretorio-origem diretorio-destino
```

**-v ou --verbose**
Mostra os arquivos sendo copiados.

```bash
cp -v arquivo.txt /destino/
```

**-u ou --update**
Copia o arquivo apenas se o arquivo de origem for mais novo que o de destino.

```bash
cp -u arquivo.txt backup/
```

**-i ou --interactive**
Pergunta antes de sobrescrever um arquivo existente no destino.

```bash
cp -i arquivo.txt destino/
```

**-p ou --preserve**
Preserva atributos como data de modificação, permissões e propriedade do arquivo original.

```bash
cp -p arquivo.txt backup/
```

#### **Combinações úteis**

-----

Copia um diretório recursivamente, preservando todos os atributos e mostrando detalhes:

```bash
cp -rpv origem destino
```

Copia um arquivo e cria um backup numerado se o arquivo de destino já existir:

```bash
cp --backup=numbered arquivo.txt destino/
```

-----
<a id="mv"></a>
### mv

  * **O que é**: O comando `mv` (move) é usado para mover ou renomear arquivos e diretórios.

#### **mv básico**

-----

Move/renomeia um arquivo:

```bash
mv arquivo.txt novo-nome.txt
```

Move um arquivo para um diretório:

```bash
mv arquivo.txt /destino/
```

Move múltiplos arquivos para um diretório:

```bash
mv arquivo1.txt arquivo2.txt /destino/
```

#### **Opções do mv**

**-v ou --verbose**
Mostra os arquivos sendo movidos.

```bash
mv -v arquivo.txt /destino/
```

**-i ou --interactive**
Pergunta antes de sobrescrever um arquivo existente.

```bash
mv -i arquivo.txt destino/
```

**-u ou --update**
Move o arquivo apenas se o de origem for mais novo que o de destino.

```bash
mv -u arquivo.txt backup/
```

**-n ou --no-clobber**
Não sobrescreve arquivos existentes no destino.

```bash
mv -n arquivo.txt destino/
```

#### **Combinações úteis**

-----

Move arquivos com confirmação e detalhes.

```bash
mv -iv arquivos* /destino/
```

-----
<a id="touch"></a>
### touch

  * **O que é**: O comando `touch` é usado para criar arquivos vazios ou para atualizar o timestamp (data e hora de acesso/modificação) de um arquivo existente.

#### **touch básico**

-----

Cria um arquivo vazio:

```bash
touch novo-arquivo.txt
```

Cria múltiplos arquivos:

```bash
touch arquivo1.txt arquivo2.txt arquivo3.txt
```

Atualiza o timestamp de um arquivo existente para a data e hora atual:

```bash
touch arquivo-existente.txt
```

#### **Opções do touch**

**-c ou --no-create**
Evita a criação do arquivo se ele não existir.

```bash
touch -c arquivo-que-pode-nao-existir.txt
```

**-t**
Define um timestamp específico. O formato é `[[CC]YY]MMDDhhmm[.ss]`.

```bash
touch -t 202312251430.30 arquivo.txt
```

**-r ou --reference**
Usa o timestamp de outro arquivo como referência para a atualização.

```bash
touch -r arquivo-referencia.txt arquivo-novo.txt
```

</details>

-----

<a id="capitulo-4"></a>

## Capítulo 4: Visualização de Arquivos

<details>
<summary>Clique para expandir o conteúdo sobre cat, less, head e tail</summary>

<a id="cat"></a>
### cat

  * **O que é**: O comando `cat` (concatenate) exibe o conteúdo de arquivos. É ideal para arquivos pequenos, pois mostra todo o conteúdo de uma vez.

#### **cat básico**

-----

Mostra o conteúdo de um arquivo:

```bash
cat arquivo.txt
```

Mostra o conteúdo de múltiplos arquivos em sequência:

```bash
cat arquivo1.txt arquivo2.txt
```

#### **Opções do cat**

**-n ou --number**
Numera todas as linhas de saída.

```bash
cat -n arquivo.txt
```

**-b ou --number-nonblank**
Numera apenas as linhas que não estão em branco.

```bash
cat -b arquivo.txt
```

**-A ou --show-all**
Mostra caracteres não imprimíveis e espaços como `$` no final da linha e `^I` para tabulações.

```bash
cat -A arquivo.txt
```

**-s ou --squeeze-blank**
Remove linhas em branco duplicadas.

```bash
cat -s arquivo.txt
```

#### **Uso com redirecionamento**

-----

Cria um novo arquivo com o conteúdo digitado a partir da entrada padrão.

```bash
cat > novo-arquivo.txt
```

Adiciona o conteúdo digitado ao final de um arquivo existente:

```bash
cat >> arquivo-existente.txt
```

Concatena o conteúdo de vários arquivos em um novo arquivo:

```bash
cat arquivo1.txt arquivo2.txt > arquivo-concatenado.txt
```

-----
<a id="less"></a>
### less

  * **O que é**: O comando `less` permite visualizar arquivos de texto de forma paginada. É a ferramenta ideal para inspecionar arquivos grandes, pois ele carrega apenas o conteúdo visível, economizando memória.

#### **less básico**

-----

Visualiza um arquivo, permitindo navegação página por página:

```bash
less arquivo.txt
```

#### **Navegação no less**

  - **Espaço**: avança para a próxima página.
  - **b**: volta para a página anterior.
  - **q**: sai do programa.
  - **/**`texto`: busca por um texto específico.
  - **n**: vai para a próxima ocorrência da busca.
  - **G**: vai para o final do arquivo.
  - **g**: volta para o início do arquivo.

#### **Opções do less**

**-N**
Mostra números de linha à esquerda.

```bash
less -N arquivo.txt
```

**-S**
Não quebra linhas longas, permitindo rolar para os lados.

```bash
less -S arquivo-com-linhas-longas.txt
```

**-i**
Busca por texto sem diferenciar maiúsculas e minúsculas.

```bash
less -i arquivo.txt
```

-----
<a id="head"></a>
### head

  * **O que é**: O comando `head` exibe as primeiras linhas de um arquivo de texto. Por padrão, ele mostra as 10 primeiras linhas.

#### **head básico**

-----

Mostra as primeiras 10 linhas:

```bash
head arquivo.txt
```

#### **Opções do head**

**-n ou --lines**
Especifica o número de linhas a serem exibidas.

```bash
head -n 20 arquivo.txt
```

Forma abreviada:

```bash
head -20 arquivo.txt
```

**-c ou --bytes**
Mostra um número específico de bytes do início do arquivo.

```bash
head -c 100 arquivo.txt
```

#### **Múltiplos arquivos**

-----

Mostra o cabeçalho de múltiplos arquivos, um após o outro.

```bash
head arquivo1.txt arquivo2.txt
```

-----
<a id="tail"></a>
### tail

  * **O que é**: O comando `tail` exibe as últimas linhas de um arquivo. Por padrão, ele mostra as 10 últimas linhas. É muito usado para monitorar arquivos de log em tempo real.

#### **tail básico**

-----

Mostra as últimas 10 linhas:

```bash
tail arquivo.txt
```

#### **Opções do tail**

**-n ou --lines**
Especifica o número de linhas a serem exibidas.

```bash
tail -n 20 arquivo.txt
```

Forma abreviada:

```bash
tail -20 arquivo.txt
```

**-f ou --follow**
Monitora o arquivo em tempo real, exibindo novas linhas assim que são adicionadas. Ideal para logs.

```bash
tail -f /var/log/syslog
```

**-c ou --bytes**
Mostra um número específico de bytes do final do arquivo.

```bash
tail -c 100 arquivo.txt
```

#### **Combinações úteis**

-----

Monitora as últimas 50 linhas de um arquivo em tempo real:

```bash
tail -n 50 -f arquivo.log
```

Mostra o conteúdo do arquivo a partir da linha 10:

```bash
tail -n +10 arquivo.txt
```

</details>

-----

<a id="capitulo-5"></a>

## Capítulo 5: Busca e Localização

<details>
<summary>Clique para expandir o conteúdo sobre find, grep, which e locate</summary>

### Diferenças entre os comandos de busca

  * **`grep`**: Procura por **texto** dentro de arquivos. Ele não se importa com nomes de arquivos ou localização, apenas com o conteúdo.
  * **`find`**: Procura por **arquivos e diretórios** com base em critérios como nome, tipo, tamanho ou data. Ele navega pela estrutura de diretórios em tempo real.
  * **`which`**: Procura por **comandos executáveis** no seu `$PATH`. É usado para descobrir a localização de um programa.
  * **`locate`**: Procura por **arquivos e diretórios** em um banco de dados pré-indexado. É extremamente rápido, mas a informação pode não estar 100% atualizada. O banco de dados é atualizado manualmente com o comando `updatedb`.

<a id="find"></a>
### find

  * **O que é**: O comando `find` é uma ferramenta poderosa para localizar arquivos e diretórios em uma hierarquia de diretórios.

#### **find básico**

-----

Busca e lista todos os arquivos e diretórios a partir do diretório atual (`.`).

```bash
find .
```

Busca por um nome de arquivo específico no diretório atual:

```bash
find . -name "arquivo.txt"
```

Busca por nome, ignorando maiúsculas e minúsculas:

```bash
find . -iname "*.TXT"
```

#### **Busca por tipo**

**-type f** (arquivos regulares)

```bash
find . -type f
```

**-type d** (diretórios)

```bash
find . -type d
```

**-type l** (links simbólicos)

```bash
find . -type l
```

#### **Busca por tamanho**

Busca arquivos maiores que 100 MB:

```bash
find . -size +100M
```

Busca arquivos menores que 1 kilobyte:

```bash
find . -size -1k
```

Busca arquivos com exatamente 50 bytes:

```bash
find . -size 50c
```

#### **Busca por tempo**

Busca arquivos modificados nos últimos 7 dias:

```bash
find . -mtime -7
```

Busca arquivos acessados há mais de 30 dias:

```bash
find . -atime +30
```

#### **Executar ações**

Executa um comando em cada arquivo encontrado. O `{}` representa o nome do arquivo, e `\;` encerra o comando.

```bash
find . -name "*.tmp" -exec rm {} \;
```

Remove os arquivos encontrados. Esta é uma forma mais eficiente que a anterior.

```bash
find . -name "*.log" -delete
```

#### **Combinações úteis**

-----

Busca arquivos `.txt` modificados na última semana e que são do tipo arquivo.

```bash
find . -name "*.txt" -type f -mtime -7
```

Busca diretórios vazios:

```bash
find . -type d -empty
```

Busca arquivos grandes (maiores que 100MB) e mostra seus detalhes de forma legível.

```bash
find . -type f -size +100M -exec ls -lh {} \;
```

-----
<a id="grep"></a>
### grep

  * **O que é**: O comando `grep` (global regular expression print) é usado para buscar por padrões de texto dentro de arquivos.

#### **grep básico**

-----

Busca a palavra "palavra" em um arquivo:

```bash
grep "palavra" arquivo.txt
```

Busca a palavra em todos os arquivos `.txt` do diretório:

```bash
grep "palavra" *.txt
```

#### **Opções do grep**

**-i ou --ignore-case**
Realiza a busca sem diferenciar maiúsculas e minúsculas.

```bash
grep -i "palavra" arquivo.txt
```

**-r ou --recursive**
Busca de forma recursiva em todos os arquivos de um diretório e seus subdiretórios.

```bash
grep -r "palavra" /caminho/diretorio
```

**-n ou --line-number**
Mostra o número da linha onde o padrão foi encontrado.

```bash
grep -n "palavra" arquivo.txt
```

**-v ou --invert-match**
Mostra as linhas que **NÃO** contêm o padrão de busca.

```bash
grep -v "palavra" arquivo.txt
```

**-c ou --count**
Conta quantas vezes o padrão foi encontrado.

```bash
grep -c "palavra" arquivo.txt
```

**-l ou --files-with-matches**
Lista apenas o nome dos arquivos que contêm o padrão, sem mostrar o conteúdo das linhas.

```bash
grep -l "palavra" *.txt
```

**-A, -B, -C** (contexto)
Mostra linhas adicionais: `-A` (after) mostra as próximas N linhas, `-B` (before) mostra as anteriores, e `-C` (context) mostra ambas.

```bash
grep -A 3 -B 2 "palavra" arquivo.txt
```

#### **Expressões regulares**

-----

Busca linhas que começam com a palavra "palavra":

```bash
grep "^palavra" arquivo.txt
```

Busca linhas que terminam com a palavra "palavra":

```bash
grep "palavra$" arquivo.txt
```

Busca `p` seguido por qualquer caractere e depois `lavra`:

```bash
grep "p.lavra" arquivo.txt
```

#### **Combinações úteis**

-----

Busca recursiva, case-insensitive, com números de linha no diretório atual:

```bash
grep -rin "palavra" .
```

Busca um arquivo de configuração, ignorando linhas de comentário (que começam com `#`):

```bash
grep -v "^#" arquivo-config.txt
```

-----
<a id="which"></a>
### which

  * **O que é**: O comando `which` localiza um comando executável no seu sistema, informando o caminho completo para o seu arquivo binário. Ele verifica os diretórios listados na sua variável de ambiente `$PATH`.

#### **which básico**

-----

Mostra o caminho completo do comando `ls`:

```bash
which ls
```

Localiza múltiplos comandos:

```bash
which ls pwd cd
```

#### **Opções do which**

**-a**
Mostra todos os caminhos para o comando, mesmo que ele apareça em múltiplos diretórios no `$PATH`.

```bash
which -a python
```

-----
<a id="locate"></a>
### locate

  * **O que é**: O comando `locate` é um utilitário de busca rápida de arquivos. Diferente do `find`, ele não busca no sistema de arquivos em tempo real, mas sim em um banco de dados pré-indexado, o que o torna muito mais rápido. Por isso, os resultados podem não estar totalmente atualizados.

#### **locate básico**

-----

Busca um arquivo por nome, de forma rápida:

```bash
locate arquivo.txt
```

Busca sem diferenciar maiúsculas e minúsculas:

```bash
locate -i ARQUIVO.TXT
```

#### **Opções do locate**

**-c ou --count**
Apenas conta quantos arquivos foram encontrados, sem listá-los.

```bash
locate -c "*.pdf"
```

**-l ou --limit**
Limita o número de resultados exibidos.

```bash
locate -l 10 "*.jpg"
```

#### **Atualizar banco de dados**

-----

Para garantir que os resultados do `locate` estejam atualizados, é necessário atualizar o banco de dados. Este comando geralmente requer privilégios de root.

```bash
sudo updatedb
```

</details>

-----

<a id="capitulo-6"></a>

## Capítulo 6: Permissões e Propriedades

<details>
<summary>Clique para expandir o conteúdo sobre chmod, chown e chgrp</summary>

### Diferenças entre os comandos

  * **`chmod`**: **Ch**ange **mod**e. Altera as permissões de acesso (leitura, escrita, execução) de arquivos e diretórios.
  * **`chown`**: **Ch**ange **own**er. Altera o proprietário (usuário e/ou grupo) de arquivos e diretórios.
  * **`chgrp`**: **Ch**ange **gr**ou**p**. Altera apenas o grupo de arquivos e diretórios. É uma alternativa mais simples para o `chown` quando a mudança se restringe ao grupo.

<a id="chmod"></a>
### chmod

  * **O que é**: O comando `chmod` (change mode) é usado para alterar as permissões de arquivos e diretórios.

#### **chmod básico**

-----

Modo octal - define permissões absolutas:

```bash
chmod 755 arquivo.txt
```

Modo simbólico - adiciona permissão de execução para o proprietário:

```bash
chmod u+x script.sh
```

Remove a permissão de escrita para todos:

```bash
chmod a-w arquivo.txt
```

#### **Valores octais comuns**

  - **755**: `rwxr-xr-x` (proprietário: leitura, escrita, execução; grupo e outros: leitura e execução)
  - **644**: `rw-r--r--` (proprietário: leitura e escrita; grupo e outros: apenas leitura)
  - **600**: `rw-------` (apenas o proprietário pode ler e escrever)
  - **777**: `rwxrwxrwx` (todos podem tudo - **perigoso e desaconselhável**)

#### **Modo simbólico**

**Usuários**

  - **u**: `user` (proprietário)
  - **g**: `group` (grupo)
  - **o**: `others` (outros)
  - **a**: `all` (todos)

**Operações**

  - **+**: adiciona permissão
  - **-**: remove permissão
  - **=**: define a permissão exata, substituindo as anteriores.

**Permissões**

  - **r**: `read` (leitura)
  - **w**: `write` (escrita)
  - **x**: `execute` (execução)

#### **Exemplos simbólicos**

-----

Adiciona permissão de execução para o proprietário:

```bash
chmod u+x script.sh
```

Remove as permissões de escrita para o grupo e outros:

```bash
chmod go-w arquivo.txt
```

Define a permissão de apenas leitura para todos:

```bash
chmod a=r arquivo.txt
```

#### **Opções do chmod**

**-R ou --recursive**
Aplica a alteração de permissões recursivamente em um diretório e seu conteúdo.

```bash
chmod -R 755 diretorio
```

**-v ou --verbose**
Mostra as mudanças realizadas em cada arquivo.

```bash
chmod -v +x script.sh
```

-----
<a id="chown"></a>
### chown

  * **O que é**: O comando `chown` (change owner) é usado para alterar o proprietário de um arquivo ou diretório. Ele também pode alterar o grupo. Geralmente requer privilégios de root.

#### **chown básico**

-----

Muda o proprietário do arquivo:

```bash
sudo chown usuario arquivo.txt
```

Muda o proprietário e o grupo do arquivo:

```bash
sudo chown usuario:grupo arquivo.txt
```

Muda apenas o grupo (sintaxe alternativa):

```bash
sudo chown :grupo arquivo.txt
```

#### **Opções do chown**

**-R ou --recursive**
Aplica a mudança de proprietário e/ou grupo recursivamente.

```bash
sudo chown -R usuario:grupo diretorio
```

**-v ou --verbose**
Mostra os detalhes das mudanças realizadas.

```bash
sudo chown -v usuario arquivo.txt
```

**--reference**
Usa o proprietário e grupo de outro arquivo como referência para a mudança.

```bash
sudo chown --reference=arquivo-referencia.txt arquivo-destino.txt
```

-----
<a id="chgrp"></a>
### chgrp

  * **O que é**: O comando `chgrp` (change group) é usado para alterar o grupo de um arquivo ou diretório. É uma alternativa mais específica para o `chown` quando você precisa mudar apenas o grupo.

#### **chgrp básico**

-----

Muda o grupo do arquivo:

```bash
sudo chgrp grupo arquivo.txt
```

#### **Opções do chgrp**

**-R ou --recursive**
Aplica a mudança de grupo recursivamente.

```bash
sudo chgrp -R grupo diretorio
```

**-v ou --verbose**
Mostra os detalhes das mudanças realizadas.

```bash
sudo chgrp -v grupo arquivo.txt
```

</details>

-----

<a id="capitulo-7"></a>

## Capítulo 7: Informações do Sistema

<details>
<summary>Clique para expandir o conteúdo sobre df, du, ps e top</summary>

<a id="df"></a>
### df

  * **O que é**: O comando `df` (disk free) exibe a quantidade de espaço livre e usado nos sistemas de arquivos montados.

#### **df básico**

-----

Mostra o espaço em disco de todos os sistemas de arquivos:

```bash
df
```

#### **Opções do df**

**-h ou --human-readable**
Mostra os tamanhos em um formato legível para humanos (ex: GB, MB).

```bash
df -h
```

**-T ou --print-type**
Mostra o tipo do sistema de arquivos (ex: `ext4`, `xfs`).

```bash
df -T
```

**-i ou --inodes**
Mostra informações sobre os inodes (estruturas de dados que armazenam informações sobre arquivos).

```bash
df -i
```

#### **Combinações úteis**

-----

Informações completas e legíveis sobre o sistema de arquivos:

```bash
df -hT
```

Informações apenas para um diretório específico:

```bash
df -h /home
```

-----
<a id="du"></a>
### du

  * **O que é**: O comando `du` (disk usage) estima o uso de espaço em disco de arquivos e diretórios.

#### **du básico**

-----

Mostra o uso do disco do diretório atual, incluindo subdiretórios:

```bash
du
```

#### **Opções do du**

**-h ou --human-readable**
Mostra os tamanhos em formato legível (ex: GB, MB).

```bash
du -h
```

**-s ou --summarize**
Mostra apenas o total de uso do disco para o diretório, sem detalhar o conteúdo.

```bash
du -s
```

**-a ou --all**
Inclui arquivos individuais na listagem.

```bash
du -a
```

**-c ou --total**
Mostra o total geral ao final da listagem.

```bash
du -c
```

**--max-depth**
Limita a profundidade da varredura de diretórios.

```bash
du --max-depth=1
```

#### **Combinações úteis**

-----

Mostra um resumo legível do uso de disco do diretório atual:

```bash
du -sh
```

Lista os 10 maiores diretórios (requer `sort` e `head`):

```bash
du -h | sort -hr | head -10
```

Faz uma análise do uso de disco apenas no primeiro nível de subdiretórios:

```bash
du -h --max-depth=1
```

-----
<a id="ps"></a>
### ps

  * **O que é**: O comando `ps` (process status) exibe uma lista de processos ativos no sistema em um determinado momento.

#### **ps básico**

-----

Mostra os processos em execução no terminal atual:

```bash
ps
```

#### **Opções do ps**

**aux**
Mostra todos os processos de todos os usuários, incluindo os que não estão associados a um terminal.

```bash
ps aux
```

**-ef**
Mostra todos os processos em um formato completo, com mais informações.

```bash
ps -ef
```

**-u**
Mostra os processos de um usuário específico.

```bash
ps -u usuario
```

#### **Combinações úteis**

-----

Busca um processo específico pelo nome:

```bash
ps aux | grep nome-do-processo
```

Lista processos ordenados pelo uso de CPU (do maior para o menor):

```bash
ps aux --sort=-pcpu
```

Lista processos ordenados pelo uso de memória:

```bash
ps aux --sort=-pmem
```

-----
<a id="top"></a>
### top

  * **O que é**: O comando `top` fornece uma visão dinâmica e em tempo real dos processos em execução no sistema, com informações sobre uso de CPU e memória.

#### **top básico**

-----

Inicia o monitor de sistema em tempo real:

```bash
top
```

#### **Comandos interativos no top**

  - **q**: sair do programa.
  - **k**: matar um processo (pede o PID).
  - **M**: ordenar a lista por uso de memória.
  - **P**: ordenar a lista por uso de CPU.
  - **1**: alternar entre a visão de um único núcleo de CPU ou de todos os núcleos.
  - **h**: exibir a tela de ajuda.

#### **Opções do top**

**-p**
Monitora um processo com um PID específico:

```bash
top -p 1234
```

**-u**
Monitora os processos de um usuário específico:

```bash
top -u usuario
```

**-n**
Define o número de atualizações que o programa deve fazer antes de sair.

```bash
top -n 5
```

#### **Alternativas modernas**

-----

`htop` é uma alternativa mais amigável e interativa ao `top`:

```bash
htop
```

</details>

-----



## Capítulo 8: Diferenças entre Distribuições (Gerenciadores de Pacotes)

<details>
<summary>Clique para expandir o conteúdo sobre Gerenciadores de Pacotes</summary>

<a id="capitulo-8"></a>

Os **gerenciadores de pacotes** simplificam a instalação, atualização, remoção e gerenciamento de software no Linux.  
Eles são um dos pontos mais importantes de **diferença entre distribuições**.

---

## 🔎 Como descobrir qual distribuição Linux você está usando

O arquivo mais comum é o `/etc/os-release`, mas nem sempre ele existe (principalmente em sistemas antigos).  
Outras formas:

```bash
# Método padrão (sistemas modernos)
cat /etc/os-release

# Em sistemas baseados em Red Hat
cat /etc/redhat-release

# Em sistemas antigos (Debian, Ubuntu)
cat /etc/issue

# Se nada disso funcionar, use o comando 'uname'
uname -a
````

👉 Se todos os métodos falharem, é possível **descobrir pelo gerenciador de pacotes disponível**.
Exemplo: se `apt` existe, provavelmente é Debian/Ubuntu; se `dnf` ou `yum`, Red Hat/Fedora; se `pacman`, Arch.

---

## 📦 Principais Gerenciadores de Pacotes

### Debian/Ubuntu → `apt` / `apt-get`

Conhecido pela **estabilidade** e vasta base de pacotes.

```bash
sudo apt update               # Atualiza a lista de pacotes
sudo apt upgrade              # Atualiza pacotes instalados
sudo apt install nome_do_pacote   # Instala um pacote
sudo apt remove nome_do_pacote    # Remove um pacote
```

---

### Red Hat, Fedora, CentOS → `dnf` / `yum`

* `yum` foi o predecessor
* `dnf` é a versão mais moderna, usada nas distros atuais.

```bash
sudo dnf check-update             # Verifica por atualizações
sudo dnf upgrade                  # Atualiza pacotes
sudo dnf install nome_do_pacote   # Instala um pacote
sudo dnf remove nome_do_pacote    # Remove um pacote
```

👉 Nos sistemas mais antigos ainda pode aparecer `yum`:

```bash
sudo yum check-update
sudo yum upgrade
```

---

### Arch Linux → `pacman`

Famoso por sua **simplicidade e velocidade**.

```bash
sudo pacman -Syu                 # Atualiza repositórios e pacotes
sudo pacman -S nome_do_pacote    # Instala um pacote
sudo pacman -R nome_do_pacote    # Remove um pacote
```

---

## 💡 Dica prática

Se você acabou de acessar um sistema desconhecido e quer saber **qual gerenciador está disponível**, teste:

```bash
command -v apt
command -v dnf
command -v yum
command -v pacman
```

O primeiro que retornar um caminho (ex: `/usr/bin/apt`) indica o gerenciador de pacotes usado pela distro.

</details>


---

-----



## Capítulo 9: Variáveis e Histórico

<details>
<summary>Clique para expandir o conteúdo sobre variáveis de ambiente e histórico de comandos</summary>

<a id="capitulo-9"></a>
### Variáveis de Ambiente Essenciais

  * **O que são**: Variáveis de ambiente são valores nomeados que influenciam o comportamento de programas e do shell.

  * **`PATH`**:

      * Mostra os diretórios onde o shell procura por comandos executáveis.

    <!-- end list -->

    ```bash
    echo $PATH
    ```

      * Adiciona um novo diretório ao seu `$PATH`:

    <!-- end list -->

    ```bash
    export PATH=$PATH:/novo/diretorio
    ```

  * **`HOME`**:

      * Caminho para o diretório home do usuário atual.

    <!-- end list -->

    ```bash
    echo $HOME
    ```

  * **`USER` ou `USERNAME`**:

      * Nome do usuário atual.

    <!-- end list -->

    ```bash
    echo $USER
    ```

  * **`PWD`**:

      * Caminho para o diretório de trabalho atual.

    <!-- end list -->

    ```bash
    echo $PWD
    ```

  * **`OLDPWD`**:

      * Caminho para o diretório anterior.

    <!-- end list -->

    ```bash
    echo $OLDPWD
    ```

-----

### Histórico de Comandos

  * **O que é**: O histórico de comandos armazena os comandos que você executou, permitindo reexecutá-los ou editá-los facilmente.

#### **history básico**

-----

Mostra o histórico de comandos:

```bash
history
```

Executa um comando pelo seu número no histórico:

```bash
!123
```

Executa o último comando digitado:

```bash
!!
```

Executa o último comando que começava com 'git':

```bash
!git
```

#### **Busca no histórico**

-----

Busca interativa (pressione `Ctrl+R` e comece a digitar):

```
(reverse-i-search)`git': git status
```

Limpa todo o histórico da sessão atual:

```bash
history -c
```

</details>
