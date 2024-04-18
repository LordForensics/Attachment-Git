# AD DS sur Windows Server

## Mise en contexte

Pour notre exemple, nous prendrons des machines virtuelles, le serveur sous Windows Server 2022 (SRV-WIN-DHCP), le client sous Windows 10 Pro (CLI-WIN-DHCP). Afin d'éviter toutes interférences, nous allons procéder en réseau interne, donc dépourvue de connexion avec l'extérieur.

Bien que le réseau soit interne, nous avons tout de même effectuer les mises à jour disponibles avant désactivation des cartes NAT.

Il ne sera pas mentionné la question de DNS et d'Active Directory, nous aborderons ces points dans un autre tutoriel.

NB. Nous travaillerons avec une version de Windows Server en langue US, mais si vous l'utilisez dans une autre langue les options sont identiques, seuls les termes utilisés seront différents.

Notre serveur est configuré sur l'adresse IP fixe : 178.16.10.10/24

![Win_DHCP_Install_01](attachment/Win_DHCP_Install_01.jpg)

## Installattion de AD-DS sur Windows Server

Il est temps de se rendre sur le Server Manager. En toute logique, celui-ci se lance au démarrage, mais vous pouvez le démarrer via la barre de recherche Windows.

![Win_DHCP_Install_02](attachment/Win_DHCP_Install_02.jpg)

Une fois le Server Manager lancé, rendez-vous sur `Manage` (en haut à droite) puis sélectionnez `Add Roles and Features`

![Win_DHCP_Install_03](attachment/Win_DHCP_Install_03.jpg)

Une fenêtre va s'ouvrir, elle attire votre attention sur certains pré-requis pour continuer
* Le compte administrator doit avoir un mot de passe résistant
* Votre configuration réseau doit être configurée avec un IP fixe
* Les mises à jours de sécurité Windows doivent avoir été faites

Une fois toutes cas tâches validées, vous pouvez cliquer sur `Next`

![Win_DHCP_Install_04](attachment/Win_DHCP_Install_04.jpg)

Choississez ensuite l'otion `Role-based or featured-based installation` puis cliquez sur `Next`

![Win_DHCP_Install_05](attachment/Win_DHCP_Install_05.jpg)

Le serveur étant déjà en local, il est donc déjà selectioné, cliquez sur `Next`

![Win_DHCP_Install_06](attachment/Win_DHCP_Install_06.jpg)

Nous rentrons alors dans le vif du sujet, vous devez ajouter le rôle `Active Directory Domain Services`

Une nouvelle fenêtre s'ouvre, assurez-vous d'avoir l'option `Include management tools (if applicable)` cochée, puis cliquez sur `Add Features`

La fenêtre se ferme, le rôle `Active Directory Domain Services` est bien coché, cliquez sur `Next`

![Win_AD_Install_01](attachment/WIN_AD_Install_01.jpg)

Dans l'onglet `Features`, laissez comme c'est et cliquez sur `Next`

![Win_DHCP_Install_08](attachment/Win_DHCP_Install_08.jpg)

L'installation du rôle `Active Directory Domain Services` est presque terminée, cliquez sur `Next`

![Win_AD_Install_02](attachment/WIN_AD_Install_02.jpg)

Cliquez sur `Install` pour finaliser

![Win_AD_Install_03](attachment/WIN_AD_Install_03.jpg)

A la fin de l'installation, un message vous avertit qu'une configuration est requise, et vous avez notamment une ligne `Promote this server to a domain controller`, cliquez sur cette ligne afin de convertir votre Serveur en Contrôleur de Domaine du réseau

![Win_AD_Install_04](attachment/WIN_AD_Install_04.jpg)

Une nouvelle fenêtre s'ouvre, c'est ici que nous allons ajouter un domaine, dans notre cas c'est un premier serveur d'un nouveau réseau, donc nous choisissons `Add a new forest`, puis nous remplissons le champ `Root domain name` et nous cliquons sur `Next`

![Win_AD_Install_05](attachment/WIN_AD_Install_05.jpg)

Il faut alors s'assurer que l'option `Catalogue Global` est bien cochée, dans notre cas, il s'agit également d'un serveur DNS donc l'option est validée

Saisissez un Mot de passe et sa confirmation, puis cliquez sur `Next`

![Win_AD_Install_06](attachment/WIN_AD_Install_06.jpg)

Sur l'onglet suivant, un message vous alerte sur la délégation du serveur, mais il n'y a rien à faire à cette étape, cliquez sur `Next`

![Win_AD_Install_07](attachment/WIN_AD_Install_07.jpg)

Vous changez d'onglet, le champ `The NetBios domain name` est rempli automatiquement, cliquez sur `Next`

![Win_AD_Install_08](attachment/WIN_AD_Install_08.jpg)

Il en est de même pour l'onglet `Path`, cliquez sur `Next`

![Win_AD_Install_09](attachment/WIN_AD_Install_09.jpg)

Sur l'onglet `Review options`, vérifiez vos paramètres et cliquez sur `Next`

![Win_AD_Install_10](attachment/WIN_AD_Install_10.jpg)

Toutes les vérifications de pré-requis sont validées (bandeau en haut), la fenêtre attire tout de même votre attention sur certains points, mais surtout que le Serveur peut redémarrer lors de l'installation, cliquez sur `Install`

![Win_AD_Install_11](attachment/WIN_AD_Install_11.jpg)

Une fois que le Serveur a redémarré des suites de l'nstallation, vous pourrez remarquer que la page de connexion au Serveur a changé, le `Domain name` a bien été pris en compte

![Win_AD_Install_12](attachment/WIN_AD_Install_12.jpg)

L'installation est terminée. Tous nos services sont opérationnels

![Win_AD_Install_13](attachment/WIN_AD_Install_13.jpg)
