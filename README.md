# Tips Git
## 1. Install
```
apt-get install git
git config --global user.name <user_git>
git config --global user.email <user_mail>
git config --global push.default matching
```
## 2. SSH
> Repository : github \
> OS : Linux \
> Objet : automatiser et sécuriser l'autentification à GitHub via SSH
```
cd && mkdir .ssh && cd .ssh
ssh-keygen -t rsa -b 4096 -C "user@mail.fr"
```
Deux fichiers sont créés dans \$HOME/.ssh :
- id_rsa : la clé privée
- id_rsa.pub : la clé publique
```
cat id_rsa.pub
```
 Résultat à copier/coller sur GitHub section Settings / SSH and GPG Keys / New SSH key.
 > https://github.com/settings/keys
 ```
 # Contrôler si l'agent ssh est en cours d'exécution :
 eval "$(ssh-agent -s)"
 # Ajouter la clé privée à l'agent de gestion des connexions SSH
 ssh-add ~/.ssh/id_rsa
 ```
On peut alors sans avoir à fournir de user/pass redescendre un de ses propres repositories Git depuis GitHub via une commande du type :
```
git clone git@github.com:user/monrepo.git
```
et surtout alimenter (push) ses repositories sans avoir à fournir de login/passwd !
> Plus d'infos : https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account
