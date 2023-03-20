## Clock Update

### How to setup dev environment
---------------------------------

- install Docker
- Clone (https://github.com/mana82/clock-update.git) repository and go to the project directory
- Create .env file and run the below commands
```bash 
cp .env.example .env

composer install 

./vendor/bin/sail up -d 

sail artisan optimize

sail artisan migrate

sail npm install

sail npm run dev
```

- visit http://localhost

### Configuring A Shell Alias
---------------------------------
```bash 
alias sail='[ -f sail ] && sh sail || sh vendor/bin/sail'
```

- to stop sail run 
```bash 
sail stop
```
- Remove all the unused data run  
```bash 
docker system prune -a
```

### Run test 
- Change your .env file APP_ENV to testing (APP_ENV=testing) and tehn run below commands
```bash 
sail artisan config:clear

sail artisan optimize

sail artisan test


```