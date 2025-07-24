---
theme: dracula
favicon: './image/vscodium.ico'
fonts:
  sans: Oswald
  serif: Source Sans Pro
---

# Présentation VSCode

6CEN AURA

<div class="pt-12">
  <span @click="next" class="px-2 p-1 rounded cursor-pointer hover:bg-white hover:bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

---

# Interface

Peut paraître complexe à première vue...

La barre de tâche permet de sélectionner des fichiers, à ouvrir ou un dossier qui vous servira de projet.
Vous pourrez naviguer dans les fichiers du projet et les modifier.

La barre de gauche permet de lister les extensions installées, par défaut on y trouve aussi l'explorateur de fichier, la recherche l'interface git, le deboggage, le magasin d'extension et la partie test. En bas de cette section on a les paramètres et ce qui concerne le profil.

Au centre, l'éditeur qui peut se séparer à la verticale et à l'horizontale pour afficher 2 fichiers en parallèles.

Sur la droite on a une vue dézoomée du fichier actuellement ouvert avec des éléments en surbrillance.

Sur le bas on a la console, les différents éléments de débuggage, le journal d'erreurs, etc...

---

# Possibilités infinies

Avec VSCode on peut :

* Développer (code, git, doc)
* Gérer des serveurs
* Gérer des BDD
* Faire de la prise de notes
* Editer des tableurs
* Faire des Slides
* etc...


---

# Création de profil

## Optimisation de VSCode

* Paramètres et Extensions peuvent être différent pour chaque profil
* Il faut éviter les profils "fourre-tout"hdfhd
* Comme pour QGIS, on a une augmentation des performances avec plusieurs profils

## Bonnes pratiques

* Créer un profil pour chaque cas d'usage
* Enregistrer ces profils sur un Git et les partager avec les autres membres des 6CEN
* Gestion des profils sur les serveurs distants

## Pour aller plus loin

* Synchronisation automatique des profils via **Settings sync**

---

# Code completion

* Comme beaucoup d'éditeur de code VSCode permet la complétion du code, c'est à dire qu'il vous proposera automatiquement des noms de variables, fonction selon ce que vous avez commencer à taper.

* Extensions pour chaque besoins (Php, Python, SQL, etc...)

* <span v-mark.box.red="1">La complétion avec TAB est possible</span>

---

# Git

* Conçu pour être utilisé avec Github (création de dépôt très simple).

## Autres plateformes

Compatible avec d'autres solution Git (Gitea, GitLab, Forgejo, Codeberg, etc...)

1. Création du dépôt au préalable via la plateforme ou ligne de commande

2. Ouvrir le dossier local depuis VSCode

3. Possible de réaliser toutes les opérations de logiciels de versionning

---

# Debug

## Principe

Nativement VSCode permet le débuggage du Javascript, mais il est également possible d'ajouter des extensions pour débugger le python par exemple.

Le debuggage permet de :

* faire avancer le code ligne par ligne en visualisant les résultats de chaque ligne

* créer des "breakpoints" afin de stopper le code à des endroits précis ou selon des conditions

* afficher l'évolution des variables et leur contenu ou encore le modifier

---

# Debug

## Commandes de débuggage

Les commandes sont assez simples, il n'y a que 6 boutons :

1. Lancer l'intégralité du script, il ne s'arrêtera que si il rencontre une erreur ou si rencontre un breakpoint.
2. Lancer la prochaine ligne uniquement
3. Rentrer dans la méthode ou la function et la suivre ligne par ligne
4. Sortir d'une fonction
5. Redémarrer le mode débuggage
6. Arrêter le mode débuggage

<div class="w-60 relative">
  <div class="relative w-50 h-40">
    <img
      v-motion
      :initial="{ x: 600, y: 400, scale: 2, rotate: 100 }"
      :enter="final"
      class="absolute inset-0 top-14"
      src="./image/debug_commands.png"
      alt=""
    />
  </div>
</div>

<!-- vue script setup scripts can be directly used in markdown, and will only affects current page -->
<script setup lang="ts">
const final = {
  x: 0,
  y: 0,
  rotate: 0,
  scale: 1,
  transition: {
    type: 'spring',
    damping: 10,
    stiffness: 20,
    mass: 2
  }
}
</script>

---

# Debug

## Breakpoints

On les ajoute en cliquant sur la gauche des chiffres indiquant le numéro de ligne.

plusieurs types de breakpoints sont disponibles :

