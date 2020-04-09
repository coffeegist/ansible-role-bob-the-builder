# ansible-role-bob-the-builder

This is role designed to run pre-configured blueprints from [Bob the Builder](https://github.com/coffeegist/bob-the-builder) across your inventory.

## Role Variables

To use this role, you must define the variables listed below. The easiest way to do this is to copy the `vars/main.yml.sample` file to `vars/main.yml` and add your Azure DevOps organization and personal access token.

### Variable Explanations

- azure_devops_pat -  A personal access token for your Azure DevOps account
- azure_organization - Your Azure DevOps organization's name
- bob_dir - The path to install Bob the Builder
- blueprints_dir - A local directory containing the Bob the Builder blueprints to run
- out_dir - A remote directory to store the final tools in

## Blueprints

This playbook uses Bob to run all of the blueprints found in the `files/blueprints` directory. Use Bob to generate blueprints, or get them from your teammates, and store them there before running the role.

## Adding to a Playbook

Here's how to use it in a playbook:

```yaml
- hosts: all
  become: yes
  become_method: sudo
  roles:
    - ansible-role-bob-the-builder
```

## Running Without a Playbook

If it's not part of a playbook, and you want to run this standalone, do the following:

```bash
# To run locally
$ cd ansible-role-bob-the-builder
$ ansible localhost -m include_role -a name=.

# To run remotely
$ ansible -i inventory.yml -m include_role -a name=. --private-key <PATH_TO_SSH_KEY> -u <REMOTE_USERNAME> all
```
