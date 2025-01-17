Voici un **README.md** pour documenter la configuration et l'utilisation de ton projet Ansible :

```markdown
# Ansible Configuration Setup

Ce projet Ansible configure automatiquement des services sur un système local. 
Il gère l'installation et la configuration de plusieurs outils, y compris **Auditd**, **NFtables**, et **Thunderbird**,...
Ainsi que des notifications par email pour des événements critiques.

## Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants :

- **Ansible** installé sur votre machine de gestion.
- Un serveur Ubuntu ou Debian sur lequel appliquer cette configuration.
- Un serveur de messagerie (comme Zoho ou un autre service SMTP) pour l'envoi des notifications par email.

## Structure du projet

```
ansible_playbooks/
├── inventory              # Inventaire des hôtes Ansible
├── main.yml               # Playbook principal
└── roles/
    ├── auditd             # Rôle pour configurer Auditd
    │   ├── handlers/      # Gestionnaires pour Auditd
    │   ├── tasks/         # Tâches pour Auditd
    │   └── templates/     # Modèles pour les règles d'Auditd
    ├── cron_tasks         # Rôle pour configurer les tâches cron
    │   └── tasks/         # Tâches cron
    └── nftables           # Rôle pour configurer NFtables
        ├── handlers/      # Gestionnaires pour NFtables
        ├── tasks/         # Tâches pour NFtables
        └── templates/     # Modèles pour la configuration de NFtables
```

## Fonctionnalités

### 1. **Auditd Configuration**
- Installe **Auditd** et configure les règles de sécurité pour surveiller l'activité du système.
- Envoie des notifications par email lorsqu'une activité anormale est détectée par **Auditd**.

### 2. **NFtables Configuration**
- Installe et configure **NFtables** pour le pare-feu.
- Envoie des notifications par email lorsqu'une connexion est bloquée ou si **NFtables** est arrêté.

### 3. **Thunderbird Configuration**
- Installe **Thunderbird**.
- Configure automatiquement un compte Zoho (kikimail@zoho.com) pour envoyer et recevoir des emails.
- Configure **Thunderbird** pour se lancer automatiquement au démarrage du système.

### 4. **Notification par Email**
- Si un service (comme **NFtables** ou **Auditd**) est arrêté, un email est envoyé à l'adresse spécifiée dans le playbook.
- Notifications régulières sont envoyées pour les événements importants.

## Installation

### 1. **Clonez le repository**
```bash
git clone https://your-repo-url.git
cd ansible_playbooks
```

### 2. **Configurez l'inventaire**
Assurez-vous que le fichier `inventory` contient la liste de vos hôtes cibles.

### 3. **Personnalisez les configurations**
- Modifiez les adresses email dans le playbook (`main.yml`) pour définir où envoyer les alertes.
- Si vous utilisez un autre service SMTP (ex. Zoho), ajustez les configurations dans les rôles respectifs 
(Auditd, NFtables, etc.).

### 4. **Exécutez le playbook**
Lancez le playbook principal pour appliquer la configuration sur votre système :
```bash
ansible-playbook -i inventory main.yml --ask-become-pass
```
Cela installera les outils, les configureras, et mettra en place les alertes par email.

### 5. **Testez la configuration**
- Vérifiez l'installation des services (Auditd, NFtables, Thunderbird) :
  ```bash
  systemctl status auditd
  systemctl status nftables
  systemctl status thunderbird
  ```
- Vérifiez que les notifications par email sont envoyées correctement en testant les services 
(arrêtez un service comme **NFtables** ou **Auditd** et vérifiez votre boîte email).

## Commandes Utiles

- **Vérification de la syntaxe du playbook** :
  ```bash
  ansible-playbook --syntax-check main.yml
  ```

- **Vérification des cron jobs** :
  ```bash
  crontab -l
  ```

- **Test manuel de l'envoi d'email** :
  ```bash
  echo "Test email" | mail -s "Test Subject" admin@example.com
  ```

- **Redémarrer le service cron pour appliquer les changements** :
  ```bash
  systemctl restart cron
  ```

- **Consulter les logs des mails envoyés** :
  ```bash
  tail -f /var/log/mail.log
  ```

## Conclusion

Ce playbook Ansible simplifie la gestion des services critiques et vous permet de recevoir des alertes importantes par email. 
Il vous permet également de configurer **Auditd**, **NFtables**, et **Thunderbird** rapidement et efficacement. 

...



