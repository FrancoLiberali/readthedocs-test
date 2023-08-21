==============================
Connecting to a database
==============================

Connection
-----------------------------

badaas-orm supports the databases MySQL, PostgreSQL, SQLite, SQL Server using gorm's driver. 
Some databases may be compatible with the mysql or postgres dialect, 
in which case you could just use the dialect for those databases (from which CockroachDB is tested).

To communicate with the database badaas-orm need a orm.DB object. 
To create it, you can use the function `orm.Open` that will allow you to connect to a database 
using the specified dialector with retrying. 
It also lets you configure the logger, for details visit :doc:`/badaas-orm/logger`.

When using badaas-orm with `fx` as :ref:`dependency injector <badaas-orm/concepts:Dependency injection>` you 
will need to provide (`fx.Provide`) a function that returns a `*orm.DB`.

You can access all the methods provided by gorm using the GormDB reference of the orm.DB object.

Migration
----------------------------

Migration is done by gorm using the `db.GormDB.AutoMigrate` method, where db is a orm.DB object.
For details visit `gorm docs <https://gorm.io/docs/migration.html>`_.

When using badaas-orm with `fx` as :ref:`dependency injector <badaas-orm/concepts:Dependency injection>` 
this method can't be called directly. In that case, badaas-orm will execute the migration by providing 
`orm.AutoMigrate` to fx. For this to work, you will need to provide also a method that returns 
`orm.GetModelsResult` with the models you want to include in the migration. 
Remember that the order in this list is important for gorm to be able to execute the migration.



