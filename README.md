# redmine-server

`ansible/redmine_centos7.yml` is an [Ansible](https://www.ansible.com/)
playbook that automates a deployment of [Redmine](http://www.redmine.org/)
on Centos 7 using Postgresql, Passenger + Nginx, and Let's Encrypt.

## Usage
1. Create the file `ansible/deployment_vars.yaml` and define the following
   variables:
   - `ruby_version` - the version of Ruby to install
   - `letsencrypt_email` - the email used to register for Let's Encrypt
   - `redmine_hostname` - the hostname used to register for Let's Encrypt
   - `redmine_system_user` - the name of the system user who will own Redmine
   - `redmine_database_name` - the name of the postgres redmine database
   - `redmine_database_username` - the name of the postgres redmine user
   - `redmine_database_password` - the postgres redmine user password

2. Create an `ansible/hosts.ini` (or whatver you want to call it; I already
   included `hosts.ini` in `.gitignore`) that holds all hosts to provision.

3. Add any custom Redmine themes to `ansible/roles/redmine-extras/files/themes`
   and any custom plugins to `ansible/roles/redmine-extras/files/plugins`.

4. Run the Ansible playbook using `ansible-playbook -i ansible/hosts.ini
   ansible/redmine_centos7.yml`.

   ***DO NOT CHECK `deployment_vars.yaml` or `hosts.ini` INTO VERSION
   CONTROL***

   (I already have them in `.gitignore`, but be careful.)

   Note: It is understandably concerning that this deployment uses a plaintext
   password and that Redmine itself stores the password in plaintext. However,
   it is a purely local database with no remote connectivity, and so the only
   vulnerability to the database would be someone with access to the host
   itself.