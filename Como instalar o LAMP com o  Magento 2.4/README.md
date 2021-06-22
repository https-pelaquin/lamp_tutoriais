# Como instalar o LAMP junto o magento 2.4.x 

1 -> Antes de iniciar a instalação do ambiente, você deve atualizar os diretórios do linux, executando os seguintes comandos:

 ```

sudo apt update

sudo apt upgrade

 ```

2 -> Partimos para a instalação do Apache2, executando o seguinte comando:

 ```

sudo apt install apache2

sudo a2enmod rewrite

service apache2 restart

 ```

 2.1 -> Após ter instalado o apache2 vá no terminal execute este comando para ter acesso ao arquivo .conf do apache.

```

sudo nano /etc/apache2/apache2.conf

```

2.2 -> Ao abrir o arquivo desça até encontrar esta parte do código:

![LAMP](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Como%20instalar%20o%20LAMP%20com%20o%20%20Magento%202.4/images/image6.png)

2.3 -> Nas linhas que estão escritas **AllowOverride** troque **None** por **All**. Em seguida aperte "CTRL + O" para salvar e "CTRL + X" para fechar o arquivo. 

3 -> Em seguida instalaremos o MySQL, executando os seguintes comandos:

 ```

sudo apt install wget

wget wget https://dev.mysql.com/get/mysql-apt-config_0.8.12-1_all.deb

sudo dpkg -i mysql-apt-config_0.8.12-1_all.deb

```

3.1 -> Selecione **Ubuntu bionic** e aperte Enter.

![LAMP](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Como%20instalar%20o%20LAMP%20com%20o%20%20Magento%202.4/images/image3.png)

3.2 -> Se no final da primeira linha estiver mysql-5.7 basta clicar em **Ok**, caso esteja como mysql-8.0 ou outro clique na primeira linha para selecionar outra versão.

 ![LAMP](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Como%20instalar%20o%20LAMP%20com%20o%20%20Magento%202.4/images/image5.png)

 3.3 -> Abrirá um menu de versão do mysql, selecione a versão 5.7 e aperte Enter, você voltará para a mesma tela da etapa anterior mas como já foi selecionado a versão 5.7, basta clicar em Ok e prosseguir.

 ![LAMP](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Como%20instalar%20o%20LAMP%20com%20o%20%20Magento%202.4/images/image4.png)

3.4 -> Agora finalizando a instalação, o MySQL irá pedir para você configurar a senha de acesso do root, coloque uma de facil memorização.

```

sudo apt update

sudo apt install mysql-client=5.7.34-1ubuntu18.04

sudo apt install mysql-community-server=5.7.34-1ubuntu18.04

sudo apt install mysql-server=5.7.34-1ubuntu18.04

 ```

4 -> Em caso de ser necessário instalar o MySQL 8.0  é preciso fazer algumas configurações para que o bancos de dados funcione corretamente:

 ```

sudo mysql

CREATE USER 'admin'@'%' IDENTIFIED WITH mysql_native_password BY 'senha';

GRANT all PRIVILEGES ON *.* TO 'admin'@'%';

FLUSH PRIVILEGES;

exit

 ```

Aqui estamos criando um usuario com todas as permições que o mysql 8.0 exige, no segundo comando em **senha** insira uma senha sua para acesso ao banco de dados local de sua máquina.

5 -> Para instalarmos o PHP junto com algumas bibliotecas precisamos antes adicionar um repositório ao linux para logo em seguida instalar o PHP e suas bibliotecas, execute os seguintes comandos separadamente:

 ```

sudo apt install software-properties-common

sudo add-apt-repository ppa:ondrej/php

sudo apt update

```

#### - PHP 7.4

```

sudo apt install php7.4

sudo apt install php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl libapache2-mod-php7.4 php7.4-xsl php7.4-bcmath php-xdebug php-imagick

```

6 -> Agora reiniciaremos o apache2 e habilitaremos a versão do php que você instalou substituindo o **" * "** pela versão. EX: (7.2, 7.3, 7.4) 

 ```

service apache2 restart

sudo a2enmod php7.4

service apache2 restart

 ```

7 -> Para facilitar o manuseio com banco de dados iremos instalar agora o phpmyadmin:

 ```

sudo apt install phpmyadmin

 ```

8 -> Após ter executado este comando você irá agora para tela de configuração do phpmyadmin, nesta primeira opção selecione **apache2** e aperte enter.

![phpmyadmin](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Como%20instalar%20o%20LAMP%20com%20o%20%20Magento%202.4/images/image1.png)

9 -> Agora o phpmyadmin irá pedir para você configurar o usuário root, selecione **Sim** e aperte Enter (essa configuração é necessária para o funcionamento do phpmyadmin).

![phpmyadmin](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Como%20instalar%20o%20LAMP%20com%20o%20%20Magento%202.4/images/image2.png)

10 -> Para facilitar o acesso ao phpmyadmin execute este comando para que seja criado um atalho do phpmyadmin na pasta /var/www/html e assim conseguindo acessar-lo por localhost no navegador:

```

sudo ln -s /usr/share/phpmyadmin /var/www/html

```

<hr>

## Instalando o Magento 2.4.x

1 -> Agora iremos instalar o Elasticsearch, componente fundamental para o funcionamento do magento 2.4.x, execute o seguintes comandos para instalar o Elasticsearch.

```

curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list

sudo apt update

sudo apt install elasticsearch

sudo systemctl start elasticsearch

sudo systemctl enable elasticsearch

```

2 -> Primeiramente você deve ir até o site oficial do magento e realizar o <a href="https://magento.com/tech-resources/download">DOWNLOAD</a> do zip da versão do magento que você deseja utilizar ou pegar o comando composer para para efetuar o download pelo terminal.

3 -> Extraia o arquivo na pasta em que você deseja instalar o magento e no terminal, navegue até o diretório onde o ZIP foi extraido.

**Importante:** antes de processeguir você já deve ter criado o banco de dados que será usado pelo magento.

4 -> No terminal execute o seguinte comando, realizando as devidas substituições dos itens em parenteses.

```

bin/magento setup:install --backend-frontname=(NOME DO PAINEL) --db-host=(HOST DO BD) --db-name=(NOME DO BD) --db-user=(USUÁRIO DO BD) --db-password=(SENHA DO BD) --admin-user=(NOME DO USUÁRIO) --admin-password=(SENHA DO USUÁRIO) --admin-email="(EMAIL DO USUÁRIO)" --admin-firstname=(PRIMEIRO NOME) --admin-lastname=(SEGUNDO NOME) --currency=BRL --session-save=files


```

5 -> O Magento 2.4.x conta com 2 fatores de autenticação e isso não é necessário para nós, então desabilite-o rodando o seguinte comando no terminal:

```

bin/magento module:disable -c Magento_TwoFactorAuth

```

6 -> Pronto, agora seu Magento está instalado e configurado.