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



