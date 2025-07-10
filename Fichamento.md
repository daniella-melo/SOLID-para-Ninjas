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


## Capítulo 3 - 
## Capítulo 4 - 

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