# Tips Git
## 1. ssh
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
On peut alors sans avoir à fournir de user/pass redescendre un repository Git depuis GitHub via une commande du type :
```
git clone git@github.com:user/monrepo.git
```
