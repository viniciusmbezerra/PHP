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

1. Estrutura do código

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

2. Variáveis

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

3. Tipagem
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
