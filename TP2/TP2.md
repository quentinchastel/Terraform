<!--- 
Ceci est la version en markdown !
Utilisez l'aperçu pour avoir une version plus lisible
-->
# Terraform - TP2: Syntaxe HCL - Utilisation basique

> **Objectifs du TP** :
>- Se familiariser avec la déclaration de ressources AWS via Terraform
>- Manipuler les commandes de base de Terraform
>- Comprendre le fonctionnement et la manipulation des ressources
>

## 1- Objectifs détaillés

Dans ce TP, nous allons déployer une Topologie composée de :
* un subnet
* un Security Group autorisant le port 80 en entrée
* une instance
* un disque attaché à l’instance

Nous allons donc utiliser différentes ressources aws.

La documentation terraform associé à AWS est disponible [ici](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

Attention, la documentation commence par la partie datasource, dans ce tp nous utiliserons que la partie ressource disponible plus bas dans la page.


## 2- Création de la topology

Ouvrir le fichier topology.tf et y implementer les ressources décrites ci-dessous avec les informations suivantes:

Un subnet, s'appelant my_subnet, composé:
* d'un attribut "availability_zone" avec la valeur: 
* d'un attribut "cidr_block" avec la valeur: 
* d'un attribut "vpc_id" avec la valeur: 
* d’un tag "Name" valant : 
* d’un tag "Formation" valant : 
* d’un tag "User" valant :

Un security group, s'appelant my_security_group, composé:
* d'un attribut "name_prefix"  valant : 
* d'un attribut "vpc_id" avec la valeur:
* d’un tag "Name" valant :
* d’un tag "Formation" valant :
* d’un tag "User" valant :

Une règle de security group, s'appelant my_security_group_rule_out_http, composée:
* d'un attribut "type" correspondant au flux sortant
* d'un attribut "from_port" valant :
* d'un attribut "to_port" valant :
* d'un attribut "protocol" valant : 
* d'un attribut "cidr_blocks" acceptant toutes les IPs
* d'un attribut "security_group_id" correspondant à l’id du security group créé précédemment

Une règle de security group, s'appelant my_security_group_rule_out_https, composée:
* d'un attribut "type" correspondant au flux sortant
* d'un attribut "from_port" valant : 
* d'un attribut "to_port" valant : 
* d'un attribut "protocol" valant : 
* d'un attribut "cidr_blocks" acceptant toutes les IPs
* d'un attribut "security_group_id" correspondant à l’id du security group créé précédemment

Une règle de security group, s'appelant my_security_group_rule_http_in, composée:
* d'un attribut "type" correspondant au flux entrant
* d'un attribut "from_port" valant : 
* d'un attribut "to_port" valant : 
* d'un attribut "protocol" valant : 
* d'un attribut "cidr_blocks" acceptant toutes les IPs
* d'un attribut "security_group_id" correspondant à l’id du security group créé précédemment

Une instance, s'appelant my_instance, composée:
* d'un attribut "ami" avec la valeur: 
* d'un attribut "subnet_id" correspondant à l’id du subnet créé précédemment
* d'un attribut "instance_type" valant: "t2.micro"
* d'un attribut "vpc_security_group_ids" correspondant à l’id du security group créé précédemment
* d’un tag "Name" valant :
* d’un tag "Formation" valant :
* d’un tag "User" valant :

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

Les ressources sont maintenant créées.

## 3- Un petit coup de ménage

Pour détruire votre topology :
```bash
$ terraform destroy
```
