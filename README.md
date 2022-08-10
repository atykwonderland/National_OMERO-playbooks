# Playbooks
Ansible playbooks to create/update OMERO servers on Compute Canada Cloud using openstack

----------

Before running any playbooks, install all requirements/roles:

    ansible-galaxy install -r requirements.yml

They can be found in your home directory at `~/.ansible/roles`

And make backup copies of current configs located at:

    /opt/omero/web/OMERO.web/var/templates/custom_login.html
    /opt/omero/web/config
    /opt/omero/server/config

General Play Command: 
    
    #check first
    ansible-playbook --check --diff -i [INVENTORY(hosts)] [PATH_TO_PLAYBOOK]
    #check to see if any changes were made to the configs that were not intended
    #note any install checks won't pass
    #if there are, then you need to note them and restore them from the copies you made earlier after running the playbook
    #play
    ansible-playbook -i [INVENTORY(hosts)] [PATH_TO_PLAYBOOK]


----------

| File | Usage |
|---|---|
| checkCerts.yml | included in productionServer.yml and trainingServer.yml |
| clouds.yaml | things/credentials you need to access Arbutus |
| configPrometheus.yml |  |
| configureGrafana.yml |  |
| createlnstance.yml | creating instance and attach volume in openstack |
| createUsers.yml | populating training server |
| environment.yml |  |
| inventory | where all the hosts/groups are listed |
| monitoringAgents.yml |  |
| productionServer.yml | production level server config setup |
| publicWebClient.yml |  |
| publicWebClientMinimal.yml | minimal install of the public repo web client |
| rdiffBackup.yml | tasks for the backup |
| requirements.yml | roles requirements for ansible-playbook |
| site.yml | create/configure omero server on instances (only use relevant sections) <br> - calls trainingServer.yml/productionServer.yml/rdiffBackup.yml etc. after creating the server |
| test.yml | test |
| test2.yml | test |
| testola.yml | test |
| testola2.yml | test |
| trainingServer.yml | training level server config setup (calls createUsers.yml) |
| UpdateAllPackages.yml | update apt, upgrade, and reboot if needed |
| updateAllServers.yml | runs UpdateAllPackages.yml for all servers |


>**Note** : `createInstance.yml` depends on the `python-openstackclient` and `openstacksdk` packages installed in the same environment as `ansible`.

>**Note** : roles may need to be updated on `ansible-galaxy` or `OME` github

>**Note** : directory structure has changed, so any older playbooks will need to edit playbook import paths