* les **breakpoints classiques** qui vont stopper le code à la ligne où ils sont placés
* les **breakpoints log message**, qui ne stoppent pas le code mais renvoie un message dans la console de debuggage
* les **breakpoints par expression** qui stoppent que si l'expression renseignée est égale à True
* les **breakpoints hit count** qui ne stoppent qu'à partir du moment ou ils ont été parcourus un certain nombre de fois
* les **breakpoints qui vont attendre qu'un autre breakpoint soit atteint avant de pouvoir être atteint à leur tour** et stopper la commande

---
layout: image-right
image: './image/debug.png'
---

# Debug

## Evolution des variables

Dans le panneau de gauche, vous pouvez suivre l'évolution des variables, une nouvelle entrée est crée à chaque déclaration d'une nouvelle variable avec sa valeur.

En double-cliquant sur la valeur il est possible de la changer.

En appuyant sur <kbd>ctrl</kbd> + <kbd>alt</kbd> + <kbd>f</kbd> il est possible de faire une recherche dans les variables
---

# SSH avec KeePassXC

## Sous Windows

1. S'assurer que **OpenSSH soit activée** (powershell en mode administrateur)

    ```
    Get-Service ssh-agent | Set-Service -StartupType Automatic
    Start-Service ssh-agent
    ```

