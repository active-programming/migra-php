MigraPHP
========

Very primitive script for Mysql migrations.

Don't ask about new features or improves, just do a pull request.

Install
-------

Run in root folder of project:

```
$ php -r "file_put_contents('migra', file_get_contents('https://raw.githubusercontent.com/active-programming/migra-php/master/migra'));"
```

Commands
--------

```
./migra config [database] [dbuser] [dbpassword] [dbhost] [dbport] - configure PDO connection
./migra status {number}
./migra create {migration_name} - create migration
./migra apply|up {number} - apply last {number} of migrations
./migra revert|down {number} - revert last {number} of migrations
./migra delete {number} - revert and delete last {number} of migrations
```

So, fast configure will looks like:

```
$ ./migra config
Enter database name: migra
Enter db user name: root
Enter db password: password
Enter db host [localhost]: 
Enter db port [3306]: 
 Result configuration:
   name: 'migra'
   user: 'root'
   password: 'password'
   host: 'localhost'
   port: '3306'
 Test connection ... Success!
Configure completed
```

Migration
---------

```
$ ./migra create my_first_migration
    Migration '1481366582_my_first_migration' created (.../migrations/1481366582_my_first_migration.php)
```

Will looks like:

```
<?php
/**
 * Migration 1481366582_my_first_migration
 * @author YourName
 */ 

class migration_1481366582_my_first_migration extends MigrationObject
{

    function apply()
    {
        // todo your code
        
        // examples:
        // $this->createTable('test', ['`id` int(11) NOT NULL PRIMARY KEY AUTO_INCREMENT', '`str` varchar(120) NOT NULL', '`num` float NOT NULL']);
        // $this->addColumn('test', 'column',  'float NOT NULL');
        // $row = $this->query("SELECT * FROM `test` WHERE `id` > :id", [':id' => 2], self::ROW);

        return true; // if the method doesn't return true, then migration is failed
    }

    function revert()
    {
        // todo your code
        // example
        // $this->dropTable('test');

        return true;
    }

}
```

Apply migration:

```
$ ./migra up
```

etc.