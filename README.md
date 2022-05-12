# PHP

## 1. Instalação e Configuração para Windows

1. [Instalar XAMPP](https://www.apachefriends.org/index.html)

2. Configurar ambiente de desenvolvimento, coloque as configurações no fim do arquivo:
    * C:\xampp\php\php.ini:

        ```php
        display_errors = On
        memory_limit = 256M 
        max_execution_time = 120 
        error_reporting = E_ALL 
        file_uploads = On 
        post_max_size = 100M 
        upload_max_filesize = 100M 
        session.gc_maxlifetime = 14000
        ```

3. Configurar ambiente de produção, altere:
    * C:\xampp\php\php.ini:

        ```php
        display_errors = Off
        error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT & ~E_NOTICE
        ```

4. Informações sobre o seu PHP:
    * abrir um arquivo php com o código:

        ```php
        <?php 
            phpinfo(); 
        ?>
        ```

Arquivos do projeto -> C:\xampp\htdocs\nome_projeto.<br>
Acessar a aplicação -> <http://localhost/nome_projeto>.

5. Avisos de erro no PHP:
    * ``Notice``: nível de erro baixo, "olha provavelmente você não deveria ter feito esse código fonte, mas ok, a gente consegue viver com isso";
    * ``Warning``: nível de erro mais severo, "olha você está fazendo uma coisa errada, isso pode te causar problemas mais na frente", mas o php ainda consegue se virar com isso;
    * ``Fatal error``: nível de erro grave, "o programa aborta a execução na mesma hora";
    * ``Parse error``: nível de erro grave, "a sintaxe está errada";

## 2. Estrutura

```php
<?php 

    $a = 'bonito';
    echo 'Olá Mundo, ', $a;
    print 'Ola';
    print_r($a);
    var_dump($a);

    // isso é um comentário.
    /*
        * j
        * j
        * j
        * j
        * */

?>
```

## 2. Variáveis

```php
<?php
//declaração
$nome='João';
$sobrenome='Silva';

//concatenação
print $nome.' '.$sobrenome;
print "{$nome} {$sobrenome}";
print '<br>';

//aspas
print " '' ";
print ' "" ';
print " \"{$nome}\" ";
print '<br>';

//mutiplicação
$a=5;
$b='4ff';
var_dump($a * $b);
print '<br>';

//atribuição com referência
$a=5;
$b=&$a;
$a=10;
var_dump($a);
var_dump($b);
print '<br>';

//booleano
/* false:
0
0.0
''
'0'
NULL
FALSE
array
*/
$var = '0';
empty($var);
!empty($var);

//vetor
$lista = ['cor' => 'vermelho', 'peso' => 20];

//objeto, sempre passado com referência
$pessoa1 = new stdClass;
$pessoa1->nome = 'Pedro';
$pessoa1->altura = 1.8;

$pessoa2=$pessoa1;
var_dump($pessoa1);
print '<br>';
var_dump($pessoa2);
print '<br>';

?>
```

## 3. Tipagem

* O PHP é uma linguagem dinamicamente tipada, com inferência;

```php
<?php

//tipagem restrita
//declare(strict_types=1);

//inferência no tipo
$codigo = 5.5;
$nome = 'teste';
var_dump($codigo);
var_dump($nome);

//conversão automática
var_dump('4'+'5');

//forçar conversão
function calcula_imc(float $peso, float $altura): float 
{
    var_dump($peso, $altura);
    return $peso/($altura*$altura);
}
var_dump(calcula_imc(75, 1.8));

?>
```

## 4. Superglobais

* Uma variável superglobal estará disponível em qualquer escopo e arquivo;

```php
<?php
//informações gerais sobre o servidor
var_dump($_SERVER);

//dados enviados via url
var_dump($_GET);

//dados enviados via formulário do tipo post
var_dump($_POST);

//arquivos de upload
var_dump($_FILES);

//tem acesso aos dados de entrada, get, post, session
var_dump($_REQUEST);

//uma sessão aberta que armazena qualquer dado
var_dump($_SESSION);
?>
```

## 5. Constantes

* Valores que não podem ser alterados depois de definidos

```php
<?php
//definindo um constante
define('LANGUAGE', 'PT-BR');
var_dump( LANGUAGE );

//constantes mágicas
var_dump( __FILE__  );//endereço do arquivo
var_dump( __LINE__ );//linha em que o comando se encontra
var_dump( __DIR__ );//diretório do arquivo
?>
```

## 6. Operadores

* Permitem realizar interações lógicas entre valores

```php
<?php

//operações simples
$valor = 100;
$valor += 5;
$valor -= 5;
$valor *= 5;
$valor /= 5;

//operador de incremento
$teste = $valor ++;//o incremento é realizado por último
$teste = ++ $valor;//o incremento é realizado primeiro

//operadores de comparação
// < | > | <= | >= | == | === | != | !==

//operadores lógicos
// AND && | OR ||

?>
```

## 7. Estruturas de controle

* Realizam operações com base em verificações

```php
<?php

//if e else
if(true){
    echo 'Verdadeiro';
}else{
    echo 'False';
}

//operador ternário
echo (true)? 'verdadeiro': 'false';

//loop com white
$cont = 1;
while($cont <= 5){
    echo '<hr>'.$cont;
    $cont ++;
}

//loop com for
for($cont=1; $cont<=10; $cont++){
    echo $cont.' '; 
}

//verificação mútua com switch
$tipo = '';
switch ($tipo){
    case 'pdf':
        print 'arquivo pdf';
        break;
    case 'csv':
        print 'arquivo csv';
        break;
    case 'doc':
        print 'arquivo doc';
        break;
    default:
    print 'arquivo default';
        break;
}

//percorrer vetor com foreach
$lista = ['maça', 'laranja', 'banana'];
foreach ($lista as $fruta){
    print $fruta.' ';
}

?>
```
