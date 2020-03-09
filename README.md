## mysql docker-compose sample

### NOTE：HOW TO USE
Basic

```
// to start
$ docker-compose up -d
// enter the container
$ docker exec -it sample_db bash
// login mysql
$ mysql -u beeeeyan -ptest
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| sample_db          |
+--------------------+

mysql> use sample_db;
mysql> show tables;
+---------------------+
| Tables_in_sample_db |
+---------------------+
| users               |
+---------------------+
1 row in set (0.00 sec)

mysql> select * from users;
+----+----------+----------+--------------------+
| id | username | password | email              |
+----+----------+----------+--------------------+
|  1 | keid     | keidpass | keid@developer.com |
|  2 | jobs     | jobspass | jobs@developer.com |
|  3 | mask     | maskpass | mask@developer.com |
+----+----------+----------+--------------------+
3 rows in set (0.01 sec)

mysql>
```

To access mysql in container from my local environment.

```
$ mysql -u beeeeyan -ptest -h 127.0.0.1 --port 33306
```

Other example
→ SQLAlchemy

```config.py
import os

class Config(object):
    '''
    Config Class
    '''
    # SQLAlchemy
    SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://{user}:{password}@{host}:33306/sample_db?charset=utf8'.format(**{
        'user': os.getenv('DB_USER', 'beeeeyan'),
        'password': os.getenv('DB_PASSWORD', 'test'),
        'host': os.getenv('DB_HOST', '127.0.0.1'),
    })
```