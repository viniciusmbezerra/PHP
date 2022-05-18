# PHP

## PHP: Introdução

### 1. Instalação e Configuração para Windows

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
            phpinfo(); 
        ```

Arquivos do projeto -> C:\xampp\htdocs\nome_projeto.<br>
Acessar a aplicação -> <http://localhost/nome_projeto>.

5. Avisos de erro no PHP:
    * ``Notice``: nível de erro baixo, "olha provavelmente você não deveria ter feito esse código fonte, mas ok, a gente consegue viver com isso";
    * ``Warning``: nível de erro mais severo, "olha você está fazendo uma coisa errada, isso pode te causar problemas mais na frente", mas o php ainda consegue se virar com isso;
    * ``Fatal error``: nível de erro grave, "o programa aborta a execução na mesma hora";
    * ``Parse error``: nível de erro grave, "a sintaxe está errada";

### 2. Estrutura

```php
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
```

### 3. Variáveis

```php
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
```

### 4. Tipagem

* O PHP é uma linguagem dinamicamente tipada, com inferência;

```php
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
```

### 5. Superglobais

* Uma variável superglobal estará disponível em qualquer escopo e arquivo;

```php
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
```

### 6. Constantes

* Valores que não podem ser alterados depois de definidos

```php
//definindo um constante
define('LANGUAGE', 'PT-BR');
var_dump( LANGUAGE );

//constantes mágicas
var_dump( __FILE__  );//endereço do arquivo
var_dump( __LINE__ );//linha em que o comando se encontra
var_dump( __DIR__ );//diretório do arquivo
```

### 7. Operadores

* Permitem realizar interações lógicas entre valores

```php
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
```

### 8. Estruturas de controle

* Realizam operações com base em verificações

```php
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
```

### 9. Requisição de arquivos

```php
//importam um arquivo para dentro de outro

include 'arquivo.php';
//tenta executar o código mesmo que tenha dado erro na importação

require 'arquivo.php';
//já da um fatal error se a importação estiver errada

include_once 'arquivo.php';
require_once 'arquivo.php';
//permite a importação desse aquivo uma única vez
```

### 10. Manipulação de funções

```php
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
```

### 11. Manipulação de Arquivos e Diretórios

```php
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
```

### 12. Manipulação de Strings

```php
$nome = 'Maria';
$sobrenome = 'da Silva';

//concatenando 2 strings
$nome_completo = $nome . $sobrenome;
$nome_completo = "$nome $sobrenome";//aspas duplas a string é interpretada
$nome_completo = "xxx{$nome} - {$sobrenome}xxx";//chaves para colocar conteúdos junto com a string
$nome_completo = '$nome $sobrenome';//aspas simples tratam como string literal

var_dump($nome_completo);

//aspas dentro de aspas
print "Exemplo de 'aspas' ";
print 'Exemplo de "aspas" ';
print 'Exemplo de \'aspas\'';
print "Exemplo de \"aspas\"";
print '\t';//tabulação
print '\n \r';//quebra de linha

//funções de manipulação de strings
print strtoupper($nome . $sobrenome);//tudo para caixa alta
print strtolower($nome . $sobrenome);//tudo para caixa baixa
print strlen($nome);//tamanho de uma string
print substr($nome . $sobrenome, 6, 8);//retorna do 6º caracter ao 8º
print substr($nome . $sobrenome, 0, 5);//retorna do caracter 0 ao 5º
print substr($nome . $sobrenome, -3);//retorna os 3 últimos caracteres
print str_replace('a', 'e', $nome . $sobrenome);//substituir caracteres
```

### 13. Manipulação de Arrays

#### 1. Vetor unidimensional

```php
$cores = array('vermelho', 'verde', 'amarelo');//versão 5 para baixo
$cores = ['vermelho', 'verde', 'amarelo'];//mais moderna

$cores = [];//declarando vazio
$cores[] = 'vermelho';//inserindo no final
$cores[] = 'verde';
$cores[] = 'amarelo';

$cores = [];//declarando vazio
$cores[1] = 'vermelho';//inserindo no índice numérico
$cores[3] = 'verde';
$cores[5] = 'amarelo';

$pessoa = [];//declarando vazio
$pessoa['nome'] = 'Maria';//inserindo no índice do tipo string
$pessoa['endereco'] = 'rua tal';
$pessoa['nascimento'] = '1990-01-01';

