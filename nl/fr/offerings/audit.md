---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2018-00-00 -->

# Consignation dans le journal d'audit


La consignation dans le journal d'audit enregistre les principaux {{site.data.keyword.cloudantfull}} ayant accédé à des données stockées dans {{site.data.keyword.cloudant_short_notm}}. Pour tous ls accès d'API HTTP à {{site.data.keyword.cloudant_short_notm}}, la fonction de consignation dans le journal d'audit enregistre les informations suivantes relatives à chaque demande HTTP :


Informations | Description
------------|------------
`Principal` | Identifiants de compte, clé d'API ou données d'identification IBM Cloud IAM. 
`Action` | Action effectuée (par exemple, lecture de document). 
`Ressource` | Détails sur le compte, la base de données, le document ayant fait l'objet d'un accès ou la requête créée.
`Horodatage` | Enregistrement de l'heure et des données de l'événement. 

Les journaux d'audit {{site.data.keyword.cloudant_short_notm}} peuvent permettre de comprendre :

- Quelles bases de données et quels documents ont fait l'objet d'un accès dans un compte, à quel moment et par qui.

- Quelles requêtes ont été exécutées, à quel moment et par qui.
- Quel principal ou utilisateur spécifique a fait l'objet d'un accès ou a été mis à jour ou supprimé et à quel moment.
- Quels documents de réplication ont été créés ou supprimés et à quel moment.
{:shortdesc}

## Comment accéder aux journaux d'audit pour votre compte

Afin de demander l'accès aux journaux d'audit pour votre compte, contactez le support {{site.data.keyword.cloudant_short_notm}}. Le support fournit un accès aux journaux d'audit intéressants.


Lorsque vous contactez le support, veillez à inclure :

- Le compte concerné par la demande {{site.data.keyword.cloudant_short_notm}}. 
- Le délai des journaux d'audit (ne doit pas dépasser un mois par demande de support).
- Les bases de données, documents ou principaux présentant un intérêt.
