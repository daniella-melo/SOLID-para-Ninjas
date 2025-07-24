# Orientação a Objetos e SOLID para Ninjas - Projetando classes flexíveis

## Capítulo 1 - Orientação a Objetos, pra que te quero?
- código procedural (implementação é o que importa) x linguagem orientada a objetos (implementação é fundamental, mas pensamento maior no projeto de classes)
- OO como um quebra cabeça (p. 2)
- Problemas típicos de código: propagação de mudanças, repetições desnecessárias e otimização de reúso de código
- Acoplamento, coesão e encapsulamento
- Abstrações e flexibilizações
- "[...] facilitar a evolução e manutenção de nossos sistemas" (p.2)

## Capítulo 2 - A coesão e o tal do SRP
- Coesão, em definição é a ligação entre as partes de um texto, criando harmonia e unidade, permitindo fluidez e compreensão.
- "[...] uma classe coesa é aquela que possui uma única responsabilidade" ou, <b> uma única razão para mudar </b>
- Focar na coesão e ter em mente o SRP (Single Responsability Principle) cria classes mais simples de serem mantidas e de reuso maior
- quanto mais código numa classe, mais chance de problemas e erros (ex: uma regra influenciando na outra, muitas responsabilidades acopladas)

#### Exemplo de ferramentas para construir coesão com SRP:
-   abstrações ("esqueletos" generalizavéis)
- isolamentos (menor chance de uma mudança de regra afetar outra) (p. 8) - métodos publicos e privados, classes, contextos, pastas
- responsabilidades separadas (classes menores, melhores e mais coesas)
- encapsulamento (também auxilia no problema da propagação de alterações, deixando "a decisão de design mais clara (p.11)")
    + lembrar o exemplo do livro quanto à classe enum Cargo que recebe uma instância que implementa a interface RegraDeCalculo()
    + sinais de alerta para um possível mal encapsulamento: uma mudança precisar ser feita em muitos pontos do código (dependências implicitas)
- métodos privados como forma de melhora de legebilidade de métodos públicos

### Recordando MVC
- <b>M</b> (Camanda de Modelo): regras de negócio, é o universo do problema
- <b>V</b> (Camada de Visualização): interface com o usuário
- <b>C</b> (Camada de Controlador): ligação entre a interação do usuário e as regras de negócio do modelo

### Inveja da outra classe (Seção 2.7)
- Feature Envy: Funções que deveriam ser de responsabilidade de uma classe sendo feitas por outra
- O comportamento do objeto deveria ser coordenado pela sua classe de domínio

### O SRP
- <b> Single Responsability Principle</b>
- "[...] A classe deve ter uma, e apenas uma, razão para mudar" (p.19)
- "Dois comportamentos "pertencem" ao mesmo conceito/responsabilidade se ambos mudam juntos" (p. 20)

### Separação do Modelo, Infraestrutura, e a tal da Arquitetura Hexagonal
- "A sugestão é para que você separe ao máximo toda e qualquer  infraestrutura (seja sem seu framework MVC, ou seu framework de persistência ou mesmo a biblioteca que você usa para criar serviços web) dos seus modelos e regras de negócio" (p.21)
- As regras de negócio são o que movem e param o software (p.21)
#### Arquitetura Hexagonal
- <b> ports and adpaters </b>
- portas (classes do domínio); adaptadores (classes que fazem a ponte entre mundos diferentes) (p.21)

## Capítulo 3 - Acoplamento e o tal do DIP
"Tenha classes que são muito coesas e pouco acopladas"

### Acoplamento
- Acoplamento = dependência
- Problemática: o grande problema do acoplamento é que uma mudança em qualquer uma das classes pode impactar em mudanças na classe principal (p.25) 
- Muitas dependências = todas essas dependêcias podem propagar problemas para a classe principal, tornando ela <b>mais frágil e fácil de quebrar</b>
- Acoplamento são necessários, mas é preciso fugir de acoplamentos perigosos


### 3.2 Estabilidade de Classes
- <b>""acoplamento bom": a dependência é estável"</b> (p.26)
- Ou seja, é melhor que a classe dependa de outras que são mais estáveis, assim <b> a chance dessa dependência propagar um erro, uma mudança, é menor </b>

