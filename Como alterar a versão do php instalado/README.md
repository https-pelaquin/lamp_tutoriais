# Como mudar a versão do PHP que está ativa na máquina

Dependendo da situação é preciso utilizar uma versão do php diferente do que está ativo em sua máquina. Exemplo: você está usando o php7.2 e precisa instalar um magento 2.4* que requer o php7.4, então você instala o 7.4 e por ele ser mais recente ele sobrepoe automaticamente o 7.2, mas e se você precisar voltar a usar o 7.2? Como que faz?

### Habilitando o PHP 7.2 como padrão do ambiente

1 -> Iremos "setar" o php7.2 como padrão da máquina, logo em seguida iremos ativar o php no apache2 e dar um restart.

```

sudo update-alternatives --set php /usr/bin/php7.2

sudo a2dismod (versão do php ativa no momento)

service apache2 restart

sudo a2enmod php7.2

service apache2 restart

```

### Habilitando o PHP 7.3 como padrão do ambiente

1 -> Para "setar" o php7.3 para padrão do ambiente, execute os comandos abaixo sendo eles para habilitar, ativar no apache2 e dar restart no ambiente.

```

sudo update-alternatives --set php /usr/bin/php7.3

sudo a2dismod (versão do php ativa no momento)

service apache2 restart

sudo a2enmod php7.3

service apache2 restart

```

### Habilitando o PHP 7.4 como padrão do ambiente

1 -> Por ultimo, agora iremos ver como "setar" o php 7.4 como padrão do ambiente.

```

sudo update-alternatives --set php /usr/bin/php7.4

sudo a2dismod (versão do php ativa no momento)

service apache2 restart

sudo a2enmod php7.4

service apache2 restart

```

<hr>

### Dúvidas?
Em caso de ainda houver alguma dúvida, chame seus supervisores para auxiliá-lo.