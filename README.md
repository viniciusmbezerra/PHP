# PHP

## Instalação
1. [Instalar XAMPP](https://www.apachefriends.org/index.html)

2. Configurar ambiente de desenvolvimento, coloque as configurações no fim do arquivo:
    - C:\xampp\php\php.ini:
        - display_errors = On
        - memory_limit = 256M 
        - max_execution_time = 120 
        - error_reporting = E_ALL 
        - file_uploads = On 
        - post_max_size = 100M 
        - upload_max_filesize = 100M 
        - session.gc_maxlifetime = 14000
3. Configurar ambiente de produção, altere:
    - C:\xampp\php\php.ini:
        - display_errors = Off
        - error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT & ~E_NOTICE
4. Informações sobre o seu PHP:
    - abrir um arquivo php com o código:
        ```
        <?php 
            phpinfo(); 
        ?>
        ```
Arquivos do projeto -> C:\xampp\htdocs\projeto_x.<br>
Acessar a aplicação -> http://localhost/projeto_x.
