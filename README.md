# ALTSCHOOL CLOUD ENGINEERING
# DOCKER MINI-PROJECT WITH LARAVEL
-------------------------------------

## STEPS TAKEN
 1. Create non-root user with sudo privileges, and switch to that user.
 
 ```
 sudo adduser USERNAME
 sudo usermod -aG sudo USERNAME
 su - USERNAME
 ```
 
 2. Install Docker
 - Update system packages
 `sudo apt-get update`
 
 - Install required packages
 `sudo apt install apt-transport-https ca-certificates curl software-properties-common`
 
 - Add the GPG key for the official Docker repository:
 `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
 
 - Add the Docker repository to APT sources:
 `sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"`
 
 - Ensure installation is from the Official Docker Repo
 `apt-cache policy docker-ce`
 
 - Install Docker:
 `sudo apt install docker-ce`
 
 - Check if Docker is up and running
 `sudo systemctl status docker`
 
 - Add user to docker group
 `sudo usermod -aG docker ${USER} && su - ${USER}`
 
 - Download the 1.29.2 version and store the executable file to /usr/local/bin/docker-compose:
 
 ```
 sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 sudo chmod +x /usr/local/bin/docker-compose
 ```
 
 3. Clone the laravel repository
 `git clone https://github.com/laravel/laravel.git ~/altschool-docker-laravel`
 
 - Switch into the project's directory:
 `cd ~/altschool-docker-laravel`
 
 - Make $USER owner of project folder
 `sudo chown -R $USER:$USER ~/altschool-docker-laravel`
 
 4. Create docker-compose.yml and Dockerfile in the project folder.
 
 5. Configure PHP, NGINX and MYSQL
 
 - PHP: Create PHP directory and local.ini file. See php/local.ini file [here](https://github.com/ozirichigozie/altschool-docker-laravel/blob/main/php/local.ini)
 
 - NGINX: Create nginx/conf.d/app.conf file
 
 > Find content of app.conf file [here](https://github.com/ozirichigozie/altschool-docker-laravel/blob/main/nginx/conf.d/app.conf)

 - MYSQL:
   
   ```
   $ mkdir ~/altschool-docker-laravel/mysql
   $ vi ~/altschool-docker-laravel/mysql/mysql.cnf
   ```

 > Find content of mysql.cnf file [here](https://github.com/ozirichigozie/altschool-docker-laravel/blob/main/mysql/mysql.cnf)

 Customize Docker Environment Variables
 - Copy .env.example file to .env file
   `cp .env.example .env && vi .env`
 - ...and edit the code block shown below:

   ```
   DB_CONNECTION=mysql
   DB_HOST=db
   DB_PORT=3306
   DB_DATABASE=laravel
   DB_USERNAME=write_your_username
   DB_PASSWORD=write_your_password
   ```

 > Find content of .env.example file [here](https://github.com/ozirichigozie/altschool-docker-laravel/blob/main/.env.example)
 
 6. Run the Application Using Docker Compose 
 - Build app image
 `docker-compose build app`
 
 - Run environment in background mode
 `docker-compose up -d`
 
 - Display comprehensive information about files in the application directory
 `docker-compose exec app ls -l`
 
 - If composer.lock is present in the output of the previous command, run the next command, else skip it.
 `docker-compose exec app rm -rf vendor composer.lock`
 
 - Install the application dependencies:
 `docker-compose exec app composer install`
 
 - Create a special application key using the artisan Laravel command-line tool
 `docker-compose exec app php artisan key:generate`
 
 7. Visit http://your_server_ip in the browser


> ### NOTE: 
> -------------------------------------------
> This project was carried out on AWS EC2
> The AMI used was Ubuntu 20.04LTS 
