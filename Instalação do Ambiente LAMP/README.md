# Instalação do Ambiente LAMP

### Instalando o LAMP com PHP 7.2 e/ou superior

```

ATENÇÃO: ANTES DE EXECUTAR O PROCEDIMENTO LISTADO ABAIXO, RECOMENDA-SE QUE VOCÊ FIXE SEU IP ATRAVÉS DA CONFIGURAÇÃO DO COMPUTADOR E/OU VIA ROTEADOR (MAC)

```

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

![LAMP](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image6.png)

2.3 -> Nas linhas que estão escritas **AllowOverride** troque **None** por **All**. Em seguida aperte "CTRL + O" para salvar e "CTRL + X" para fechar o arquivo. 

3 -> Em seguida instalaremos o MySQL, executando os seguintes comandos:

 ```

sudo apt install wget

wget wget https://dev.mysql.com/get/mysql-apt-config_0.8.12-1_all.deb

sudo dpkg -i mysql-apt-config_0.8.12-1_all.deb

```

3.1 -> Selecione **Ubuntu bionic** e aperte Enter.

![LAMP](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image3.png)

3.2 -> Se no final da primeira linha estiver mysql-5.7 basta clicar em **Ok**, caso esteja como mysql-8.0 ou outro clique na primeira linha para selecionar outra versão.

 ![LAMP](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image5.png)

 3.3 -> Abrirá um menu de versão do mysql, selecione a versão 5.7 e aperte Enter, você voltará para a mesma tela da etapa anterior mas como já foi selecionado a versão 5.7, basta clicar em Ok e prosseguir.

 ![LAMP](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image4.png)

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
### Escolha qual versão do PHP você deseja utilizar:

#### - PHP 7.2

```

sudo apt install php7.2

sudo apt install php-pear php7.2-curl php7.2-dev php7.2-gd php7.2-mbstring php7.2-zip php7.2-mysql php7.2-xml libapache2-mod-php7.2 php7.2-common php7.2-intl php7.2-xsl php7.2-bcmath php7.2-soap php-xdebug php-imagick

 ```


#### - PHP 7.3

```

sudo apt install php7.3

sudo apt install php-pear php7.3-curl php7.3-dev php7.3-gd php7.3-mbstring php7.3-zip php7.3-mysql php7.3-xml

```

#### - PHP 7.4

```

sudo apt install php7.4

sudo apt install php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl libapache2-mod-php7.4 php7.4-xsl php7.4-bcmath php-xdebug php-imagick

```

6 -> Agora reiniciaremos o apache2 e habilitaremos a versão do php que você instalou substituindo o **" * "** pela versão. EX: (7.2, 7.3, 7.4) 

 ```

service apache2 restart

sudo a2enmod php*

service apache2 restart

 ```

7 -> Para facilitar o manuseio com banco de dados iremos instalar agora o phpmyadmin:

 ```

sudo apt install phpmyadmin

 ```

8 -> Após ter executado este comando você irá agora para tela de configuração do phpmyadmin, nesta primeira opção selecione **apache2** e aperte enter.

![phpmyadmin](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image1.png)

9 -> Agora o phpmyadmin irá pedir para você configurar o usuário root, selecione **Sim** e aperte Enter (essa configuração é necessária para o funcionamento do phpmyadmin).

![phpmyadmin](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image2.png)

10 -> Para facilitar o acesso ao phpmyadmin execute este comando para que seja criado um atalho do phpmyadmin na pasta /var/www/html e assim conseguindo acessar-lo por localhost no navegador:

```

sudo ln -s /usr/share/phpmyadmin /var/www/html

```
11 -> Para que você consiga acessar o phpMyAdmin de outros computadores ou usando seu IP, você precisa editar a configuração do apache, conforme abaixo:

> No terminal cole o comando abaixo:

```
sudo nano /etc/phpmyadmin/apache.conf

```
> Você deve inserir na tela que se abre o seguinte contéudo:

```
Alias /yournewalias /usr/share/phpmyadmin

```
> Feito isso pressione CTRL + O, salve o arquivo e posteriormente CTRL + X para sair do editor. Após retornar ao terminal você precisará reiniciar o Apache2, insira o comando abaixo:

```
sudo service apache2 restart

```

![acesso via ip](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image7.png)


12 -> Agora você deve acessar a pasta /var/www/html e excluir o arquivo *index.html*, pois ele não será mais necessário, caso desejar baixe o arquivo *phpinfo.php* contido neste tutorial e coloque na pasta /var/www/html o resultado esperado deve ser similar ao abaixo:


![phpinfo](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image8.png)


13 -> Para facilitar sua usabilidade insira o usuário do seu sistema operacional no grupo www-data (grupo do apache). Para isso siga os procedimentos listados abaixo:

> No terminal digite o seguinte comando:

```
grep www-data /etc/group

```
O resultado esperado deve ser:

![www-data](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image9.png)

> Note que seu usuário ainda não está no grupo, para executar a inserção digite:

```
sudo adduser {NOMEDOUSUARIO} www-data

```

Exemplo:

```
sudo adduser dev-01 www-data

```

O resultado esperado é:

![usuario em www-data](https://github.com/Buzz-Dev-Web/MaterialApoio/blob/main/Instalação%20do%20Ambiente%20LAMP/images/image10.png)

> Pronto usuário adicionado ao grupo www-data.

14 -> Instale também o Composer, que é usado para instalação do Magento e de seus módulos:

```

sudo apt install composer

```

15 -> Pronto, seu Ambiente LAMP já esta habilitado e funcionando. Para acessar o phpmyadmin utilize o usuário e a senha do mysql que foi criado na etapa 3 ou caso tenha instalado o MySQL 8.0, use a senha que você inseriu no passo 4.

<hr>

### Dúvidas?
Em caso de ainda houver alguma dúvida, chame seus supervisores para auxiliá-lo.