### 3.3 Buscando poro classes estáveis
- <b>Interfaces são um bom caminho para criar módulos estáveis</b>
- os contratos promovidos pelas interfaces faz com que o desenvolvedor pense 2x antes de mudar
- interfaces tendem a ser mais coesas, se o contrato mantiver-se simples e bem definido -> coisas coesas tendem a mudar pouco
- "programe voltado para interfaces" (p.28) - mas cada cenpario precisa ser analisado individualmente
- interfaces promovem <b>flexibilidade</b>, pois permite que existam diversas implementações
- Ou seja, o ideal é <b>ACOPLAR-SE A MÓDULOS ESTÁVEIS</b>, que tendem a mudar menos

#### Interfaces coesas:
- contrato simples e bem definidos, mais reutilizavéis
- interfaces coesas são aquelas que suas implementações não precisem fazer "gambiarras" para se adaptarem

### 3.4 DIP Dependency Inversion Principle
> "Se precisamos acoplar, que seja com classes estáveis" (p.31)
- Princípio da Inversão de Dependência: <b>"Sempre qie uma classe for depender de outra, ela deve depender sempre de outro módulo mais estável do que ela mesma"</b>
- Abstrações tendem a ser mais estáveis e implementações instáveis. Tentar não depender de implementações
- Abstrações não devem depender de implementações

>De maneira mais elegante, o princípio diz: 
>- Módulos de alto nível não devem depender de módulos de baixo nível.
Ambos devem depender de abstrações.
> - Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.

- Clases com menos dependências são mais dimples, com menos regras de negócio e mais fácil de serem testadas
- "Agrupar dependências é, no fim, aumentar a coesão" (p.36) -> dependencias que façam sentido serem agrupadas, por contexto
- Cuidado com acoplamentos lógicos, ou seja, aqueles que não são explicitos, mas as mudanças serão propagadas

> - Conclusão: Classes não coesas devem ter suas responsabilidades dividas em pequenas classes, e classes devem tentar ao máximo se acoplar com classes que são estáveis, ou seja, mudam pouco.

## Capítulo 4 - Classes abertas e o tal do OCP
- Nosso código deve estar sempre pronto para evoluir 
- Como balencear enrte acoplamento e coesão? Buscar o equilíbrio é fundamental

### 4.2 OCP Princípio do Aberto-Fechado
- Fazer com que a criação de novas regras seja mais simples e que as mudanças se propaguem automaticamente por todo o sistema.
- "Um outro conceito que nos ajuda a ter classes coesas e que evoluam mais
fácil é pensar sempre em escrever classes que são “abertas para extensão”, mas “fechadas para modificação” (sim, esse é o famoso Open Closed Principle)" (p.43)
>- <b>Abertas para extensão:</b> estender o compartamento deve ser fácil
>- <b>Fechadas para alteração:</b> a classe nçao deve ser modificada o tempo todo
- Abstrações são uma boa ferramenta para isso e passar a receber pelo construtor a implementação, dando mais flexibilidade sem precisar modificar o tempo todo a cada necessidade de uso, <b>mudando o comportamento final sem mudar o código.</b>
- Uma classe que depende de abstrações é um bom exemplo do uso do OCP. Afinal, basta passar diferentes implementações para que ela execute de maneira distinta. Ao mesmo tempo estando fechada para modificações, já que não há razões ára mudar o código dessa classe. (p.46)
- "Se está difícil de testar, é poque seu código pode ser melhorado" (p.49)
- A falta de abstração gera repetição de código
- <b> Classes abertas são aquelas que deicam explícitas suas dependências</b>

## Capítulo 5 - O encapsulamento e a propagação de mudanças
Ideia principal: o uso do encapsulamento como forma de diminuir os pontos de atuação necessários para propagar mudanças

### O encapsulamento
Encapsulamento: "nome que damos à ideia de a classe <b>esconder os detalhes de implementação</b>, ou seja, <b>como</b> o método faz o trabalho dele" (p.58) 
"[...] uma classe (ou método) bem encapsulada é aquela que esconde bem a maneira como faz as coisas" (p.60)

#### Por que esconder?
- facilidade de alterar a implementação (ela está concentrada dentro do método, podemos facilmente apagar e implementar de novo sem muita dificuldade) -> facilita propagação de mudança
- um código mal encapsuçlado implica em ter a regra de negócio espalhada por lugares diferentes
- melhor não deixar regras expostas em contextos que não deveriam ter domínio sobre ela.

Deixe exposto o <b> O QUÊ </b> e esconda o <b>COMO</b>

