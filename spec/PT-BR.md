# Koins

## 1. Introdução

### 1.1. Objetivo

O objetivo deste documento é registrar os requisitos básicos para um aplicativo de controle financeiro pessoal *online*. Ele contém uma visão geral dos itens mais relevantes que este projeto deve conter.

Público-alvo: Pessoas que almejam um controle de finanças simples de usar e fácil de gerenciar, e que os aplicativos de controle de finanças existentes não atendam. O aplicativo irá atender os mais diversos tipos de públicos, principalmente por causa do recurso de *plugins*, que permitirá a extensão do aplicativo para qualquer tipo de funcionalidade.

### 1.2. Materiais de referência

Como referências foram tomadas experiências pessoais obtidas com diversos aplicativos com o mesmo intuito deste.

Dois que podem ser citados como ótimas referências para o projeto são o *Toshl* (https://toshl.com/), que propõe uma forma mais descontraída e bem humorada de gerenciar suas finanças, e o *Finance41* (https://finance41.com/), que no caso tem uma interface mais simples e uma ótima usabilidade.

## 2. Descrição geral do produto

### 2.1. Visão geral

Finanças pessoais são um assunto muito conversado atualmente. Cada vez mais as pessoas estão precisando controlar sua vida financeira. Pensando nisso, vários aplicativos de controle de finanças pessoais foram criados, com o foco de atingir essas necessidades emergentes.

O principal foco deles é o registro de gastos e controle categorizado deles, podendo registrar várias *wallets* diferentes, e controlar elas separadamente. Alguns ainda propõe certos tipos de controles financeiros pessoais bem difundidos no mundo, como o conceito de *budgets*. Muitos dos sistemas têm vários tipos de gráficos; mensais, por categoria e diversos outros.

Vários tem uma maneira de importar e exportar dados para formatos conhecidos, mas nenhum deles tem uma abertura grande para, por exemplo, desenvolvimento de *plugins* para importar, exportar ou tratar informações de outras maneiras. Este é o diferencial deste projeto.

O aplicativo deve ter uma *API* de alto nível para facilitar a extensão, e suportar implementações de *plugins* para ele. Os *plugins* serão um diferencial importante do aplicativo, já que com eles poderão ser gerados gráficos e outros tipos de editores ou até mesmo integrações com outros serviços, como email, redes sociais, serviços de pagamento *online* e até *internet banking*.

Fora este diferencial, o aplicativo deve ter uma maneira de diferenciar *lançamentos* e *orçamentos*. Coisa que os demais aplicativos analisados também não tinham, ou tinham algo parecido, mas não atendiam certas necessidades. Por exemplo, quando tenho uma dívida mensal que pode variar (telefone por exemplo) devo ter um registro de orçamento. Nos outros aplicativos isto é feito com um lançamento com data no futuro, e quando a data do pagamento chegar, o valor do lançamento, que deve ser colocado fixo, fica do jeito que está, e deve ser editado manualmente se não foi o planejado. Assim o registro do planejado para aquele mês se perde. Com orçamentos e lançamentos separados, pode-se ter um controle de orçado e realizado mais preciso.

### 2.2. Stakeholder / Usuários

Basicamente qualquer pessoa que saiba navegar na internet, do mais leigo ao com conhecimentos mais avançados. Outras pessoas que irão usar o produto são desenvolvedores que pretendem estendê-lo por meio dos plugins.

### 2.3. Benefícios do produto

1. Rapidez no cadastro de lançamentos
1. Interface visual limpa e fácil de usar
1. Consulta rápida nos lançamentos
1. Desenvolvimento colaborativo de *plugins* para o site

### 2.4. Limitações do produto

1. Não disponibilizará gráficos para consulta, somente a partir de extensões
1. O site não se responsibilizará por *plugins* que foram habilitados e usaram seus dados de maneiras indevidas

## 3. Especificação de requisitos

### 3.1 Requisitos funcionais

**RF01** O aplicativo deve permitir o registro de usuário

O registro de usuário deve pedir os seguintes dados: *login*, email, senha, *wallet* padrão e moeda principal. Onde o *login* é uma chave única.

**RF02** O aplicativo deve enviar email de confirmação de registro de usuário

Ao registrar o usuário, deve ser mandado um email ao endereço registrado, com um link para a página de confirmação de email.

**RF03** O aplicativo deve permitir o registro de *wallet*

Uma *wallet* representa uma conta onde o dinhero pode ser guardado pelo usuário, como por exemplo a carteira, conta corrente, conta poupança. O registro de *wallet* deve pedir os seguintes dados: nome e valor inicial.

**RF04** O aplicativo deve permitir transferências entre *wallets*

A transferência entre *wallets* deve ser transparente, onde é feito um lançamento de débito na *wallet* origem, e outro de crédito na *wallet* destino. O registro de transferência deve pedir os seguintes dados: valor, *wallet* origem, *wallet* destino e *tags*

**RF05** O aplicativo deve permitir o registro de *tags*

Uma *tag* é um classificador que poderá ser usado no registro de lançamento ou orçamento, por exemplo, "aluguel", "gasolina", "supermercado". O registro de *tag* deve pedir apenas o campo nome. O registro da *tag* pode ser feito informando uma tag que não existe na hora de registrar um lançamento ou um orçamento.

**RF06** O aplicativo deve permitir o registro de lançamentos do usuário

O registro de lançamento deve pedir os seguintes dados: valor, *tags*, anotações, data e *wallet*.

**RF07** O aplicativo deve permitir o registro de orçamentos do usuário

O registro de orçamento deve pedir os seguintes dados: valor, *tags*, data, *wallet* e *frequência*. Neste caso, *wallet* e frequência são campos opcionais.

**RF08** O aplicativo deve ter um reconhecedor de frases para utilizar texto plano para inserção de registros

A partir de um reconhecedor de frases, o usuário deve poder digitar uma frase do tipo "gastei 15 reais com comida", e o sistema deve inserir um registro de lançamento com valor de 15 reais e com a tag "comida" aplicada a ele. Os tipos de registros que podem ser inseridos a partir de texto são os lançamentos, orçamentos e transferências entre *wallets*.

**RF09** O aplicativo deve permitir pesquisa rápida nos lançamentos e orçamentos

A pesquisa rápida pode ser feita utilizando o reconhecedor de frases também.

**RF10** O aplicativo deve permitir cadastro geral de moedas

O cadastro deve ser colaborativo, onde cada um pode cadastrar suas moedas.

**RF11** O aplicativo deve disponibilizar uma *API* alto nível para desenvolvimento de *plugins*

Deve ser uma *API* *Ruby* com comandos de criação, leitura, edição e remoção básicos. Os plugins serão todos escritos em *Ruby*, sendo que eles serão basicamente uma *gem* *Ruby*

**RF12** O aplicativo deve fazer upload de *plugins*

O upload de plugins pode ser feito de 2 maneiras distintas:

1. disponibilizar no repositório do *RubyGems* e informar apenas o nome da gem;
1. disponibilizar num repositório *GitHub*, informar o caminho do repositório (usuário/repositório) e o *branch* produção (por padrão o *branch* "koins").

**RF13** O aplicativo deve permitir pesquisa rápida na lista de *plugins* disponíveis

A pesquisa deve filtrar por nome e descrição.

**RF14** O aplicativo deve permitir o usuário associar os *plugins* desejados a sua conta

O usuário deve poder selecionar o plugin e associá-lo a sua conta.

### 3.2. Requisitos não funcionais

**RNF01** O aplicativo deve rodar nos navegadores: *Firefox*, *Chrome*, *Safari* e *Opera*.

**RNF02** O aplicativo deve rodar nos sistemas operacionais: *Windows*, *Linux* e *Mac*.

**RNF03** O aplicativo deve ser desenvolvido com o framework *Rails* da linguagem *Ruby*.

**RNF04** O aplicativo deve utilizar o banco de dados *PostgreSQL*.

**RNF05** O aplicativo deve ser desenvolvido utilizando o padrão *MVC*.

**RNF06** A interface gráfica do aplicativo deve ser limpa e direta.

**RNF07** O sistema deve utilizar senhas de acesso para o controle seguro da aplicação.

**RNF08** O sistema deve utilizar o protocolo *SMTP*.

### 3.3. Regras de negócio

**RN01** Ao adicionar um *plugin* a sua conta, o usuário deve poder escolher se dá as permissões de leitura e escrita a ele.

**RN02** O aplicativo só deve permitir o usuário selecionar *plugins* se ele tiver confirmado o cadastro.

**RN03** Se, ao registrar um lançamento, não for informada uma *wallet*, ele deve ir para a *wallet* padrão

## 4. Lista de riscos

1. Mudança de requisitos
1. Sobrecarga nos servidores
1. Complexidade do desenvolvimento de *plugins* com Rails

## 5. Glossário

| Item                    | Tipo    | Significado                           |
|:-----------------------:|:-------:|---------------------------------------|
| API                     | Técnico | Sigla de Application Programming Interface (Interface de programação da aplicação), é uma biblioteca que disponibiliza métodos públicos para extensão ou integração com a aplicação
| Budget                  | Negócio | Conceito de economia pessoal que consiste em um valor planejado de gastos com certa dívida ou tipo de dívida
| Chrome                  | Técnico | Navegador de Internet
| Firefox                 | Técnico | Navegador de Internet
| Frequência do orçamento | Técnico | Frequência de repetição do orçamento, basicamente, de quanto em quanto tempo o orçamento se repete
| Gem                     | Técnico | Pacote de fontes Ruby
| Git                     | Técnico | Gerenciador de versões de arquivos muito usado globalmente pela comunidade open source
| GitHub                  | Técnico | Host *online* de repositórios *git*
| Internet Banking        | Negócio | Recursos de determinados bancos para acesso a serviços bancários via web
| Lançamento              | Negócio | Dívida ou lucro ocorrido, ou que irá ocorrer, mas com um valor definido
| Linux                   | Técnico | Sistema operacional
| Login                   | Técnico | Apelido que o usuário pode utilizar para entrar no site
| Mac                     | Técnico | Sistema operacional
| MVC                     | Técnico | Padronização de modelo de desenvolvimento de sistemas
| Opera                   | Técnico | Navegador de Internet
| Orçamento               | Negócio | Dívida ou lucro planejado, um orçamento é um planejamento prévio de dívidas que podem ou não ocorrer, e também podem mudar de valor
| Plugin                  | Técnico | Extensão que pode ser adicionada ao aplicativo
| PostgreSQL              | Técnico | Banco de dados estrutural
| Rails                   | Técnico | Framework para desenvolvimento de sites web dinâmicos
| Ruby                    | Técnico | Linguagem dinâmica e alto nível de programação
| RubyGems                | Técnico | Host global padrão de gems Ruby, site: http://rubygems.org/
| Safari                  | Técnico | Navegador de Internet
| SMTP                    | Técnico | Protocolo de transferência de email
| Tag                     | Negócio | Marcador para classificação dos lançamentos e orçamentos
| Wallet                  | Negócio | Carteira em inglês, basicamente um lugar onde o dinheiro pode estar guardado, sejam contas bancárias, cartões de vale, etc
