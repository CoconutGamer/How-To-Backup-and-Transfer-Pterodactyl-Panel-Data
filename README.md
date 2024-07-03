# How-To-Backup-and-Transfer-Pterodactyl-Panel-Data
1. Backup your hidden `.env` file containing the decryption APP_KEY from `/var/www/pterodactyl`
2. Export the database, in this case ours is named **panel**
    ```mysql
    mysqldump -u root -p --opt panel > /var/www/pterodactyl/panel.sql
    ```
    The *.sql* file would be saved in the `/var/www/pterodactyl/` folder.

3. Follow the panel [installation Video's](https://www.youtube.com/watch?v=SbclGE3ovd8) to install the panel on your new server.
<br>
    - Here is the documentation of Pterodactyl [Docs](https://pterodactyl.io).

4. Transfer the `panel.sql` file to your new server and import the database. Make sure you're in the folder containing your *.sql* dump when performing the commands.

    ```mysql
    mysql -u root -p panel < panel.sql
    ```

    <br>

5. After this, transfer your old `.env` file to the `/var/www/pterodactyl` location to complete the panel migration.

## Migrating Wings

1. Follow the Wings [installation Video's](https://www.youtube.com/watch?v=SbclGE3ovd8) to install Wings on your new machine.

<br>

2. Once new Wings are configured, migrate all your volumes from your old machine to the new one. By default, the path would be `/var/lib/pterodactyl/volumes/`. Check your Wings `config.yml` for your configured data path.

## Updating allocations

After the migration of volumes is done, you must update all the allocations since your IP most likely has changed.
<br>

Type ```hostname -I | awk '{print $1}'``` on your Wings machine to retrieve the IP. After that, login to your Panel machine to modify the database.

In the example below, we assume that the database name is `panel`. Replace `newiphere`with the IP returned from the hostname command above while `oldiphere` with the IP of your old allocation.

```mysql
mysql -u root -p
UPDATE panel.allocations SET ip = 'newiphere' WHERE ip = 'oldiphere';
exit
```