### 5.2 Intimidade Inapropriada
- exemplo de má encapsulamento
- uma classe entende mais do que devia sobre o comportamento de uma outra classe (p.61)

### 5.4 Tell, Don't Ask
- evitar perguntar ao objeto, a ideia é <b>dizer ao objeto o que ele tem que fazer</b> e não primeiro perguntar algo a ele e depois ter que decidir
- "Quando temos códigos que perguntam uma coisa para um objeto, para então tomar uma decisão, é um código que não está seguindo o  Tell, Don't Ask"(p.64)
- códigos que perguntam antes de tomar a decisão tendem a ser procedurais

### 5.6 A famosa Lei de Demeter
- é difícil manter o encapsulamento frente a cadeias de invocações (A.getA().getB().getC().metodoQualquer()) -> "se b mudar, ou se c mudar, ou se d mudar, esse código quebrará" (p.66)
- A Lei de Demeter suegere que evitemos o uso de invocações em cadeia, a ideia é sempre <b> diminuir pontos de mudança </b>

### 5.9 Modelos Anêmicos
- OO busca unir dados e comportamentos, mas há aplicações que fogem disso e separam. Ou a classe tem atributos, ou ela tem métodos, nunca os dois juntos. A isso damos o nome de modelo anêmico.


## Capítulo 6 - Herança x Composição e o tal do LSP
- Utilizar herança pode não ser tão simples, exige parcimônia. "É fácil cair em armadilhas criadas por hierarquias de classes longas ou confusas" (p.75)
- Na herança <b>clases filhas precisam respeitar os contratos definidos pela classe pai</b>

### 6.2 LSP Liskov Substitutive Principle
- "Ao herdar, você deve sempre lembrar do contrato estabelecido pela classe pai" (p.78)
- Para utilizar herança de maneira correta o desenvolvedor precisa levar em conta as <b>pré e pós-condições</b> que a classe pai definiu
- <b>PRÉ-CONDIÇÕES:</b>
    - são os dados que chegam, restrições iniciais
    - somente podem ser <b>afrouxadas</b>, nunca apertadas (ex.: se o método recebe de 0 a 100, pode passar a receber de 0 a 200, mas não de 0 a 50)
- <b>PÓS-CONDIÇÕES:</b>
    - o que o comportamento devolve
    - podem somente ser <b>apertadas</b>, nunca afrouxadas (ex.: se o método retorna entre 0 e 100, pode passar a retornar entre 0 e 50, mas não entre 0 e 200)

### 6.4 Acoplamento entre a classe pai e a classe filho
- "Modele hierarquias nas quais as classes filhos precisam conhecer pouco (ou não conhecer nada) dos detalhes da classe pai" (p.81) -> reduzuir acoplamento
- Se isso não ocorre, pode haver complicações pela classe filho não saber de comportamentos da classe pai que vai herdar, por exemplo que um método super.x() lançará uma execeção ou que para fazer um envio o filho precisaria antes solicitar um super.init()
- "O ideal seria o método ter sua própria implementação, sem depender da implementação do pai" (p.82)
- "Se a classe filho conhece demais da implementação da classe pai, é porque ela não encapsulou bem seus detalhes de implementação" (p. 82)

### 6.5 Favoreça a Composição
- favorecer/preferir o uso de composição em vez de herança. Embora nada seja 8 ou 80, tudo é uma troca, e composição nesse caso é, com frequência, a melhor
- <b>VANTAGENS:</b>
    - relação menos íntima entre classe principal e classe dependida em relação à entre classe pai e classe filho
    - por isso, quebrar o encapsulamento é mais dificil
    - ou seja, composição propões relação mínima
    - mais flexibilidade

### 6.6 Herança para DSLs e afins
- DSLs = Domain-SPecific Languages - são pequenas linguagens criadas especificamente para resolver problemas em um domínio particular. O objetivo principal de uma DSL é tornar o código mais expressivo e fácil de ler e escrever para especialistas do domínio (que talvez não sejam programadores experientes) e para os próprios desenvolvedores ao lidar com tarefas específicas.

- "Apesar de a relação entre ambas as classes ser de uma relação de herança justa, às vezes abrimos mão de boas práticas para facilitar a escrita e uso de DSLs" p.87
    - isso porque, em teoria, a herança é uma ferramenta poderosa para promover a reutilização de código e estabelecer uma relação "é um tipo de" entre classes. Para que uma DSL seja fluida muitas vezes precisamos de uma sintaxe muito específica. Para conseguir essa sintaxe, os desenvolvedores podem recorrer a "truques" ou padrões de design que, embora funcionais, podem quebrar algumas das boas práticas de herança ou de design de código no sentido mais estrito


