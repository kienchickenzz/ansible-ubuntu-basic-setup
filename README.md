### System-level task
sudo ansible-playbook src/playbook.yml \
  --limit local \
  --tags nerd_font --list-task

sudo ansible-playbook src/playbook.yml \
  --limit local \
  --tags package --list-task


### User-level task
ansible-playbook src/playbook.yml \
  --tags dotfile \
  -e @src/vars/local_user.yml --list-task

ansible-playbook src/playbook.yml \
  --tags ohmyzsh \
  -e @src/vars/local_user.yml --list-task
  



📁 Layout đề xuất

ansible/
├── ansible.cfg
├── inventory.ini
├── README.md
└── src
    ├── playbook.yml
    ├── inventory/
    │   └── host_vars/
    │       └── local.yml
    ├── group_vars/
    │   └── all.yml
    └── roles/
        ├── system/          # 🔒 root-only
        │   ├── tasks/
        │   │   ├── main.yml
        │   │   ├── packages.yml
        │   │   ├── fonts.yml
        │   │   └── locale.yml
        ├── users/           # 👤 user-level
        │   ├── tasks/
        │   │   ├── main.yml
        │   │   ├── dotfiles.yml
        │   │   ├── shell.yml
        │   │   └── editor.yml
        │   └── defaults/
        │       └── main.yml
        └── shared/          # 🔁 logic chung (NO side-effect)
            └── tasks/
                └── main.yml
