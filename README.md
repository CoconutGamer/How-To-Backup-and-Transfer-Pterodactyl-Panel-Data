# How-To-Backup-and-Transfer-Pterodactyl-Panel-Data

1. Backup your hidden `.env` file containing the decryption APP_KEY from `/var/www/pterodactyl`
<br>

2. Export the database, in this case ours is named **panel**

    ```mysql
    mysqldump -u root -p --opt panel > /var/www/pterodactyl/panel.sql
    ```

    The *.sql* file would be saved in the `/var/www/pterodactyl/` folder.
<br>

3. Follow the panel [installation documentation](https://www.youtube.com/watch?v=Rcsd7AmFnAc&list=PLpYUyXTDvQJJlfergkeyW7er2n04x9Xfc) to install the panel on your new server.
<br>

4. Transfer the `panel.sql` file to your new server and import the database. Make sure you're in the folder containing your *.sql* dump when performing the commands.

    ```mysql
    mysql -u root -p panel < panel.sql
    ```

    <br>

5. After this, transfer your old `.env` file to the `/var/www/pterodactyl` location to complete the panel migration.

## Migrating Wings

1. Follow the Wings [installation documentation](https://www.youtube.com/watch?v=Rcsd7AmFnAc&list=PLpYUyXTDvQJJlfergkeyW7er2n04x9Xfc) to install Wings on your new machine.

<br>

2. Once new Wings are configured, migrate all your volumes from your old machine to the new one. By default, the path would be `/var/lib/pterodactyl/volumes/`. Check your Wings `config.yml` for your configured data path.