//percorrendo vetor
foreach ($pessoa as $chave => $informacao)
{
    print $chave . ': ' . $informacao . '<br>';
}
```

#### 2. Vetor multidimensional

```php
//declarando
$carros = [ 'palio' => ['cor' => 'azul',
                        'marca' => 'fiat',
                        'ano' => 2002],
            'corsa' => ['cor' => 'prata',
                        'marca' => 'GM',
                        'ano' => 2003],
          ];

foreach ($carros as $modelo => $informacoes)
{
    print $modelo."<br>";
    foreach ($informacoes as $atributo => $valor)
    {
        print "$atributo: $valor <br>";
    }
}
```

#### 3. Funções de manipulação de vetores

```php
$cores = ['vermelho', 'verde', 'amarelo'];

$cores = 'ciano';//adiciona no final

array_push($cores, 'ciano');//adiciona no final

array_unshift($cores, 'ciano');//adiciona no início

array_shift($cores);//remove a primeira posição do vetor

array_pop($cores);//remove a última posição do vetor

$cores = array_reverse($cores);//inverte a ordem dos valores do vetor

$resultado = array_merge($cores, ['ciano', 'cinza']);//mescla dois vetores

$carros = [];
$carros[10001] = 'Palio 2002';
$carros[73933] = 'Corsa 2003';
$carros[82634] = 'Celta 2005';
$carros[12838] = 'Uno 1999';

sort($carros);//ordena, mas perde os índices

asort($carros);//ordena pelo conteúdo

ksort($carros);//ordena pelas chaves

array_keys($carros);//retorna um vetor com as chaves do vetor de parâmetro

array_values($carros);//retorna um vetor com o conteúdo do veto de parâmetro

count($carros);//retorna quantas posições tem o vetor

in_array('Uno 1999', $carros);//verifica se está no vetor

$data = '2013-10-20';
$partes = explode('-', $data);//transforma em vetor separando pelo caracter escolhido
print implode('-', $partes);//junta as partes do vetor com o caracter escolhido
```

## PHP: Orientação a Objetos

### 1. Classes

``A classe é um molde que produz N objetos;``

``Cada objeto terá atributos e métodos de acordo com o que foi definido na classe;``

```php
class Produto
{
    //atributos do tipo privado só pode ser manipulados dentro do contexto da própria classe
    private $descricao;
    private $estoque;
    //atributos do tipo public podem ser manipulados em qualquer lugar do código
    public $preco;

    //O método construtor inicia um objeto com valores que serão passados por parâmetros
    //sem esse método o objeto irá iniciar com o valor null e depois seriam inseridos os dados
    public function __construct($descricao, $estoque, $preco)
    {
        //o $this referencia ao próprio objeto que está sendo criado
        $this->setDescricao($descricao);
        $this->setEstoque($estoque);
        $this->setPreco($preco);
    }

    //Cada função a seguir é um método do objeto, que trará funcionalidade
    //funções do tipo public podem ser acessadas fora do contexto da classe
    public function setDescricao($descricao)
    {
        if (is string($descricao))
        {
            $this->descricao = $descricao;
        }
    }
    public function getDescricao()
    {
        return $this->descricao;
    }

    public function setEstoque($estoque)
    {
        if (is numeric($estoque))
        {
            $this->estoque = $estoque;
        }
    }
    public function getEstoque()
    {
        return $this->estoque;
    }

    public function setPreco($preco)
    {
        if (is string($preco))
        {
            $this->preco = $preco;
        }
    }
    public function getPreco()
    {
        return $this->preco;
    }

    public function aumentarEstoque($unidades)
    {
        if (is numeric($unidades) and $unidades >= 0)
        {
            $this->estoque -= $unidades;
        }
    }
    public function diminuirEstoque($unidades)
    {
        if (is numeric($unidades) and $unidades >= 0)
        {
            $this->estoque -= $unidades;
        }
    }
    public function reajustarPreco($percentual)
    {
        if (is numeric($percentual) and $percentual >= 0)
        {
            $this->preco *= (1 + ($percentual/100));
        }
    }

    //O método destrutor é usado para fazer com que o objeto deixe a memória no fim da execução
    public function __destruct()
    {
        echo "DESTRUÍDO: Objeto {$this->getDescricao()} ";
    }
}

//Criando um objeto ou instanciando um objeto
$p1 = new Produto('Chocolate', 10, 8);

echo "O estoque de {$p1->getDescricao()} é {$p1->getEstoque()} <br>";
echo "O estoque de {$p1->getDescricao()} é {$p1->getPreco()} <br>";


