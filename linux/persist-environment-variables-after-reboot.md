# Persist Environment Variables after Reboot

If you want to persist environment variables after reboot, there's a simple command you can use.

I've just come across a way to persist env variables after reboot with a simple command.

Following these steps assuming you have a `.env` file with the following content located in your home directory:

```sh
MY_NAME=John
MY_PASSWORD=123456
```

1. Log into the machine and open the `.bash_profile` file.
2. Add the following line in the end of the file, replacing `joshua` with your own username:

```sh
set -o allexport; source /home/joshua/.env; set +o allexport
```

3. Save and exit the file.
4. Log out and log in again.
5. To verify that the environment variables have been persisted, run the following command in the console:

```sh
printenv
```

This should print out the environment variables that you set in the `.env` file.
