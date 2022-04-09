# Teste para pessoa desenvolvedora PHP

[← Voltar](README.md).

⚠️ Todas as perguntas são baseadas no **PHP 7.4.28**.

## Exemplo

### 0. Quais os valores de `$a` e `$b` no código abaixo? Por quê?

```php
$a = array_merge(array(1,2), NULL);
$b = array_merge($a, array(3));

var_dump($a);
var_dump($b);
```

> ```
> NULL
> NULL
> ```
> 
> A função `array_merge` retorna `NULL` quando qualquer um dos argumentos não for do tipo `array`. Embora o PHP 7 emita warnings sobre erro no tipo do argumento nem toda instalação está configurada para exibir warnings, logo é importante o desenvolvedor verificar os valores maualmente antes da chamada do `array_merge`, especialmente quando estamos concatenando o retorno de um `array_merge`.
>
> No PHP 8 esse comportamento foi atualizado para emitir um erro, o que ajuda a prevenir problemas.
> 
> ```
> Fatal error: Uncaught TypeError: array_merge(): Argument #2 must be of type array
> ```

## Perguntas

### 1. Qual a diferença entre `echo` e `print`?

> print é uma função e o echo uma declaração, sendo que o print sempre retorna 1 porém o echo não retorna valor.

### 2. Qual é a saída do código abaixo? Por quê?

```php
$x = true and false;
var_dump($x);
```

> Retorna um booleano true, porque o and tem a precedência de um operador menor que o igual. Como por exemplo em uma conta simples: 2 + 2 * 2 e (2 + 2) * 2. O primeiro retorna 6 e o segundo 8

### 3. Qual é a saída do código abaixo? Por quê?

```php
$x = 5;
$a = array(
    $x++ + $x++,
    $x,
    $x-- - $x--,
    $x,
);

var_dump($a);
```

> 11, 7, 1, 5. Porque está definido como pós incremento e pós decremento. Portanto primeiro retorna-se o valor original para então incrementar/decrementar $x em um.

### 4. Quais serão os valores de `$a` e `$b` após a execução do código abaixo? Por quê?

```php
$a = '1';
$b = &$a;
$b = "2$b";
```

> Ambos serão 21. Primeiro estamos concatenando duas strings 2 e 1 e segundo pois $b = &$a; está utilizando de atribuição por referência que indica que a variável $a é uma referência de $b.

### 5. O que são Traits e para que servem? 

> Traits são partes de código que servem para reutilização por diferentes classes.

### 6. Qual será a saída do código abaixo? Por quê?

```php
var_dump(0123 == 123);
var_dump('0123' == 123);
var_dump('0123' === 123);
```

> false, true, false. 
  1. var_dump(0123 == 123); false porque 0123 é um octal e o 123 octal é igual a 83 decimal e 123 é decimal
  2. var_dump('0123' == 123); true porque a string '0123' será automaticamente forçada a ser interpretada como um número ao ser comparada com um inteiro e o 0 é ignorado
  3. var_dump('0123' === 123); false porque === é um operador de comparação idêntica então verifica-se se são iguais e do mesmo tipo.

### 7. Qual será a saída do código abaixo? Por quê?

```php
$a = '';
$b = 0;
$c = '0a';

var_dump($a == $b);
var_dump($b == $c);
var_dump($c == $a);
```

> true, true, false
  1. var_dump($a == $b); true pois como foi usado o operador de comparação igual (==) ele verifica somente os valores iguais onde $a é uma string 0 (vazio é igual a 0) e $b um int 0 sendo os valores iguais
  2. var_dump($b == $c); true pois como foi usado o operador de comparação igual (==) ele verifica somente os valores iguais onde "0a" o a é ignorado na variável $c 
  3. var_dump($c == $a); false pois como foi usado o operador de comparação igual (==) ele verifica somente os valores iguais e como são duas strings os valores de $c e de $a são claramente diferentes.

### 8. Qual será o valor de `$x` após a execução do código abaixo? Por quê?

```php
$x = 3 + "15%";
```

> 18, pois como nas questões anteriores o php tem suporte para conversão automática de tipo no contexto que está sendo usada, como é o caso dessa operação aritmética, então como "15%" começa com um número (15) o restante é ignorado

### 9. Qual a diferença entre `require_once()` e `include_once()`?

> são quase idênticas, porém em caso de algum erro o include_once ainda mostrará a saída e o require_once surgirá um fatal error e a saída não é exibida

### 10. Qual será o valor de `$name` após a execução do código abaixo? Por quê?

```php
$name = 'John ';
$name[10] = 'Doe';
```

> Porque uma string é um array de caracteres, ele adicona somente o D pois está sendo carregado apenas uma ocorrência [10], então só há espaço para o primeiro caractere do 'Doe'

### 11. Qual será a saída do código abaixo? Por quê?

```php
$x = PHP_INT_MAX;
echo gettype($x + 1);
echo (int)($x + 1);

$y = 1.0;
echo is_float($y);
echo gettype($y);
```

> double, -9223372036854775808, 1, double
  1.  Pois está sendo adicionado +1 no maior inteiro suportado
  2. para não causar estouro de buffer com um bit extra flutuando na RAM
  3. Porque ele verificou como verdadeiro que o número em questão é um float
  4. float e double são semelhantes porém o PHP interpreta como double pois o double consegue armazenar mais números à direita do ponto

### 12. Qual será o valor de `$x` após a execução do código abaixo? Por quê?

```php
$x = "one" + 1;
```

> 1 causando um erro de valor não numérico "one". Isso acontece pois o PHP entende que está sendo efetuada uma operação aritmética, e não é possível fazê-la com uma string (somente se essa string fosse números para o php fazer a conversão automática)

### 13. Qual a diferença entre `isset()` e `empty()`?

> isset() verifica se a variável existe e empty() verifica se contém algum valor na variável
