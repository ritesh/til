# Setting up on Linux
After you `apt-get` postgres, switch to the `postgres` user
```
$ sudo su - postgres
$ createuser <youruserid>
$ createdb <youruserid>
```
=psql= should now let you connect to your very own personal database without a password (uses ident authentication).
