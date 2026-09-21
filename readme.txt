Lineage 2 aCis 409 modified java server with Fake Players, Traders & bots; (c) 2026 rdavidian71@gmail.com v0.03

You are using this software at your own risk. Author does not bear any responsibility for potential damage concerning it's use.

Version notes:

L2aCis409botMod v0.03
* Random fake player shops have been added to all villages and cities. (just Buy & Sell).
  Random shops have been tuned to be more realistic.
  They sell only No, D & C grade at the moment.
* Fixed disconnect bug with Fermata client.
* You need to recompile whole project, so the changes take effect.
  Including recreating database if so, "sudo mariadb" and than
  "drop database l2aCismoddb;" And re-create it again with the new patch.diff applied.
  If you don't want to recreate database, you can just drop tables fake_traders_items
  and fake_traders and apply again new scrips fake_traders.sql & fake_traders_items.sql

L2aCis409botMod v0.02
* Random fake player shops have been added to Elven village. (just Buy & Sell).
  Fake players have random names, from gameserver/data/fake_names.txt
  They sell only D-grade equipment at the moment.
* You need to recompile whole project if so, so the changes take effect.
  Including database, "sudo mariadb" and than "drop database l2aCismoddb;"
  And re-create it again with the new patch.diff applied.

L2aCis409botMod v0.01
* Initial release
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
