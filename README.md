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
