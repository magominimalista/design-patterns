# Design Patterns

### 1. Strategy
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

### 2. Chain of Responsbility
**`Na prática:`** Precisamos aplicar descontos em nosso orçamento, só que esses descontos precisam seguir uma sequência, uma ordem.

**`A solução:`** Para evitar um if dentro do outro criamos a classe de desconto que irá chamar o primeiro desconto em seguida o próximo desconto, por fim, chama um desconto com valor nulo para encerrar o ciclo. Esse padrão existe para chamar sequências. 

---

### 3. Template Method
**`Na prática:`** Dentro dos impostos aplicados, sopomos que hajam impostos com 2 alicotas que fogem do padrão aplicado em Strategy

**`A solução:`** Vamos criar um template que aplicam essas novas regras (classes abstratas) e esses novos impostos extendem essas classes apenas com as regras e os calculos. [ Regra para aplicar a taxa máxima, calculo da taxa máxima e táxa mínima por exemplo.]

---

### 4. State
**`Na prática:`** Um orçamento tem vários estados, em aprovação, aprovado, finalizado ou reprovado e no estado de em aprovação ou aprovado é possível receber um desconto. 

**`A solução:`** Vamos criar um código que lance um erro caso já esteja aprovado e queira aprovar novamente, tando aprovado pode finalizar, estando em aprovação pode reprovar e finalizar. Compreender essa lógica dentro do código configura o padrão State. 

---

### 5. Command
**`Na prática:`** Criar um pedido 

**`A solução:`** Após aprovação de um pedido vamos executar vários comando. 
1. Vai aplicar algum desconto? 
2. Gerar o pedido com os dados do cliente
3. Salvar no banco de dados
4. Enviar um e-mail

---

### 6. Observer
**`Na prática:`** É preciso lidar com vários eventos, executálos ou não e lidar com cada um separadamente, pois alguns deles podem implementar outras bibliotecas de terceiros para executar o serviço. 

**`A solução:`** Este mecanismo consiste em um array que vai adiconar itens ou remover itens a serem executados. O php possui uma classe própria para lidar com isso, o **splobserver**, mas o ideal seria criar uma interface personalizada.

---

### 7. Iterator
**`Na prática:`** Quando é preciso lidar com muitos objetos ou um passo a passo muito grande, na criação de várias coleções ou execução de város dados.

**`A solução:`** Há uma biblioteca do php que percorre esses dados. É um padrão simples para execução de muitas instruçõess. Podemos conhecer um pouco mais sobre ele em: https://refactoring.guru/design-patterns/iterator