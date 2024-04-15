# DNS sur Windows Server

## Présentation

Le serveur DNS agit comme un annuaire que consulte un ordinateur au moment d'accéder à un autre ordinateur via un réseau. Autrement dit, le serveur DNS est ce service qui permet d'associer à site web (ou un ordinateur connecté ou un serveur) une adresse IP, comme un annuaire téléphonique permet d'associer un numéro de téléphone à un nom d'abonné.

## Mise en contexte

Pour notre exemple, nous prendrons des machines virtuelles, le serveur sous Windows Server 2022 (SRV-WIN-DHCP), le client sous Windows 10 Pro (CLI-WIN-DHCP). Afin d'éviter toutes interférences, nous allons procéder en réseau interne, donc dépourvue de connexion avec l'extérieur.

Bien que le réseau soit interne, nous avons tout de même effectuer les mises à jour disponibles avant désactivation des cartes NAT.

Il ne sera pas mentionné la question d'Active Directory, nous aborderons ces points dans un autre tutoriel.

NB. Nous travaillerons avec une version de Windows Server en langue US, mais si vous l'utilisez dans une autre langue les options sont identiques, seuls les termes utilisés seront différents.

Notre serveur est configuré sur l'adresse IP fixe : 178.16.10.10/24

![Win_DHCP_Install_01](attachment/Win_DHCP_Install_01.jpg)

## Installation du DNS sur Windows Server

Une fois les mises à jour effectuées, rendez-vous sur le Server Manager

En toute logique, celui-ci se lance au démarrage, mais vous pouvez le démarrer via la barre de recherche Windows.

![Win_DHCP_Install_02](attachment/Win_DHCP_Install_02.jpg)

Une fois le Server Manager lancé, rendez-vous sur `Manage` (en haut à droite) puis sélectionnez `Add Roles and Features`

![Win_DHCP_Install_03](attachment/Win_DHCP_Install_03.jpg)

Une fenêtre va s'ouvrir, elle attire votre attention sur certains pré-requis pour continuer
* Le compte administrator doit avoir un mot de passe résistant
* Votre configuration réseau doit être configurée avec un IP fixe
* Les mises à jours de sécurité Windows doivent avoir été faites

![Win_DHCP_Install_04](attachment/Win_DHCP_Install_04.jpg)

Choississez ensuite l'otion `Role-based or featured-based installation` puis cliquez sur `Next`

![Win_DHCP_Install_05](attachment/Win_DHCP_Install_05.jpg)

Le serveur étant déjà en local, il est donc déjà selectioné, cliquez sur `Next`

![Win_DHCP_Install_06](attachment/Win_DHCP_Install_06.jpg)

Nous rentrons alors dans le vif du sujet, vous devez ajouter le rôle `DNS Server`

Une nouvelle fenêtre s'ouvre, assurez-vous d'avoir l'option `Include management tools (if applicable)` cochée, puis cliquez sur `Add Features`

La fenêtre se ferme, le rôle `DNS Server` est bien coché, cliquez sur `Next`

![WIN_DNS_Install_01](attachment/WIN_DNS_Install_01.jpg)

Dans l'onglet `Features`, laissez comme c'est et cliquez sur `Next`

![Win_DHCP_Install_08](attachment/Win_DHCP_Install_08.jpg)

L'installation du rôle `DHCP Server` est presque terminée, cliquez sur `Next`

![Win_DNS_Install_02](attachment/Win_DNS_Install_02.jpg)

Cliquez sur `Install` pour finaliser

![Win_DNS_Install_03](attachment/Win_DNS_Install_03.jpg)

Une fois l'installation terminée, cliquez sur `Close`

Votre serveur DNS est installé, il vous reste désormais à le configurer.

## Configuration du DNS sur le Serveur

### Configuration du DNS

Pour accéder à la configuration du DNS, vous pouvez recherchez l'application via la barre Windows en tapant `DNS`

![Win_DNS_Config_01](attachment/WIN_DNS_Config_01.jpg)

Il vous faut ensuite ajouter une zone pour faire autorité

Clique-droit sur `Forward Lookup Zones` puis sélectionez `New Zone`

![Win_DNS_Config_02](attachment/WIN_DNS_Config_02.jpg)

L'assistant d'installation se lance, cliquez sur `Next`

![Win_DNS_Config_03](attachment/WIN_DNS_Config_03.jpg)

Sélectionnez `Primary Zone` puis cliquez sur `Next`

![Win_DNS_Config_04](attachment/WIN_DNS_Config_04.jpg)

Remplissez le champ `Zone Name`, `wilders.lan` dans notre exemple, puis cliquez sur `Next`

![Win_DNS_Config_05](attachment/WIN_DNS_Config_05.jpg)

Sélectionnez `Create a new file with this file name`, le champ `wilders.lan.dns` est rempli automatiquement, puis cliquez sur `Next`

![Win_DNS_Config_06](attachment/WIN_DNS_Config_06.jpg)

Sélectionnez l'option `Do not allow dynamic updates` puis cliquez sur `Next`

![Win_DNS_Config_07](attachment/WIN_DNS_Config_07.jpg)

