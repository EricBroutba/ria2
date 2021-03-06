# RIA2 - Datalab API

This project setup a basic **API** for the *CPNV DATALAB*.  
The api allow people to access to the data used in during the project.  

For more information, the [documentation](fr.docs.md) is avaiable (in french).  

## Prerequisites
* Apache / Nginx
* PHP (with PECL)

## Installation
Install MongoDB on Ubuntu 16.04:   
```bash
# Import the public key used by the package management system.  
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5  

# Create a list file for MongoDB.  
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list  

# Reload local package database.  
sudo apt-get update  

# Install the MongoDB packages.  
sudo apt-get install -y mongodb-org  

```  

Start MongoDB.  
```bash
sudo service mongod start  
```  
To keep the service up in case of reboot, use  
```bash
sudo systemctl enable mongod
```  

_source: https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/_  

By default, mongodb has no enabled access control, which means there's no default user or password.  
User creation: 
```bash
mongo --port 27017
```  
And create a admin user.  
```bash
use admin
db.createUser(
  {
    user: "laravel",
    pwd: "root",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
```  

`sudo apt-get install libmongoc-1.0-0`  


install the php-mongodb driver :
```bash
sudo pecl install mongodb
```  
Add the following line to your `php.ini` file for **fpm** and **cli**.  
`extension=mongodb.so`  

sudo systemctl restart php7.2-fpm.service
    
_source: http://php.net/manual/en/mongodb.installation.pecl.php_  

Then run `composer install`  

Make a **.env** file, or copy the example.  
`cp .env.example .env`  
Generate the key.  
`php artisan key:generate`  
And you should be good to go.  

## Usage

| method | route                      | description                                 | fields     |
|--------|----------------------------|---------------------------------------------|------------|
| GET    | /api/projects              | Return a list of all the projects.          |            |
| POST   | /api/projects/{project_id} | Create (or update) a project with its data. | json: data |
| GET    | /api/projects/{project_id} | Get specific project                        |            |

## Docs

* [French documentation](fr.docs.md)

## License
This project is licensed under the MIT License - see the [license](license) for details.  
