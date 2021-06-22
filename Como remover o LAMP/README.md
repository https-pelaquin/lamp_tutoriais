# Como remover o LAMP

### Apache

```

sudo apt remove --purge apache*

sudo apt autoremove

```

### MySQL

Substiua o **" * "** pela versão do mysql que você deseja remover, caso você queira remover todas as versões que estão instaladas na máquina basta deixar o **" * "**.

```

sudo apt remove --purge mysql*

sudo apt autoremove

sudo rm -rf /var/lib/mysql

sudo rm -rf /etc/mysql

```

### PHP

Substiua o **" * "** pela versão do PHP que você deseja remover, caso você queira remover todas as versões que estão instaladas na máquina basta deixar o **" * "**.

```

sudo apt remove --purge php*

sudo apt autoremove

```

### PHPMYADMIN

```

sudo apt remove --purge phpmyadmin*

sudo apt autoremove

sudo apt autoclean

```

### Remover tudo de uma vez

```

sudo apt remove --purge apache*; sudo apt remove --purge mysql*; sudo rm -rf /var/lib/mysql; sudo rm -rf /etc/mysql; sudo apt remove --purge phpmyadmin*; sudo apt autoremove; sudo apt autoclean

```

<hr>

### Dúvidas?
Chame seus supervisores.