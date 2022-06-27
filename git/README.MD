# GIT

## PREPARATION INITIALISATION

### préparation

git config --global user.email "ben@mail.fr"
git config --global user.name "benlamouche"

### voir autre commande

git help config

### voir config

git help config

### intialisation du dossier

git init

## STATUS ADD et COMMIT

### status du dossier

git status

### ajouter des fichier avant commit

git add  
git add --all  
git add *.html

### commit

git commit  
git commit -m "message"

### commit + add

git commit -a -m "message"

### modif commit précedent

git commit --amend

### modif commit précedent sans edition du log

git commit --amend --no-edit

### fichier listant les fichier à ne pas suivre

.gitignore

## LOG

### voir les commit

git log

### voir 5  dernier commit

git log -n 5

### voir commit en une ligne

git log --oneline

## DIFFÉRRENCE

git diff

## RETOUR AR

### retour sans perte

### commit impossible

git checkout e3299f8  
git checkout master

## RETOUR AR 1 FICHIER + COMMIT

git checkout e3299f8 index.html  
git commit  
git checkout master index.html

### retour et ajout à l'historique

git revert e3299f8

## RESET

### efface les add sans modif espace de travaille

git reset

### retour en arriere dans l historique sans modif espace de travaille

git reset e3299f8

### vide les add modifie historique sans modif fichier

git reset [monFichier.html]

### ne vide pas les add

git reset --soft [nr commit]

### need add (par defaut)

git reset --mixed [nr commit]

### efface definitvement les modif

git reset --hard [nr commit]

### retour de 2 commit en arriére

git reset HEAD^^

### retour et efface des modif de 1 commit en arriére

git reset --hard HEAD^

## BRANCHES

### création de branche

git branch maBranche

### se placer dans une branch

git checkout maBranche

### retour branche principale

git checkout master

### fusion branches

se placer sur le branche ou on veut importer

git merge maBranche

## A TRAVAILLER

git merge --no-ff maBranche

### supression branch

git branch -d maBranche

## MODIFF HISTORIQUE

## REBASE TRANSFERT LES COMMIT ENTRE BRANCHES

### rebase

### se placer sur le branche d'ou on veut exporter

### exporte commit sur l'autre branch

git rebase master

### retour sur branch importer

git checkout master

### merge

git merge maBranche

### rebase interactif

git rebase -i maBranche

## MISE MODIFF EN ATTENTE

### mettre les derniere modif en attente

git stash

### réapliquer ces modif

git stash apply

### lister les modif en attente

git stash list

### voir une modif

git stash show 'stash@{0}'

### efface la modif en attente

git stash drop

### aply + drop

git stash pop

### creer une branch a partir

git stash branch 'branchName'

### include untraked

git stash -u

## SSH

ssh-keygen -t rsa -b 4096 -C "johndoe@example.com"

## REMOTE

### creer un depot dans un dossier vide

git init --bare

### liste remote

git remote -v

### ajout remote

git remote add nom_remote adress_remote

### renomage remote

git remote rename ancien_nom nouveau_nom

### voir branch sur remote

git branch -r

## PUSH

git push nom_remote nom_branch  
git push --all nom_remote  
git push nom_remote --delete nom_branch

## PULL

git pull nom_remote nom_branch  
git pull --rebase nom_remote nom_branch  
git config --global branch.autosetuprebase always

## FETCH + MERGE

git fetch  
git merge

## CLONE

## creer un dossier qui clone un depot (profondeur)

git clone [--depth 5] adress_remote dossier_a_creer

## TRACKING REMOTE

### creer un branche avec option tracking

git branch --track dev origin/dev

### tracking sur une brache existante

```sh
git branch (--set-upstream-to=<upstream> | -u <upstream>) [<branchname>]
```
