Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).


*Contexte :*
Vous disposez de trois serveurs avec des environnements différents. Deux serveurs fonctionnent sous *Ubuntu, et un serveur utilise une distribution Linux avec **YUM* (par exemple *CentOS). Vous devez mettre en place un processus de déploiement automatisé pour une application API Java sur trois environnements distincts : **Intégration, **Qualification, et **Production*.

*Objectifs :*
L'objectif est de créer un *rôle Ansible* permettant d'installer *Java, récupérer le code source depuis un dépôt **Git, compiler l'application avec **Maven*, et déployer le livrable sur les trois environnements. Chaque serveur devra installer Java selon son gestionnaire de paquets, cloner le dépôt Git contenant le code source de l'API, compiler l'application via Maven, puis déployer l'API en tant que service sur les serveurs.

### Détails de l'exercice :

1. *Environnements :*
    - *Intégration* : Une machine Ubuntu.
    - *Qualification* : Une autre machine Ubuntu.
    - *Production* : Une machine avec une distribution qui utilise *YUM* (par exemple CentOS).

2. *Installation de Java et Maven :*
    - Sur les machines *Ubuntu, vous devez installer **Java 11* et *Maven* avec *APT*.
    - Sur la machine utilisant *YUM* (par exemple *CentOS), vous devez installer **Java 11* et *Maven* avec *YUM*.

3. *Récupération du code :*
    - Vous devez cloner le dépôt Git contenant l’API Java (par exemple, un dépôt sur GitHub). Le dépôt doit être cloné dans le répertoire /opt/api.

4. *Compilation du code avec Maven :*
    - Une fois le code récupéré, vous devez compiler l'application avec *Maven* en exécutant la commande mvn clean install.
    - Le livrable (un fichier *JAR* ou *WAR*) doit être généré dans un répertoire spécifique (/opt/api/target).

5. *Déploiement :*
    - Après le build, vous devez copier le fichier JAR ou WAR compilé vers un emplacement définitif sur le serveur (par exemple /opt/api/api.jar).
    - Vous devez ensuite créer un service *systemd* pour démarrer l’API en tant que service.
    - Ce service doit démarrer automatiquement au démarrage du serveur et être lancé immédiatement après le déploiement.

6. *Création du rôle Ansible :*
    - Créez un rôle Ansible appelé deploy_app qui :
        - Installe *Java* et *Maven* en fonction du gestionnaire de paquets disponible (APT ou YUM).
        - Clone le dépôt *Git* contenant le code de l'API.
        - Compile l'API avec *Maven*.
        - Déploie le fichier JAR ou WAR et configure l'API pour être gérée par *systemd*.

7. *Exécution :*
    - Créez un fichier d’inventaire Ansible pour définir les trois environnements (Intégration, Qualification, Production).
    - Créez un playbook Ansible qui appelle le rôle deploy_app pour chacun des trois environnements.

### Critères de réussite :

- *Java* et *Maven* sont installés correctement sur chaque machine selon le gestionnaire de paquets respectif.
- Le code source de l'API est cloné correctement depuis le dépôt *Git* sur chaque machine.
- L’application est compilée sans erreur avec *Maven* sur chaque environnement.
- Le livrable (fichier JAR ou WAR) est déployé sur chaque machine, et l'API est configurée pour démarrer automatiquement via un service *systemd*.
- Le service *systemd* est actif et démarre l'application API sur chaque serveur après le déploiement.

### Bonus :
- Si possible, ajoutez un test dans votre rôle Ansible pour vérifier que l'API est bien déployée et répond sur un port spécifique (par exemple, en utilisant un module *uri* d'Ansible pour tester une requête HTTP sur l'API déployée).

---

*Exemple de commande pour exécuter le playbook :*
bash
ansible-playbook -i inventory/hosts.ini playbooks/deploy.yml


*Dépôt Git à utiliser :* Vous pouvez créer un dépôt Git simulé pour l'exercice ou utiliser n'importe quel dépôt existant contenant une application Java compatible.
