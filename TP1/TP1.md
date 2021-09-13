<!--- 
Ceci est la version en markdown !
Utilisez l'aperçu pour avoir une version plus lisible
-->
# Terraform - TP1 : CLI - Utilisation basique

> **Objectifs du TP** :
>- Valider l’installation de Terraform
>- Valider l’accès au compte AWS
>- Se familiariser avec les commandes de base de Terraform
>

## 1- Objectifs détaillés

Pour les besoins de l’exercice, j'ai pré-installé la stack de base qui n'apparaît pas dans votre code pour simplifier les bases.
Nous allons commencer par prendre en main l'outil en ligne de commande permettant de créer et gérer des ressources sur AWS avec Terraform. 

L’objectif ici sera de déployer une instance EC2 (une VM)

## 2- Commandes de base de Terraform 

Vérifier/corriger la syntaxe terraform:
```bash
$ terraform fmt
```

Initialiser le provider:
```bash
$ terraform init
```

Visualiser le plan d'exécution:
```bash
$ terraform plan
```

Appliquer le plan d'exécution:
```bash
$ terraform apply
```

## 2- Création de la Topology

Créez le fichier `topology.tf` dans le dossier du TP1 (attention, c'est important de respecter l'arborescence !) avec le contenu suivant, en remplançant `var.user` par le user qui vous a été transmit sous le format `"nom.prenom"` : 

```tf

# Création d'une instance
resource "aws_instance" "web" {
  ami                    = "ami-0e3f7a235a05f8e99"
  instance_type          = "t2.micro"               

  tags = {
    Name      = var.user
    Formation = "terraform"
    TP        = "TP1"
  }
}

```

Si vous êtes sur WINDOWS ajoutez ceci au fichier `topology.tf` déjà créé afin de pouvoir utiliser l'outil Terraform :

```tf 
provider "aws" {
  region     = "eu-west-1"
  access_key = "<id>"
  secret_key = "<secret>"
}
```


Une fois le tout renseigné, lancez succèssivement les commandes suivantes : 

```bash
$ terraform fmt
```

Initialiser le provider:
```bash
$ terraform init
```

Visualiser le plan d'exécution:
```bash
$ terraform plan
```
Vous l'aurez remarquer, comme vous n'avez pas renseigner la variable "user", il vous est demandé de la renseigné au moment du lancement de la commande.
Renseignez-y la valeur qui vous a été fournie sous le format "nom.prenom" normalement.

Vous aurez à faire la même chose dans la commande ci-dessous.

Appliquer le plan d'exécution puis écrire "yes" sur l'input demandé par le terminal:
```bash
$ terraform apply
```

Vous devriez voir le message :
`Apply complete! Resources: 1 added, 0 changed, 0 destroyed.`

Bien joué si c'est le cas, vous venez de créer votre première instance AWS en Infra as Code ! PogU 

N'hésitez pas à relancer la commande `terraform apply` afin de vérifier le concept d'Idempotence. Jetez un oeil au contenu du fichier `terraform.tfstate` également afin de voir ce qui s'y trouve.

## 3- Un petit coup de ménage pour finir

Pour détruire votre topology plus qu'à lancer la commande suivante et écrire "yes" pour valider votre action :
```bash
$ terraform destroy
```

## 4- Bonus: Voir le graphe de dépendance

Pour consulter le graphe votre topology et comprendre comment se font les liens entre vos ressources :
```bash
$ terraform graph -draw-cycles
```

Vous pourrez ainsi savoir quels sont les liens entre les ressources.

Vous pouvez également en faire des images, il faudra cependant installer l'outil `brew install graphviz` (https://graphviz.org/download/) puis utilisez la commande suivante : 

```bash
$ terraform graph | dot -Tsvg > graph.svg
```
