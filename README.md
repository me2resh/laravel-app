## Setup instructions

#### 1 - Clone the repo
```bash
git clone https://github.com/me2resh/laravel-app.git
```

#### 2- Run composer install
```bash
docker run --rm -v $(pwd):/app composer install
```

#### 3- Set environment settings by creating .env file
```bash
cp .env.example .env
```

#### 4- Start the application docker containers
```bash
docker-compose up -d
```

#### 5- Login to DB container to create a user to access the database 
```bash
docker-compose exec db bash
mysql -uroot -p{password from docker-compose file}
```
Inside the mysql shell run:
```sql
GRANT ALL ON laravel.* TO 'laraveluser'@'%' IDENTIFIED BY 'your_laravel_db_password';
FLUSH PRIVILEGES;
EXIT;
```
Exit the container
```bash
exit

```
#### 6- Modify the .env file
```bash
vim .env
```

Modify the following section to the user & password you have created
```yml
DB_DATABASE=laravel
DB_USERNAME=laraveluser
DB_PASSWORD=your_laravel_db_password
```


#### 7- Configure laravel application
Set application key for laravel application
```bash
docker-compose exec app php artisan key:generate
```

Cache environment settings to boost application's load speed
```bash
docker-compose exec app php artisan config:cache
```

#### 8- Run migrations
```bash
docker-compose exec app php artisan migrate
```



