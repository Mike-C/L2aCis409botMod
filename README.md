# L2aCis409botMod
Lineage 2 aCis 409 modified java server with Fake Players, Traders &amp; bots.

<img width="1440" height="834" alt="Example" src="https://github.com/user-attachments/assets/f4a6ed87-f9ca-4106-8111-7aec4110c5e7" />

**Usage example:**

Patch the aCis 409 repository with given patch.diff.
First clone the aCis 409 repository and than copy the patch.diff 
file into the root of your repository and apply patch.diff:

**Guide on Linux:**

```
cd ~
mkdir git
cd git
git clone https://gitlab.com/Tryskell/acis_public/
cd acis_public
git apply patch.diff
```

* Than build the source as normally. i.e. through Eclipse Ant build.xml (import the project first).
Both projects aCis_datapack and aCis_gameserver have to be build.
Copy the build files into ~/L2aCisMod/ directory.
```
cd ~
mkdir L2aCisMod
cp -r ~/git/acis_public/aCis_gameserver/build/dist/ ~/L2aCisMod
cp -r ~/git/acis_public/aCis_datapack/build/ ~/L2aCisMod
```
* Than copy L2OFF Interlude geodata ([can be found on the internet](http://anothercrappyinterludeserver.com/files/geodata/)),
into ~/L2aCisMod/gameserver/data/geodata directory.
If you want to use L2J geodata, configure it in
~/L2aCisMod/gameserver/config/geoengine.properties Set: GeoDataType = L2J

* You need MariaDB to run the server, on Ubuntu Linux:
```
sudo apt install mariadb-server mariadb-client galera-4
sudo mariadb-secure-installation
```
Or on CachyOS:
```
sudo pacman -Syu mariadb
sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
sudo systemctl start mariadb.service
sudo systemctl enable mariadb.service
```
Than create l2aCismoddb database on MariaDB server:
```
sudo mariadb
```
Than run the following sql script, don't forget to change database user 'password':
```
CREATE DATABASE l2aCismoddb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'l2database'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON l2aCismoddb.* TO 'l2database'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
After that apply all sql scripts:
```
cd ~/L2aCisMod/sql
cat *.sql > all.sql
sudo mariadb -u l2database -p l2aCismoddb < all.sql
```
Than modify ~/L2aCisMod/gameserver/config/server.properties
In the section "Database informations", put this (don't forget to change the pasword you set for l2database user):
```
URL = jdbc:mariadb://localhost:3306/l2aCismoddb
Login = l2database
Password = password
```
Than modify ~/L2aCisMod/login/config/loginserver.properties
In the section "Database informations", put the same.
After this update all scripts rights in ~/L2aCisMod/login/ 
and after that also in ~/L2aCisMod/gameserver/ server directories.
```
cd ~/L2aCisMod/login/
chmod +x *.sh
cd ~/L2aCisMod/gameserver/
chmod +x *.sh
```
* Than run ./RegisterGameServer.sh in ~/L2aCisMod/login/
choose server number and press enter, hexid(server x).txt will be generated
in ~/L2aCisMod/login/ directory.
Move this file into ~/L2aCisMod/gameserver/config directory as hexid.txt
* Than run ./startLoginServer.sh in ~/L2aCisMod/login/ directory.
* And ./startGameServer.sh in ~/L2aCisMod/gameserver/ directory
You can see the login/ and gameserver/logs server directories, if there are any errors.
* Connect with Interlude client, which connects to localhost, 127.0.0.1

**Release notes**

**L2aCis409botMod v0.03**
* Random fake player shops have been added to all villages and cities. (just Buy & Sell).
  Random shops have been tuned to be more realistic.
  They sell only No, D & C grade at the moment.
* Fixed disconnect bug with Fermata client.
* You need to recompile whole project, so the changes take effect.
  Including recreating database if so, "sudo mariadb" and than
  "drop database l2aCismoddb;" And re-create it again with the new patch.diff applied.
  If you don't want to recreate database, you can just drop tables fake_traders
  and fake_traders_items and apply again new scrips fake_traders.sql & fake_traders_items.sql

**L2aCis409botMod v0.02**
* Random fake player shops have been added to Elven village. (just Buy & Sell).
  Fake players have random names, from gameserver/data/fake_names.txt
  They sell only D-grade equipment at the moment.
* You need to recompile whole project if so, so the changes take effect.
  Including database, "sudo mariadb" and than "drop database l2aCismoddb;"
  And re-create it again with the new patch.diff applied.

**L2aCis409botMod v0.01**
* You can spawn bots using admin command: //spawnbot
  Your character needs to have accessLevel 7, that is admin in the
  'characters' Mariadb table.
  Bots have random lvl 1..19, and are chosen randomly from the template
  Elven Fighter or Elven Mystic.
  Bots use basic skills Power Strike, Wind Strike & Ice Bolt.
  Levels of those skills is approximated to bot level, not perfect yet.
* In Elven Village near Newbie Helpers sits fake traders.
  Fake traders can Sell, Buy & Manufacture and can have a Clan.
* Bots and their shops can be added through, 'fake_traders' and
  'fake_trader_items' MariaDB tables.
* Manor is working from the start of the server. For convenient purposes
  its been added to Oren only. That means you can use it in Oren territory
  and in the Elven & Dark Elven Villages.
* Some Castles are taken from the start of the server by bot Clans.
* Tax rate for those territories are set randomly, except for Giran's 15% tax.
* Total adena dropped is tracked in 'server_memo' database table,
  which gets updated into database every 2 minutes.
* Community server is running by default.
* GNU General Public License v2.0
