# AD : Exemple de GPO

## Désactivation du Panneau de Configuration Windows

Nous allons dans un premier temps ouvrir le `Group Policy Management`

![WIN_AD_GPO_01](attachment/WIN_AD_GPO_01.jpg)

Déployez l'abrorescence de votre forêt jusqu'à voir votre Unité Organisationnelle

![WIN_AD_GPO_02](attachment/WIN_AD_GPO_02.jpg)

Clique-droit sur votre Unité Organisationnelle puis `Create a GPO in this domain and Link it here`

![WIN_AD_GPO_03](attachment/WIN_AD_GPO_03.jpg)

Reamplissez le champ `Name` puis cliquez sur `OK`

![WIN_AD_GPO_04](attachment/WIN_AD_GPO_04.jpg)

Clique-droit sur votre GPO puis `Edit`

![WIN_AD_GPO_05](attachment/WIN_AD_GPO_05.jpg)

Cliquez sur `User Configuration`

![WIN_AD_GPO_06](attachment/WIN_AD_GPO_06.jpg)

Cliquez sur `Policies`

![WIN_AD_GPO_07](attachment/WIN_AD_GPO_07.jpg)

Cliquez sur `Administration Templates`

![WIN_AD_GPO_08](attachment/WIN_AD_GPO_08.jpg)

Cliquez sur `Control Panel`

![WIN_AD_GPO_09](attachment/WIN_AD_GPO_09.jpg)

Sélectionnez `Prohibit access to Control Panel and PC Settings`

![WIN_AD_GPO_10](attachment/WIN_AD_GPO_10.jpg)

Sélectionnez l'option `Enabled` puis cliquez sur `Apply` puis `OK`

![WIN_AD_GPO_11](attachment/WIN_AD_GPO_11.jpg)

L'accés au Panneau de Configuration Windows est désormais bloqué pour les Utilisateur de l'Unité Organisationnelle

![WIN_AD_GPO_12](attachment/WIN_AD_GPO_12.jpg)

La nouvelle GPO apparait bien dans le Group Policy Managment pour notre Unité

![WIN_AD_GPO_13](attachment/WIN_AD_GPO_13.jpg)