### 6.7 Quando usar Herança então?
- Herança: X <b>é um</b> Y
- Composição: X <b>tem um</b> Y, ou X <b>faz uso de</b> Y

### 6.8 Pacotes: como usá-los
- Deixe perto coisas que se relacionam e mudam juntas

### 6.9 Conclusão
- Um bom uso de herança evita ao máximo que a classe filho conheça detalhes da implementação do pai, e não violam as restrições de pré e pós-condições na hora de sobreescrever determinado comportamento
- Não descarte a herança, apenas favoreça a composição

## Capítulo 7 - Interfaces magras e o tal do ISP
ISP - Interface segregation principle — Princípio da Segregação de interface
- criar interfaces coesas
- <i>fat interface</i>: sobrecarga de função ou de métodos desnecessários, BAIXO REÚSO
- uma má interface fará com que os clientes sintam necessidade de fazer gambiarras para se adaptar, quebrando também o princípio de Liskov

### 7.1 Interfaces coesas e magras
- Uma interface coesa é aquela que possui uma responsabilidade
- se uma interface não é coesa, também pode ser interessante dividir em duas ou mais
- cosão favorece o reúso, e interfaces coesas tendem a ser mais <b>estáveis</b>, impedem gambiarras

### 7.2 Pensando na Interface mais magra possível
- avaliar bem quais parâmetros deve-se receber em um método, avalie a discussão sobre acoplamento
- quanto mais simples, menos problemas
- método deve receber somente o que precisa, bem como ser semântico
>- "Classes que dependem de interfaces leves sofrem menos com mudanças em outros pontos do sistema. Novamente, elas são pequenas, portanto, têm poucas razões para mudar."

### 7.4 Fábricas ou Injeção de Dependência?
- Temos duas opções: 
  - usar algum framework de injeção de dependência, como Spring, Guice, entre outros 
  - ou utilizar fábricas, isto é, classes cuja responsabilidade é instanciar outras classes.
- Fábricas 
  - independem de frameworks e de bibliotecas para funcionar
  - ela é uma solução OO simples e de fácil implementação.
  - "Em uma fábrica, você precisa manualmente instanciar C, que é uma dependência de B, que, por sua vez, é uma dependência de A" -> **dependência explícita**
  - não deve conter regra de negócio
  - altamente acoplada, mas **estáveis**. (só quebrará se a quando a maneira de construir a classe principal mudar)
  - decisões de design
- Frameworks 
  - facilitam o trabalho de gerenciamento, requer menos código
  - "por fazer tudo de forma automatizada e requerer menos código,“esconde” de você as suas reais dependências" -> **árvore de dependências implícita.**
  
## Capítulo 8 - Consistências, objetinhos e objetões
- discutir a consistência do objeto. Como validar esse estado?
- **Objetos Inválidos:**  "Objetos em estado inválido são  bastante problemáticos. Por estado inválido, entenda-se quele objeto cujos atributos possuem valores não aceitáveis" (p.100) 
### 8.1 Construtores ricos
- Objetos instáveis podem apresentar comportamento instável
- "Garantir a integridade do seu estado é responsabilidade do próprio objeto." (p.101) -> não deve permitir que classes clientes o levem a um estado inválido
- "Construtores são uma ótima maneira de se resolver esse problema. Se a classe possui atributos sem as quais ela não pode viver, eles devem ser pedidos no construtor" (p.101) -> ou seja, classe deve exigir antes de ser instanciada
- se o objeto for complexo para ser construído somente com construtor, há alternativas (builders, factories, etc)

### 8.2 Validando Dados
- TIPOS DE VALIDAÇÃO:
  - Validação de forma: garantem que o tipo de dado enviado pelo usuário seja válido
  - Validação de negócio: regras de negócio
- Controllers fazem essa ponte entre onde o usuário interage e o mundo do domínio, onde as regras vivem (p.104) -> é neles que acontecem as validações de forma, integridade dos dados
- Onde devem ocorrer as validações de negócio? Depende
  - Dentro da própria entidade
    - construtores ou métodos internos. Não é muito elegante ter que tratar exceções lançadas por construtores
  - Implementação de validação intermediária
    - builders
    - classes específicas
    - decorator, chain of responsability