La configuration est terminé, cliquez sur `Finish` pour quitter l'assistant

![Win_DNS_Config_08](attachment/WIN_DNS_Config_08.jpg)

La zone de DNS a bien été créé

![Win_DNS_Config_09](attachment/WIN_DNS_Config_09.jpg)

### Configuration de l'annuaire inversé

Clique-droit sur `Reverse Lookup Zones` puis `New Zone`

![Win_DNS_Config_10](attachment/WIN_DNS_Config_10.jpg)

L'assistant se lance, cliquez sur `Next`

![Win_DNS_Config_11](attachment/WIN_DNS_Config_11.jpg)

Sélectionnez `Primary Zone` puis cliquez sur `Next`

![Win_DNS_Config_12](attachment/WIN_DNS_Config_12.jpg)

Sélectionnez `IPv4 Reverse Lookup Zone` puis cliquez sur `Next`

![Win_DNS_Config_13](attachment/WIN_DNS_Config_13.jpg)

Saisissez les 3 premiers octets de botre IP de serveur

![Win_DNS_Config_14](attachment/WIN_DNS_Config_14.jpg)

Dans notre exmple, c'est `178.16.10` puis cliquez sur `Next`

![Win_DNS_Config_15](attachment/WIN_DNS_Config_15.jpg)

Sélectionnez `Create a new file with this file name`, le champ `10.16.178.in-addr.arpa.dns` est rempli automatiquement, puis cliquez sur `Next`

![Win_DNS_Config_16](attachment/WIN_DNS_Config_16.jpg)

Sélectionnez l'option `Do not allow dynamic updates` puis cliquez sur `Next`

![Win_DNS_Config_17](attachment/WIN_DNS_Config_17.jpg)

La configuration est terminé, cliquez sur `Finish` pour quitter l'assistant

![Win_DNS_Config_18](attachment/WIN_DNS_Config_18.jpg)

La zone inversée de DNS a bien été créé

![Win_DNS_Config_19](attachment/WIN_DNS_Config_19.jpg)

### Configuration des hôtes

Clique-droit sur la fenêtre de la zone puis sélectionnez `New Host (A or AAAA)`

![Win_DNS_Config_20](attachment/WIN_DNS_Config_20.jpg)

Remplissez les champs `Name` et `IP Address`

![Win_DNS_Config_21](attachment/WIN_DNS_Config_21.jpg)

Dans notre cas, c'est `server` et l'IP `178.16.10.10`

Assure-vous de bien avoir la cas `Create associated pointer (PTR) record` cochée, puis cliquez sur `Add Host`

![Win_DNS_Config_22](attachment/WIN_DNS_Config_22.jpg)

Même opération pour le Client

![Win_DNS_Config_23](attachment/WIN_DNS_Config_23.jpg)

Les Hotes sont bien créés

![Win_DNS_Config_24](attachment/WIN_DNS_Config_24.jpg)

### Configuration de l'Alias

De la même façon que pour les hôtes, clique-droit sur la fenêtre puis `New Alias (CNAME)`

Remplissez les champs `Alias name`

![Win_DNS_Config_25](attachment/WIN_DNS_Config_25.jpg)

Dans notre exmple on met `dns`, puis à la ligne `Fully qualified doamin name`, cliquez sur `Browse`

![Win_DNS_Config_26](attachment/WIN_DNS_Config_26.jpg)

Sélectionnez votre Serveur puis cliquez sur `OK`

![Win_DNS_Config_27](attachment/WIN_DNS_Config_27.jpg)

Sélectionnez la zone de DNS puis cliquez sur `OK`

![Win_DNS_Config_28](attachment/WIN_DNS_Config_28.jpg)

Sélectionnez votre DNS puis cliquez sur `OK`

![Win_DNS_Config_29](attachment/WIN_DNS_Config_29.jpg)

Sélectionnez votre Hôte Serveur puis cliquez sur `OK`

![Win_DNS_Config_30](attachment/WIN_DNS_Config_30.jpg)

Cliquez pour terminer sur `Apply` puis `OK`

![Win_DNS_Config_31](attachment/WIN_DNS_Config_31.jpg)

Votre Alias de serveur est créé

![Win_DNS_Config_32](attachment/WIN_DNS_Config_32.jpg)

Plus qu'à inscrire votre DNS par défaut dans vos paramètres de carte réseau IPv4 avec l'IP de votre Serveur, ici `178.16.10.10`

![Win_DNS_Config_33](attachment/WIN_DNS_Config_33.jpg)

La configuration est terminée

## Vérification de la configuration DNS avec nslookup

Afin de vérifier la configuration, ouvrez le Command Prompt (ou Invite de Commande) en recherchant `cmd` dans la barre Windows

Vous n'avez ensuite qu'à faire votre recherche comme suit

Côté Serveur :

![Win_DNS_Config_34](attachment/WIN_DNS_Config_34.jpg)

Côté Client :

![Win_DNS_Config_35](attachment/WIN_DNS_Config_35.jpg)

On peut s'apercevoir ainsi que tout fonctionne

Enjoy :)