2. Installer KeepassXC (si ce n'est pas déjà fait)
3. Paramétrer l'**Agent SSH** (dans les paramètres généraux), cocher :  
    Activer l'intégration de l'agent SSH  
    Utiliser OpenSSH
4. Potentiellement redémarrer l'ordinateur
5. Créer une nouvelle entrée "SSH ip_du_serveur / hostname du serveur"
6. Créer un **MDP fort**, qui servira de passphrase

---

# SSH avec KeePassXC

7. Dans une nouvelle fenêtre Windows Powershell (sans activer le mode administrateur), créer une clé ssh dans le dossier souhaité :

    ```
    ssh-keygen -t ed25519 -f keepassxc3 -C "jgrillot"
    ```

    ed25519 = type de signature unique  
    keepassxc3 = nom du fichier contenant la signature, généralement l'adresse ip du serveur  
    "jgrillot" = commentaire de la signature pour l'identifier (nom d'utilisateur, nom de l'appareil, autre)

    2 fichiers seront créé 'keepassxc3' et keepassxc3.pub qui correspondent à la **clé privée** et la **clé publique**.

8. Renseigner la passphrase créer précédemment dans KeePassXC (2x)

9. Dans KeepassXC, se rendre dans l'entrée créé précédemment, dans <kbd>Avancé</kbd> ajouter un **nouveau fichier joints**, sélectionner la **clé privée** (fichier sans le .pub)

---

# SSH avec KeePassXC

10. Se rendre dans l'onglet <kbd>Agent SSH</kbd> :

    * ajouter le fichier en tant que fichier joint. La clé publique va apparaître.
    * cocher également les 2 premiers paramètres <kbd>Ajouter la clé à l'agent si la base de données est ouverte ou déverouillée</kbd> et <kbd>Supprimer la clé de l'agent si la base de données est fermée ou verrouillée</kbd>. Cela permet d'ajouter toutes les clés à l'agent SSH lors du déverouillage de la BDD et de les supprimer automatiquement lorsque celle-ci est vérouillée. Il est donc **obligatoire d'avoir KeePassXC ouvert et la base dévérouillée pour accéder aux serveurs via ssh** avec une clé.

    **Remarque** : On peut choisir de décocher la première case pour plus de sécurité et ajouter manuellement la clé à l'agent SSH avant d'essayer de s'y connecter en appuyant sur le bouton <kbd>Ajouter à l'agent</kbd> situé dans le même onglet.

---

# SSH avec KeePassXC

11. Si c'est un **serveur auquel vous vous êtes déjà connecté et avec lequel vous aviez déjà mis en place une méthode d'authorized_keys**  
    Se rendre sur le serveur, modifier la signature dans l'authorized_keys par la clé publique (déchiffrée) renseignée dans KeePassXC

12. Si vous ne vous êtes jamais connecté au serveur, il vous faudra vous y rendre une première fois par une méthode plus traditionnelle

    ```shell
    ssh username@ip -p numero_port
    ```

    Puis renseignez le MDP utilisateur  
    **Créer ou modifier le fichier authorized_keys** situé ici :

    ```shell
    nano ~/.ssh/authorized_keys
    ```

    **Coller la clé publique (déchiffrée) renseignée dans KeePassXC**

---

# SSH avec KeePassXC

13. **Relancez le service ssh** avec cette commande :

    ```bash
    sudo service ssh restart
    ```

14. Quittez le serveur, tenter de vous y connecter avec la **BDD KeePassXC fermé** en retapant la commande :

    ```bash
    ssh username@ip -p numero_port
    ```

    Si tout va bien, le **mdp utilisateur va vous être demander**  
    Faites <kbd>Ctrl</kbd> + <kbd>C</kbd>

15. **Ouvrez la BDD KeePassXC** puis relancer la commande dans Windows Powershel, si tout va bien, la **connexion devrait réussir**.

---

# SSH avec KeePassXC

## Paramétrage VsCodium

1. Téléchargez l'extension **Open Remote - SSH**
2. Cliquez sur l'icône de l'extension dans le panneau de gauche
3. Cliquez sur l'engrenage situé en haut à droite du volet qui vient d'apparaître
4. Un fichier config va s'ouvrir, c'est là où vous pourrez renseigner toutes vos connexions SSH

---

# SSH avec KeePassXC

5. Exemple de connexion :

    ```
    Host Nom du serveur
      HostName 10.25.68.24
      User nom_utilisateur
      Port 22
      PreferredAuthentications publickey
      ForwardAgent no
      IdentitiesOnly yes
      IdentityFile //lien/vers/public_key/10.25.68.24.pub
    ```

- **PreferredAuthentications publickey** sert à prioriser la méthode d'authentification via une paire de clés, une publique et une privée
* **ForwardAgent no** si paramétrer sur oui permet de déplacer l'agent SSH au sein de la connexion SSH afin de se connecter à partir de cette dernière aux autres connexion de l'agent, pas forcément secure de balader son agent SSH partout.
* **IdentitiesOnly yes** Force la connexion à passer par un fichier d'identité
* **IdentityFile //lien/vers/public_key/10.25.68.24.pub** Lien vers la clé publique qui permettra à KeePassXC de trouver la clé privé à utiliser pour se connecter au serveur qui lui possède également la clé publique. La connexion ne peut pas se faire entre 2 clés publiques.

---

# SSH avec KeePassXC

6. Une fois toutes vos connexions SSH renseignées, elles apparaîtront dans le volet de l'extension
7. Si vous avez l'extension KeePassXC déverrouillée, vous pouvez lancer la connexion SSH en cliquant sur la connexion créer précédemment dans KeePassXC
8. Fermez la fenêtre, fermez la BDD KeePassXC et réessayez, VsCodium vous demandera le MDP de l'utilisateur

---

# SSH avec KeePassXC
## Mise en place à Asters

Actuellement toutes nos clés SSH privées sont stockées dans KeePassXC et elles sont ajoutées à l'Agent SSH à chaque déverouillage de la BDD et supprimées dès que celle-ci est fermée.

Nos clés publiques sont stockées sur notre serveur de fichier partager, nous n'avons besoin que d'une seule clé pour 2.

Nous avons également un fichier de configuration commun.

Pour ajouter le fichier de configuration à l'extension remote SSH de VSCodium :
* se rendre dans les paramètres (<kbd>Ctrl</kbd> + <kbd>,</kbd>)
* dans la barre de recherche taper **Remote.SSH: Config File**
* un seul paramètre va apparaître, ajouter le chemin vers votre dossier de config.

---

# BDD

Outil **SQLTools**, je ne l'utilise pas pour l'instant je suis toujours sur PgAdmin, mais je cherche à changer ça.
Peut être complémentaire niveau sécurité avec le SSH. Obligation de se connecter en SSH pour avoir accès à certains compte admin.

Permet de se connecter à une BDD sans enregistrer le MDP en dur dans un fichier de configuration contrairement aux autres extensions.
Possibilité d'enregistrer des requêtes et d'avoir un historique des requêtes faites.

Pas plus testé pour l'instant.
Possibilité de faire du SQLite également.

---

# Live Server

Très pratique pour le développement web.

Permet de créer un mini server en local et d'afficher directement les modifications faites sur le code.

Pour le webmapping, on évite les erreurs de CORS avec des données en local, ce qui est pratique.

---

# CodeTogether

Outil permettant de rejoindre une autre personne sur un projet de développement et de présenter le code, le mettre à jour, etc.

Pratique mais un peu instable, la visio n'est pas au point.
