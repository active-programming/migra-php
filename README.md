MigraPHP
========

Very primitive script for Mysql migrations.

Don't ask about new features or improves, just do a pull request.

Install
-------

Run in root folder of project:

```
$ composer require adamasantares/migra-php
$ ./vendor/adamasantares/migra-php/migra link #run once on install
 OR
$ wget https://raw.githubusercontent.com/active-programming/migra-php/master/migra; chmod +x ./migra; 
 OR
$ php -r "file_put_contents('migra', file_get_contents('https://raw.githubusercontent.com/active-programming/migra-php/master/migra'));"; chmod +x ./migra;
```

Then try

```
$ ./migra help
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

New migration will look like:

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
        // todo your code here
        // examples:
        // $this->createTable('test', ["`id` int(11) NOT NULL PRIMARY KEY AUTO_INCREMENT", "`str` varchar(120) NOT NULL", "`num` float NOT NULL"]);
        // $this->addColumn('test', 'column',  'float NOT NULL');
        // $this->renameColumn('test', 'column', 'created_at');
        // $this->retypeColumn('test', 'created_at', 'int(11)', false, '1481383022');
        // if the method doesn't return true, then migration is failed
        return true;
    }

    function revert()
    {
        // todo your code here
        // example
        // $this->dropTable('test');
        // $this->dropColumn('table_name', 'column_name');
        return true;
    }

}
```

### Apply migration:

```
$ ./migra apply
or
$ ./migra up
or
$ ./migra up 5 - apply 5 migrations
```

### Revert migration

```
$ ./migra revert
or
$ ./migra down
or
$ ./migra down 3 - revert last 3 migrations
```

### Statuses

```
$ ./migra status

   Migrations statuses

   | DateTime            | Name                          | Author     | Status    |
   |---------------------+-------------------------------+------------+-----------|
   | 13/12/2016 02:43:11 | 1481596991_createTestTable    | Konstantin | APPLIED   |
   | 13/12/2016 02:43:26 | 1481597006_addColumnToTest    | Konstantin | APPLIED   |
   | 13/12/2016 02:43:41 | 1481597021_dropColumnFromTest | Konstantin | INACTIVE  |
   | 13/12/2016 02:43:51 | 1481597031_something          | Konstantin | INACTIVE  |
   +---------------------+-------------------------------+------------+-----------+
```

### FIN
