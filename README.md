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

## 3. Variáveis

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

## 4. Tipagem

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

## 5. Superglobais

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

## 6. Constantes

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

## 7. Operadores

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

## 8. Estruturas de controle

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

## 9. Requisição de arquivos

```php
<?php

//importam um arquivo para dentro de outro

include 'arquivo.php';
//tenta executar o código mesmo que tenha dado erro na importação

require 'arquivo.php';
//já da um fatal error se a importação estiver errada

include_once 'arquivo.php';
require_once 'arquivo.php';
//permite a importação desse aquivo uma única vez

?>
```

## 10. Manipulação de funções

```php
<?php

//variáveis declaradas dentro de uma função só existem dentro do escopo de uma função
$total = 0;
function km2milhas($km)
{
    $total+=$km;
    return $km * 0.6;
}
echo km2milhas(100);

//o global define que uma variável pode ser acessada fora do contexto da função
//NÃO É RECOMENDÁVEL, pois com uma variável fora de contexto perde-se o seu controle
//ela poderia ser alterada em qualquer outro lugar do código
$total = 0;
function km2milhas($km)
{
    global $total;
    $total+=$km;
    return $km * 0.6;
}
echo km2milhas(100);
echo $total;

//o static mantém o valor da variável depois da execução da função
function percorre($km)
{  
    static $total;
    $total += $km;
    print "percorreu mais $km\n de $total<br>";
}
percorre(100);
percorre(100);
percorre(100);

//variáveis escalares(as normais) tem valores armazenados separadamente
//por isso quando passadas como parâmetro de uma função não alteram o seu valor
function incrementa($var, $valor)
{
    $var+=$valor;//$var não está manipulando o mesmo espaço da memória que $teste
}
$teste = 100;
incrementa($teste, 20);
var_dump($teste);//teste não altera o valor

//para que $teste seja alterada deve-se passar por referência (&)
function incrementa(&$var, $valor)//$var como referência de $teste com (&)
{
    $var+=$valor;//$var está manipulando o mesmo espaço da memória que $teste
}
$teste = 100;
incrementa($teste, 20);
var_dump($teste);//$teste altera o valor
//SE INVÉS DE VARIÁVEL ESCALAR FOR OBJETO, A PASSAGEM POR REFERÊNCIA É AUTOMÁTICA

//funções de ordenação trabalham internamente com referência
$lista = ['a','b','c'];
sort($lista);
var_dump($lista);

//funções anônimas não tem nome, elas são guardadas em variáveis
$remove_acento = function($str) {
    return str_replace(
         ['á', 'é', 'í', 'ó', 'ú'],
         ['a', 'e', 'i', 'o', 'u'],
         $str
    );
};//precisa de ; quando é função anônima, porque é uma atribuição a uma variável
var_dump($remove_acento('bábébíbóbú'));

//sempre que precisar usar a função em outro contexto pode ser passada como parâmetro
function teste($palavra, $funcao)
{
    $palavra = $funcao($palavra);
    return strtoupper($palavra);
}
var_dump(teste('bábébíbóbú', $remove_acento));//passando função como parâmetro

?>
```

## 11. Manipulação de Arquivos e Diretórios

```php
<?php

$handler = fopen('arquivos/teste1.txt', 'r');//abre arquivo, modo read
while (!feof($handler)){//feof, quando for a ultima linha retorna true
    print fgets($handler, 100);//ler a linha de um arquivo, segundo parâmetro são o número de caracteres
    print "<br>";
}
fclose($handler);

//criação e escrita
$handler = fopen('arquivos/teste2.text', 'w');//criando arquivo, modo escrita
//escrevendo no arquivo
fwrite($handler, "linha1" . PHP_EOL);
fwrite($handler, "linha2" . PHP_EOL);
fwrite($handler, "linha3" . PHP_EOL);

print file_get_contents('arquivos/teste1.txt');//pega todo o conteúdo do arquivo
//lado bom: é bem simples
//lado ruim: se o arquivo for grande vai pesar

file_put_contents('arquivos/teste1.txt', "a\n b\n c\n");//escreve no arquivo,\n só funciona em ""
print file_get_contents('arquivos/teste1.txt');

$arquivo = file('arquivos/teste1.txt');//lê um arquivo e transforma em vetor
foreach ($arquivo as $linha)
{
    print $linha . '<br>';
}
//acessando linha
$arquivo[0];
$arquivo[1];
$arquivo[2];
$arquivo[3];

//copiando arquivo
copy('arquivos/teste1.txt', 'arquivos/novo.txt');

//renomeando
rename('arquivos/teste1.txt', 'arquivos/teste0.txt');

//movendo
rename('arquivos/teste1.txt', 'novo_direitorio/teste1.txt');

//excluindo
unlink('arquivos/teste1.txt');

//verificando se existe
if (file_exists('arquivos/teste1.txt'))
{
    echo "arquivo existe";
}

//criando diretório
mkdir('novodir', 0777);//o segundo parâmetro são as permissões, 0777 são todas

//excluir diretório
rmdir('novodir');

//pegar todos os arquivos e pastas de um diretório
$arquivos = scandir('arquivos');
foreach ($arquivos as $arquivo){
    print $arquivo . '<br>';
}

?>
```