$p1->aumentarEstoque(10);
$p1->diminuirEstoque(5);
$p1->reajustarPreco(50);

//Para forçar que o objeto deixe a memória antes do destrutor ser executado
$p1 = null;
unset($p1);
```

* Conversões de tipo

```php
//Criando um objeto a partir da classe padrão do PHP
$produto = new stdClass;
$produto->descricao = 'Chocolate';
$produto->estoque = 100;
$produto->preco = 7;

//Convertendo um objeto em um array
$vetor1 = (array) $produto;

//Convertendo um array em um objeto
$vetor2 = [
    'descricao' => 'Café',
    'estoque' => 100,
    'preco' => 7
];
$produto2 = (object) $vetor2;

//Colocando dados de um vetor em um objeto
$produto = [];
$produto['descricao'] = 'Chocolate';
$produto['estoque'] = 100;
$produto['preco'] = 7;

$objeto = new stdClass;

foreach ($produto as $chave => $valor)
{
    $objeto->$chave = $valor;
}
```

### 2. Relação entre objetos

#### 1. Relação por apontamento

`Uma classe aponta para para outra classe afim de complementar as informações necessárias`

* Definindo classe Produto

```php
class Produto
{
    private $descricao;
    private $estoque;
    private $preco;
    private $fabricante;//este atributo fará o apontamento para o objeto que corresponde ao fabricante deste produto

    public function __construct($descricao, $estoque, $preco)
    {
        $this->descricao = $descricao;
        $this->estoque = $estoque;
        $this->preco = $preco;
    }

    public function getDescricao()
    {
        return $this->descricao;
    }

    //Nessa função temos uma indução ao tipo, que certificará que a variável $fabricante é da classe Fabricante, se não for vai retornar um erro
    public function setFabricante(Fabricante $fabricante)
    {
        $this->fabricante = $fabricante;
    }

    public function getFabricante()
    {
        return $this->fabricante;
    }
}
```

* Definindo classe Fabricante

```php
class Fabricante
{
    private $nome;
    private $endereco;
    private $documento;

    public function __construct($nome, $endereco, $documento)
    {
        $this->nome = $nome;
        $this->endereco = $endereco;
        $this->documento = $documento;
    }
    
    public function getNome()
    {
        return $this->nome;
    }
}
```

* Criando a associação por apontamento entre Produto e Fabricante

```php
//importando as classes
require_once 'classes/Fabricante.php';
require_once 'classes/Produto.php';

//criando os objetos
$p1 = new Produto('Chocolate', 10, 7);
$f1 = new Fabricante('Fabrica de Chocolate', 'Rua tal ...', '93.292901.200');

$p1->setFabricante($f1);//declarando fabricante no produto
```

* Exibindo informações

```php
$descricao = $p1->getDescricao();
$nome_fabr = $p1->getFabricante()->getNome();//encadeamento de chamada

print "Descrição: {$descricao} <br>";
print "Nome fabricante: {$nome_fabr}";
```

#### 2. Relação por composição

``Um objeto pai contém várias partes que são outros objetos que foram criados dentro do objeto pai;``

``TODO -> PARTE;``

``As partes só existem enquanto o todo existe;``

* Criando a classe característica

```php
class Caracteristica
{
    private $nome;
    private $valor;

    public function __construct($nome, $valor)
    {
        $this->nome = $nome;
        $this->valor = $valor;
    }

    public function getNome()
    {
        return $this->nome;
    }

    public function getValor()
    {
        return $this->valor;
    }
}
```

* Criando a classe produto

```php
class Produto
{
    private $descricao;
    private $estoque;
    private $preco;
    private $caracteristicas;

    public function __construct($descricao, $estoque, $preco)
    {
        $this->descricao = $descricao;
        $this->estoque = $estoque;
        $this->preco = $preco;
        $this->caracteristicas = [];
    }

    public function getDescricao()
    {
        return $this->descricao;
    }

    public function addCaracteristica($nome, $valor)
    {
        $this->caracteristicas[] = new Caracteristica( $nome, $valor );
    }

    public function getCaracteristicas()
    {
        return $this->caracteristicas;
    }
}
```

* Criando a composição de Produto com as Caracteristicas

```php
require_once 'classes/Produto.php';
require_once 'classes/Caracteristica.php';

$p1 = new Produto('Chocolate', 10, 7);

