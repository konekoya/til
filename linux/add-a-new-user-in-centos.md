# Add a New User in CentOS

When working with Linux machines. It's generally recommended that you create a non-root user to perform regular tasks to avoid potential dangerous commands that required root privileges.

To create a new user in CentOS, follow the steps:

Switch to the root user to gain the necessary privileges to create a new user. You can do the running:

```sh
su root
```

Create a new user with the `adduser` command. Replace `joshua` with the desired username:

```sh
adduser joshua
```

This will add the user to the end of the `/etc/passwd` file.

Verify that the new user has been created by running the following command:

```sh
cat /etc/passwd
```

This will display a list of all users on the system. The new user should be included in the list. See the example output below:

```sh
# ... more users in the above
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
ntp:x:38:38::/etc/ntp:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
ohara:x:1000:1000:ohara:/home/ohara:/bin/bash
joshua:x:1001:1001::/home/joshua:/bin/bash # The one we just added
```

Once the user is added, you will also need to assign a password for it by running the following command. Replace `joshua` with the username you created:

```sh
passwd joshua
```

And you will often want to add this user to the `sudoers` file to allow it to perform administrative tasks. To do this, run the following command to open the `sudoers` file:

```sh
visudo
```

Scroll to the end of the file and add the following line, replacing `joshua` with the name of your new user:

```sh
joshua ALL=(ALL) ALL
```

Save and exit the `sudoers` file.

You new user should now be able to perform administrative tasks using the `sudo` command.