- Ou seja: 
>"Como você pode ver, existem diversas abordagens diferentes para validação. Todas elas possuem vantagens e desvantagens. Lembre-se de procurar por qual se encaixa melhor em seu   problema: se suas regras de validação são complexas, partir para uma solução mais flexível é necessário; se elas forem simples, talvez deixá-las puramente em seus controladores seja suficiente" (p.108)

### 8.3 Teorema do Bom Vizinho e nulos pra lá e pra cá
- "Bom vizinho no sentido de que você é educado e não passará dados inválidos para a outra classe." (p.109)
>  "Tente ser amigável com a classe que você irá consumir. Faça bom uso da interface pública que ela provê. Use sempre a sobrecarga correta; muitas vezes a classe lhe dá a sobrecarg sem aquele parâmetro que você não tem em mãos naquele momento.
> 
>  Se você tem dados que realmente  podem ser nulos, pense em usar Null Objects, ou algo parecido (algumas linguagens já têm os tais Optional, que forçam o programador a tratar se ele é nulo ou não)" p109
-  Tiny Types: um tipo particular que representa pequenas responsabilidaes, pequenas partes do sistemas e praticamente não têm comportamentos
   - vantagens:  cada pequeno tipo pode também fazer sua própria validação, garantir que todo o conteúdo seja válido. Reutilizar fica mais fácil
   - desvantagens: justamente a quantidade de código a mais que existirá no sistema.

### 8.5 DTOs do bem 
- DTO Data Transfer Objects -> devem ser usados para transferir dados, mas não devem possuir comportamentos, só atributos.
- útil para quando é necessário transformações, ou seja, quando a classe de negócio não representa bem o escopo que se precisa exibir por exemplo
- ex: relatórios; alimentar telas do front
> - "Não tenha medo de criar DTOs que representem pedaços do seu sistema. Facilite a transferência de dados entre suas camadas; aumente a semântica deles. Lembre-se que o problema não é ter DTOs, mas sim só ter DTOs."

### 8.6 Imutabilidade x Mutabilidade
- classes mutáveis: é possível mudar seu estado interno, mudando como se comportará dali em diante
- classes imutáveis: após instanciadas, nunca mudam nada de seu estado interno

### 8.7 Classes que são feias por natureza
- Controladores e fábricas, por exemplo, tendem a ser feios (podendo ter faces procedurais, muitos ifs, códigos que pegam configuração), mas isso não é péssimo pois são códigos que tendem a ser mais **estáveis**, ou seja, ter poucos motivos para mudar. Mas, classes feias devem estar nas pontas da aplicação 
> "Ou seja, não tenha medo de ter código feio, contanto que ele esteja bem controlado, escondido, e que você não precise lembrar que ele existe o tempo todo." (p.116)

### 8.8 Nomenclatura de métodos e variáveis
- Para nomear é preciso entender o significado de cada um deles, é preciso ficar semântico
- Siga as convenções definidas pela sua equipe

## Capítulo 9 - Maus cheiros de design
- Conjunto de “más práticas” é conhecido por smells, code smells.
---
**Exemplos:**

### 9.1 Refused Request
- "Refused Bequest é o nome dado para quando herdamos de uma classe, mas não queremos fazer uso de alguns dos métodos herdados." p.120

### 9.2 Feature Envy
- "Feature Envy é o nome que damos para quando um método está mais interessado em outro objeto do que no objeto em que ele está inserido" p. 121

### 9.3 Intimidade inapropriada
- Quando outra classe conhece e/ou altera detalhes internos da sua classe que não deveria 
- Geralmente percebido através de desrespeitos à ideia do Tell, Don't Ask
- Idealmente, não devemos separar o dado de seu comportamento
- Quebra de encapsulamento 

### 9.4 God Class
- "god class é aquela classe que controla muitos outros objetos do sistema." p.123
- aumenta muito o acoplamento, ou seja, torna as classes muito dependentes e, consquentemente, **fŕageis**

### 9.5 Divergent Changes
- "Divergent changes é o nome do mau cheiro para quando a classe não é coesa, e sofre alterações constantes, devido às suas diversas responsabilidades." p.123
- baixo reúso, muitas dependências, mais complexas e mais propenças a bugs

### 9.6 Shotgun Surgery
- Uma mudança qualquer requer que muitos pontos do código precisem mudar de uma vez só, ou seja, requer um esforço além do que se deveria; alterações em cascata