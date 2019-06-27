# Tips Git

Ce README est un condensé d'informations techniques et pratiques, ayant pour objectif de présenter les actions les plus courantes dans l'utilisation de GitHub, et plus largement de Git, afin que chacun puisse rapidement appréhender la mise en oeuvre et la gestion de son propre dépôt Git. \
**Remarque** : nous travaillons ici sous **Linux**, il faudra adapter quelques commandes pour travailler sous un environnement Windows ou MacOS.

## 1. Installation Git sous Linux

> Objet : installer git sous Linux
```bash
# Pour les Linux dérivés de Debian
apt-get install git
# Pour les Linux dérivés de RedHat
$ yum install git

$ git config --global user.name <user_git>
$ git config --global user.email <user_mail>
$ git config --global push.default matching
```

## 2. Configuration des clés SSH

> Objet : automatiser et sécuriser l'autentification à GitHub via SSH
```bash
$ cd && mkdir .ssh && cd .ssh
$ ssh-keygen -t rsa -b 4096 -C "user@mail.fr"
```
Deux fichiers sont créés dans \$HOME/.ssh :
- id_rsa : la clé privée
- id_rsa.pub : la clé publique

Editer la clé publique :
```bash
$ cat id_rsa.pub
```
 Résultat à copier/coller sur GitHub section Settings / SSH and GPG Keys / New SSH key.
 > https://github.com/settings/keys
 ```
 # Contrôler si l'agent ssh est en cours d'exécution :
 eval "$(ssh-agent -s)"
 # Ajouter la clé privée à l'agent de gestion des connexions SSH
 ssh-add ~/.ssh/id_rsa
 # Lister les clés enregistrées
 ssh-add -l
 ssh-add -L
 ```
On peut alors sans avoir à fournir de user/pass redescendre un de ses propres repositories Git depuis GitHub via une commande du type :
```
git clone git@github.com:user/monrepo.git
```
et surtout alimenter (push) ses repositories sans avoir à fournir de login/passwd. Pour cela il faut d'abord initialiser l'accès au Repository distant :
```
git remote set-url origin git@github.com:user/monrepo.git
git remote show origin
git push origin master
```

> Plus d'infos : https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account

## 3. Environnement de développement

Astuce sympa pour faire apparaître la branche courante dans le prompt sous Linux Debian et dérivés (Mint...) \
(A adapter pour les types RHEL/CentOS) \
Code à ajouter dans le .bashrc par exemple :
```
function getbranch () {
	if [[ -d .git ]]; then
		echo "[$(git symbolic-ref HEAD --short)] "
	else
		echo ""
	fi
}

export PS1="\[\e]0;\u@\h \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\] \[\033[01;34m\]\w \$(getbranch)\$\[\033[00m\]"
```

## 4. Commandes courantes

### a. Command line instructions with SSH
```
Git global setup

git config --global user.name "My Name"
git config --global user.email "my.name@foo.fr"

Create a new repository

git clone ssh://git@gitlab.mongitlab.fr:922/groupe/projet.git
cd images-docker
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master

Existing folder

cd existing_folder
git init
git remote add origin ssh://git@gitlab.mongitlab.fr:922/groupe/projet.git
git add .
git commit -m "Initial commit"
git push -u origin master

Existing Git repository

cd existing_repo
git remote add origin ssh://git@gitlab.mongitlab.fr:922/groupe/projet.git
git push -u origin --all
git push -u origin --tags
```

### b. Gestion d'une branche différenciée (demande de fusion...)
```bash
git remote add mabranche https://github.com/nik-hub/mon_repository/mabranche/
git push mabranche
```

## 5. Gestion de projets

> https://services.renater.fr/sourcesup/formation/chap04