$p1->addCaracteristica('Cor', 'Branco');
$p1->addCaracteristica('Peso', '500gr');
```

* Exibindo informações

```php
print 'Produto: ' . $p1->getDescricao() . '<br>';

//percorrendo vetor características
foreach ($p1->getCaracteristicas() as $caracteristica)
{
    //chamando métodos para cada característica
    $nome = $caracteristica->getNome();
    $valor = $caracteristica->getValor();

    print "Característica {$nome} = {$valor} <br>";
}
```

#### 3. Relação por agregação

``Os objetos são criados separadamente e depois reunidos;``

``As partes não dependem do todo para existir;``

``Uma cesta de compras: uma cesta pode ter vários produtos, e um produto pode estar em várias cestas;``

* Criando a classe Cesta

```php
class Cesta
{
    private $hora;
    private $itens;

    public function __construct( $hora, $itens )
    {
        $this->hora = date('Y-m-d H:i:s');
        $this->itens = [];
    }

    public function addItem(Produto $produto)
    {
        $this->itens = $produto;
    }

    public function getItens()
    {
        return $this->itens;
    }
}
```

* Criando a classe Produto

```php
class Produto
{
    private $descricao;
    private $estoque;
    private $preco;

    public function __construct($descricao, $estoque, $preco)
    {
        $this->descricao = $descricao;
        $this->estoque = $estoque;
        $this->preco = $preco;
    }

    public function getDescricao()
    {
        return $this->descricao;
    }
}
```

* Criando a agregação entre Cesta e Produto

```php
require_once 'classes/Cesta.php';
require_once 'classes/Produto.php';

$c1 = new Cesta;

$p1 = new Produto('Chocolate', 10, 5);
$p2 = new Produto('Café', 100, 7);
$p3 = new Produto('Mostarda', 50, 3);

//adicionando objetos(Produtos) dentro do array itens do objeto $c1
$c1->addItem( $p1 );
$c1->addItem( $p3 );
$c1->addItem( $p2 );
```

* Exibindo informações

```php
print_r($c1);

//$c1 tem o array de itens;
//este array contém os objetos inseridos nele;
//cada um desses objetos é um produto;
//e cada produto tem métodos;
//logo é possível chamar esse métodos a partir de cada posição do vetor itens;
foreach ($c1->getItens() as $item)
{
    print "Item: {$item->getDescricao()} <br>";
}
```

### 3. Herança

``A capacidade de herdar comportamento entre classes é acionada pela palavra-chave extends,indicando a classe pai da qual vamos absorver o comportamento.``

* Criando classe Conta

```php
class Conta
{
    //O protected é usado para definir que esses atributos serão usados por classes filhas
    protected $agencia;
    protected $conta;
    protected $saldo;

    public function __construct($agencia, $conta, $saldo)
    {
        $this->agencia = $agencia;
        $this->conta = $conta;
        if ($saldo > 0) {
            $this->saldo = $saldo;
        }
    }

    public function depositar($quantia)
    {
        if ($quantia > 0) {
            $this->saldo += $quantia;
        }
    }

    public function getSaldo()
    {
        return $this->saldo;
    }

    public function getInfo()
    {
        return "Agencia {$this->agencia}, Conta {$this->conta}";
    }
}
```

* Criando classe ContaPoupanca

```php
class ContaPoupanca extends Conta
{
    public function retirar($quantia)
    {
        if ($this->saldo >= $quantia) {
            $this->saldo -= $quantia;
        }
        else
        {
            return false;
        }
        return true;
    }
}
```

* Criando classe ContaCorrente

```php
//Herdando todos os atributos e métodos da classe pai
class ContaCorrente extends Conta
{
    protected $limite;

    public function __construct($agencia, $conta, $saldo, $limite)
    {
        //usando o método construtor da classe pai
        parent::__construct($agencia, $conta, $saldo);

        $this->limite = $limite;
    }
    
    public function retirar($quantia)
    {
        if (($this->saldo + $this->limite) >= $quantia) {
            $this->saldo -= $quantia;
        }
        else
        {
            return false;
        }
        return true;
    }
}
```

* Usando as contas

```php
require_once 'classes/Conta.php';
require_once 'classes/ContaCorrente.php';
require_once 'classes/ContaPoupanca.php';

$p = new ContaPoupanca('100', '123123', 500);

