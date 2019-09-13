# liquibase-utils

https://www.jannikarndt.de/blog/2018/08/rotating_postgresql_passwords_with_no_downtime/

Liquibase generates a hash for every changeset and warns you, if a hash changed. Since the WITH LOGIN and WITH NOLOGIN attributes are supposed to change, we add the runOnChange attribute, which just runs the SQL command again. Note that this only works with idempotent commands, like ALTER. Running a CREATE ROLE twice would result in an error.

To automatically have different passwords for prod and dev (and local), we use the context attribute. This is evaluated if you add --contexts=prod to the command line when running liquibase. Note that if you don’t provide the command line argument, the changeset will not be run at all.

And lastly, the passwords are loaded from an external file, so you can make sure that this is either on the .gitignore list or encrypted (e.g. via git-crypt).

https://aws.amazon.com/blogs/database/managing-postgresql-users-and-roles/
https://docs.aws.amazon.com/secretsmanager/latest/userguide/managing-secrets.html
https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.PostgreSQL.CommonDBATasks.html#Appendix.PostgreSQL.CommonDBATasks.RestrictPasswordMgmt
