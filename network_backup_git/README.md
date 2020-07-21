Role Name
=========

This role does network device backups, then saves the results to a git repository.
It currently only supports Cisco, Arista, and Juniper.

Requirements
------------

A git repository, private, not public like I use for testing here should be established.
An SSH key should be used to prevent the script from prompting for credentails.
  This key should be fairly easy to setup.  Also your repo clone should be in the form
  git@xxx.com:account/repo so that it will use SSH to pull and push.

Role Variables
--------------

Check the default folder for configurable variables:
---
# defaults file for network_backup_git
# the local git repo where configs are stored for push/pull
backup_dir: "{{ playbook_dir }}/net_backups"

# what format to save the file as in the git repo
backup_file: "{{ backup_dir }}/{{ inventory_hostname }}"

# location of the repo
backup_repo: git@github.com:gregsowell/net_backups

# git update details
git_name: Greg Sowell
git_email: networkbackups@gregsowell.com


Dependencies
------------
NA

Example Playbook
----------------

---
- name: network device backup to git
  hosts: crtr3
  gather_facts: false
  vars:
    backup_dir: "{{ playbook_dir }}/net_backups"
    backup_file: "{{ backup_dir }}/{{ inventory_hostname }}"
    backup_repo: git@github.com:gregsowell/backups
    git_name: Greg Sowell
    git_email: greg@gregsowell.com
  
  tasks:

  - import_role:
      name: network_backup_git

License
-------

BSD

Author Information
------------------

Greg Sowell - GregSowell.com or TheBrothersWISP.com