//Os métodos foram herdados da classe Conta para a classe ContaPoupanca
$p->depositar( 200 );
echo $p->getSaldo();
$p->retirar( 100 );
```

### 3. Polimorfismo

``Método de mesmo nome porém uma implementação diferente;``

```php
require_once 'classes/Conta.php';
require_once 'classes/ContaCorrente.php';
require_once 'classes/ContaPoupanca.php';

$contas = [];
$contas[] = new ContaCorrente(1234, 'CC.1234', 100, 500);
$contas[] = new ContaPoupanca(1235, 'PP.4566', 100)

foreach ($contas as $conta)
{
    //O comando instanceof verifica se o objeto é filho de determinada classe
    if ($conta instanceof Conta) {
        print $conta->getInfo() . '<br>';
        print "-- Saldo atual: {$conta->getSaldo()} <br>";

        $conta->depositar(200);
        print "-- depósito de 200! <br>";
        print "-- Saldo atual: {$conta->getSaldo()} <br>";

        //O método retirar é de mesmo nome na ContaCorrente e na ContaPoupanca
        //mas a operação é realizada de forma diferente
        //observando que a ContaCorrente pode ter valores negativos no saldo e a ContaPoupanca não
        if ($conta->retirar( 700 )) {
            print "-- Retirada de 700 (OK) <br>";
        }
        else
        {
            print "-- Retirada  de 700 (não permitida) <br>";
        }
        print "-- Saldo atual: {$conta->getSaldo()} <br>";
    }
}
```

### 4. Abstração

* Classe abstrata

```php
//o abstract impede que objetos sejam criados a partir desta classe
//agora somente as classes filhas podem se criar objetos
//em outras palavras ela só pode ser usada para criação de outras classes
abstract class Conta
{
    ...
}
```

* Classe final

```php
//o final indica que não é possível criar um classe filha a partir desta classe
final class ContaPoupanca extends Conta
{
    ...
}
```

* Método Abstrato

```php
//obrigar que as classes filhas implementem determinado método assinado na classe pai
abstract class Conta
{
    ...
    abstract function retirar($quantia);//assinatura do método abstrato
    ...
}
```

* Método Final

```php
//Um método final não pode ser redefinido em uma classe final
class ContaPoupanca extends Conta
{
    ...
    public final function retirar($quantia)
    {
        ...
    }
    ...
}
```

### 5. Encapsulamento

``O encapsulamento visa proteger os atributos de uma classe a partir de métodos;``

``Ou seja, só quem poder realizar operações nesses atributos são os métodos;``

* ``Public``: pode ser acessado em qualquer contexto;

* ``Private``: só pode ser acessado pela própria classe, as classes filhas não podem acessar;

* ``Protected``: só pode ser acessado no contexto da classe pai e da filha;

### 6. Membros de Classe

``Os membros são valores definidos para a classe``

```php
class Pessoa
{
    private $nome;
    private $genero;

    //definindo uma constante que pertence a classe
    //isto é um membro da classe
    private const GENEROS = ['M' => 'Masculino', 'F' => 'Feminino'];

    public function __construct($nome, $genero)
    {
        $this->nome = $nome;
        $this->genero = $genero;
    }

    public function getNome()
    {
        return $this->nome;
    }

    public function getNomeGenero()
    {
        //o self é usado para se referenciar a própria classe
        //isso significa o mesmo de fazer: Pessoa::GENEROS[]
        //mas como estamos dentro da classe é usado o self
        return self::GENEROS[ $this->genero ];
    }
}

print Pessoa::GENEROS['F'];//não é possível acessar de fora porque é private

$p1 = new Pessoa('Maria da Silva', 'F');
$p2 = new Pessoa('Carlos Pereira', 'M');

print $p1->getNome() . '<br>';
print $p1->getNomeGenero() . '<br>';
print $p2->getNome() . '<br>';
print $p2->getNomeGenero() . '<br>';
```

* Métodos e Atributos static

```php
class Software
{
    //Criando um auto incremento no ID, atributo static
    private $id;
    private $nome;

    //Uma variável static armazena o seu valor mesmo depois da chamada de uma classe
    private static $contador;

    public function __construct($nome)
    {
        //novamente, o self é usado para fazer a referência a própria classe
        //é por meio dele que se pode acessar atributos e métodos da classe dentro dela mesma
        //isso se aplica ao que pertence a classe, para se referenciar ao objeto é usado o $this
        self::$contador ++;
        $this->id = self::$contador;
        $this->nome = $nome;
    }
}
//o id é gerado automaticamente
$s1 = new Software('Gimp');
$s2 = new Software('Gnumeric');
```
