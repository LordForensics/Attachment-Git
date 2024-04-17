# AD: Les Unités Organisationnelles

Dans un premier temps, il nous faut accéder au Centre d'Administration AD, vous y avez accés en faisant une recherche dans la barre Windows

![Win_AD_Config_01](attachment/WIN_AD_Config_01.jpg)

Sélectionnez la ligne de notre Domains AD, ici `wilders`

![Win_AD_Config_02](attachment/WIN_AD_Config_02.jpg)

Il faut tout d'abord créer une Unité Organisationnelle

Cliquez sur `New` puis `OrganisationUnit`

![Win_AD_Config_03](attachment/WIN_AD_Config_03.jpg)

Remplissez le champ `Name`, dans notre cas `Wilders_students` puis `OK`

![Win_AD_Config_04](attachment/WIN_AD_Config_04.jpg)

Nous allons ensuite ajouter un Groupe d'Utilisateurs

Clique-droit sur votre Unité Organisationnelle, puis `New` puis `Group`

![Win_AD_Config_05](attachment/WIN_AD_Config_05.jpg)

Remplissez les champs `Group name` et `Group SAM`, ici nous mettons `Students` puis `OK`

![Win_AD_Config_06](attachment/WIN_AD_Config_06.jpg)

Nous allons enfin ajouter un utilisateur

Clique-droit sur `New` puis `User`

![Win_AD_Config_07](attachment/WIN_AD_Config_07.jpg)

Remplissez les champs `Full name` et `User SAM` puis `OK`

![Win_AD_Config_08](attachment/WIN_AD_Config_08.jpg)

Nous allons pour terminer ajouter l'Utilisateur au Groupe

Clique-droit sur l'Utilisateur puis `Add to group`

![Win_AD_Config_09](attachment/WIN_AD_Config_09.jpg)

Cliquez sur `Locations`

![Win_AD_Config_10](attachment/WIN_AD_Config_10.jpg)

Développez l'arborescence du Domain AD

![Win_AD_Config_11](attachment/WIN_AD_Config_11.jpg)

Sélectionnez l'Unité Organisationnelle puis `OK`

![Win_AD_Config_12](attachment/WIN_AD_Config_12.jpg)

Remplissez le champ `Enter the object names to select` puis cliquez sur `Check names`

Si l'objet existe, il va être souligné

Cliquez sur `OK`

![Win_AD_Config_13](attachment/WIN_AD_Config_13.jpg)

Après vérification, votre Utilisateur a bien été ajouté au Groupe

![Win_AD_Config_14](attachment/WIN_AD_Config_14.jpg)