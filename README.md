# Dell Server management playbook
A quick playbook for mounting the agent-based iso to iDRAC and powering on the nodes

## Directory Structure

The project directory is organized as follows:

```
.
├── LICENSE
├── README.md
├── inventory
│   ├── all.yml
│   ├── control_plane.yml
│   ├── group_vars
│   │   ├── control_plane.yml
│   │   └── worker.yml
│   └── worker.yml
├── playbook.yml
└── roles
    └── manage_dell_servers
        ├── tasks
        │   └── main.yml
        └── vars
            └── main.yml
```

## Role

The playbook uses a single role named `manage_dell_servers` located in `roles/manage_dell_servers/`. This role includes tasks to:

1. **Unmount any currently mounted virtual disk**: Ejects existing virtual media.
2. **Mount ISO as virtual media**: Inserts the specified ISO URL as virtual media.
3. **Set one-time boot to virtual media**: Configures the server to boot from the virtual media for the next reboot.
4. **Power on the servers**: Powers on the server.

## Variables

- **`idrac_ip`**: IP address of the iDRAC interface.
- **`idrac_username`**: Username for iDRAC authentication.
- **`idrac_password`**: Password for iDRAC authentication.
- **`iso_url`**: URL of the ISO to be mounted.

## Usage

1. **Update Inventory Files**: Edit `inventory/control_plane.yml`, `inventory/worker.yml`, and `inventory/group_vars/*.yml` to include your server details and shared variables.

2. **Run the Playbook**: Use the `ansible-playbook` command to execute the playbook. You can limit the execution to specific groups or hosts using the `--limit` option.

   To run the playbook for the `control_plane` group:
   ```bash
   ansible-playbook -i inventory/all.yml playbook.yml --limit control_plane

   To run the playbook for the `eject` tag:
   ```bash
   ansible-playbook -i inventory/all.yml playbook.yml 
   -t eject