1 - Ter o Mysql, Apache2, PHP 7.x, composer instalados

2 - Executar o git clone do projeto no terminal ex.: git clone https://github.com/fernandofurbringer/hibrido.git

3 - Criar/alterar arquivo de conf e fazer o apontamento no apache default (/etc/apache2/sites-available) arquivo magento2.conf
    <VirtualHost *:80>
         ServerAdmin admin@domain.com
         DocumentRoot /home/fernando/magento2
         ServerName localhost.com
         ServerAlias www.localhost.com

         <Directory /home/fernando/magento2>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
         </Directory>

         ErrorLog ${APACHE_LOG_DIR}/error.log
         CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    
4 - Lembrar de adicionar as seguintes linhas no arquivo /etc/hosts

    127.0.0.1 localhost.com
    127.0.0.1 dev.com
    127.0.0.1 m2.com
    
5 - restart o servico do apache ex.: sudo service apache2 restart

6 - execute sudo composer update na pasta aonde deu o git clone do projeto

7 - caso nescessario de permissão a toda pasta ex.: sudo chmod -R 777 /home/fernando/magento2/

8 - acesse o projeto conforme foi configurado ex: localhost.com

9 - faça a instalação/configuraçao normalmente

10 - acesse o modulo com o <link>/getipvisitante
ex.: http://localhost.com/getipvisitante

11 - Comandos talvez nescessários para funcionamento do modulo:

    sudo bin/magento module:enable -c Hibrido_GetIpVisitante
    sudo bin/magento cache:flush
    sudo bin/magento setup:upgrade
    sudo bin/magento setup:di:compile
    sudo a2enmod rewrite
    sudo bin/magento indexer:reindex

**essa é pagina criada com um titulo e conteudo aleatório mantendo o template**

**O arquivo de Log é gerado no diretório Raiz do ssitema com o nome de logip.txt**

Obs.: para não ficar abrindo a pagina em cache eu tive que remover as opções de cache como uma solução rapida, para voltar a utilizar o cache só adicionar dentro do arquivo env.php localizado em <<magento project>>/app/etc:
    
    'cache_types' => [
        'config' => 1,
        'layout' => 1,
        'block_html' => 1,
        'collections' => 1,
        'reflection' => 1,
        'db_ddl' => 1,
        'compiled_config' => 1,
        'eav' => 1,
        'customer_notification' => 1,
        'config_integration' => 1,
        'config_integration_api' => 1,
        'full_page' => 1,
        'config_webservice' => 1,
        'translate' => 1
    ],

    
    
