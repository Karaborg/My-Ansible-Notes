# Overview And Introduction

# Setup of the Lab Environment
Before we start, make sure you have **Docker** and **Docker Compose** installed on your computer. Then, start the environment by simply entering `docker compose up -d`. This will install the ubuntu and centos images and start them.

Once it's done. Check http://localhost:1000/. If your configurations are right, you should be able to see **Ansible Terminal** on tabs. Click on that, and connect to **Ubuntu-c**.

> The user and password for containers is **ansible**/**password**.

Since we have 3 ubuntu and 3 centos os containers, we want to ssh them without entering password all the time. So:

1. Enter `ssh-keygen` to generate public and private key for ubuntu-c.
   a. You can use default configurations.
2. Then we will copy our public key to other containers with `ssh-copy-id ansible@ubuntu1`.
   a. **ansible** is your username and **ubuntu1** is your container name.
3. Once it's done, you can connect to `ubuntu1` container without password.
4. But, since we want to ssh with both **ansible** and **root** user, we can do all that with the script below:

```
echo password > password.txt

for user in ansible root
do
  for os in ubuntu centos
  do
    for instance in 1 2 3 
    do
      sshpass -f password.txt ssh-copy-id -o StrictHostKeyChecking=no ${user}@${os}${instance}
    done
  done
done

rm password.txt
```

Now we can connect to all containers without a password.

# Ansible Architecture And Design

### Ansible Configuration
So, if we connect to our Ansible container which is **ubuntu-c**, and enter `ansible --version`, we can see there is no **config file** exist yet. To set this configuration file, there are 4 ways:

1. **ANSIBLE_CONFIG** as environmental variable, with a filename target.
   a. Create ansible.cfg file and use `export ANSIBLE_CONFIG=<PATH_TO_DIRECTORY>/ansible.cfg`
2. ./ansible.cfg in the current directory.
   a. Create a directory, create a ansible.cfg file under that directory.
   b. If you check the **config file** under that directory, ansible will use the closest ansible file.
3. ¬/.ansible.cfg file a hidden in the users home directory.
4. /etc/ansible/ansible.cfg which is typically provided.
   a. If you are using this type of configuration, it will be overwritten everytime when you use the other 3 ways.

> The list above listed as most **priority** to less.

# Ansible Playbooks, Introduction

# Ansible Playbooks, Deep Dive

# Structuring Ansible Playbooks

# Cloud Services And Containers

# Modules And Plugins

# Other Resources And Ares