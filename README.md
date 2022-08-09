# Design Patterns

> Só para lembrar que alguns padrões são muito parecidos entre si mas a intenção entre eles é diferente. 

## Padrões de projetos comportamentais

### 01. Strategy
**`Na prática:`** Temos uma calculadora de impostos e a cada novo imposto o nosso código fica maior. Temos um problema.

**`A solução:`** Cria uma pasta Impostos e dentro delas vamos criar um arquivo para cada imposto onde será implementado o cálculo individual de cada um. 

```php
<?php
namespace Alura\DesignPattern\Impostos;

use Alura\DesignPattern\Orcamento;

class Icms implements Imposto
{
    public function calculaImposto(Orcamento $orcamento): float
    {
        return $orcamento->valor * 0.1;
    }
}
```
Onde a classe imposto é uma interface para estabelecer um contrato com as outras classes que a implementa.

```php
<?php

namespace Alura\DesignPattern\Impostos;

use Alura\DesignPattern\Orcamento;

interface Imposto
{
    public function calculaImposto(Orcamento $orcamento): float;
}

```

---

### 02. Chain of Responsbility
**`Na prática:`** Precisamos aplicar descontos em nosso orçamento, só que esses descontos precisam seguir uma sequência, uma ordem.

**`A solução:`** Para evitar um if dentro do outro criamos a classe de desconto que irá chamar o primeiro desconto em seguida o próximo desconto, por fim, chama um desconto com valor nulo para encerrar o ciclo. Esse padrão existe para chamar sequências. 

---

### 03. Template Method
**`Na prática:`** Dentro dos impostos aplicados, sopomos que hajam impostos com 2 alicotas que fogem do padrão aplicado em Strategy

**`A solução:`** Vamos criar um template que aplicam essas novas regras (classes abstratas) e esses novos impostos extendem essas classes apenas com as regras e os calculos. [ Regra para aplicar a taxa máxima, calculo da taxa máxima e táxa mínima por exemplo.]

---

### 04. State
**`Na prática:`** Um orçamento tem vários estados, em aprovação, aprovado, finalizado ou reprovado e no estado de em aprovação ou aprovado é possível receber um desconto. 

**`A solução:`** Vamos criar um código que lance um erro caso já esteja aprovado e queira aprovar novamente, tando aprovado pode finalizar, estando em aprovação pode reprovar e finalizar. Compreender essa lógica dentro do código configura o padrão State. 

---

### 05. Command
**`Na prática:`** Criar um pedido 

**`A solução:`** Após aprovação de um pedido vamos executar vários comando. 
1. Vai aplicar algum desconto? 
2. Gerar o pedido com os dados do cliente
3. Salvar no banco de dados
4. Enviar um e-mail

---

### 06. Observer
**`Na prática:`** É preciso lidar com vários eventos, executálos ou não e lidar com cada um separadamente, pois alguns deles podem implementar outras bibliotecas de terceiros para executar o serviço. 

**`A solução:`** Este mecanismo consiste em um array que vai adiconar itens ou remover itens a serem executados. O php possui uma classe própria para lidar com isso, o **splobserver**, mas o ideal seria criar uma interface personalizada.

---

### 07. Iterator
**`Na prática:`** Quando é preciso lidar com muitos objetos ou um passo a passo muito grande, na criação de várias coleções ou execução de város dados.

**`A solução:`** Há uma biblioteca do php que percorre esses dados. É um padrão simples para execução de muitas instruçõess. Podemos conhecer um pouco mais sobre ele em: https://refactoring.guru/design-patterns/iterator

---

## Padrões de projetos estruturais

### 08. Adapter
**`Na prática:`** Precisamos enviar um orçamento para nossa API. E não importa se vamos usar o reactphp, guzzle, curl.

**`A solução:`** Essa chamada extrerna precisa de uma interface e ela precisa ser separada da camada de execução. Pra mesma interface nós temos várias implementações possíveis. O padrão Adapter pode nos ajudar a trocar detalhes de infraestrutura, sem muitas dores de cabeça.

---

### 09. Bridge
**`Na prática:`** Precisamos salvar dados dos nossos pedidos em vários formatos diferentes, xml, zip, csv contudo se fizermos vários arquivos para extrair o conteúdo para cada formato o sistema fica insustentável.

**`A solução:`** Separando os objetos (abstraindo) que queremos criar dos formatos que queremos exportar agente cria uma ponte entre o conteúdo da exportação e os formatos exportados.

---

### 10. Decorator
**`Na prática:`** Precisamos somar vários impostos em tempo de execução.

**`A solução:`** Criando uma classe abstrata para somar ou não um novo imposto agente evita ter que criar classes que somam 2 ou mais impostos, e esse padrão é conhecido como decorator. 

---

### 11. Composite
**`Na prática:`** Precisamos somar não apenas os itens de um orçamento contudo ítens de outros tipos de orçamento.

**`A solução:`** Composite é uma técnica para fazer com que a composição dos itens (árvore de objetos) dentro de uma operação. É como poder somar mais de um carrinho de compraas cada um com seus itens.

---

### 12. Facade
**`Na prática:`** Precisamos fazer log dos nossos orçamentos ou enviar os dados para um API.

**`A solução:`** Facade ou faixadas é uma maneira de intermediar com bibliotecas externas para realizar algumas funcionalidades de forma simples.

---

### 13. Proxy
**`Na prática:`** Nosso valor orçado agora está sendo consultado em uma API e leva 5 segundos para exibir o resultado. Precisamos fazer um cache do nosso valor orçado para evitar que ele consulte a api novamente caso seja chamado. 

**`A solução:`** Um Proxy é tipo um filtro que implementa ações antes do consumo dos dados. Ao criar uma classe de cache, primeiro verifica se o valor já está cacheado, se não, cachea esse valor e criamos excessões para outros métodos já implementado que não são suportados pela nossa classe como por exemplo: adicionar itens.

---

### 14. Flyweight
**`Na prática:`** Precisamos reduzir o uso de memória que a nossa aplicação consome. 

**`A solução:`** Ao criar objetos comuns separados da nossa estrutura conseguimos realizar esse feito. Exemplo a data atual é uma só pra todos então gera uma única vez e inclui ela nos pedidos que estão sendo feito. Um cliente pode ter mais de um orçamento então essa seria mais uma segregação a ser feita. [ Raro uso: Usar somente se necessário ]

---