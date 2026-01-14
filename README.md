# laravel-API-with-JWT-CRUD
## Laravel API with JWT & CRUD & Heroku 

--------------------
### First you have to download:
    XAMPP, MySQL, MySQL workbench 
    Postman, Heroku, Composer, Git
--------------------
### You have to install Laravel
````laravel
Composer global require “Laravel/install”
Composer create-project –prefer-dist Laravel/Laravel (project name)
````
--------------------
### Prepare Heroku (Cloud):
````laravel
Heroku create
Heroku logout
Heroku login 
Heroku config:set APP_KEY=
Heroku open
````

````laravel
Echo web:vendor/bin/heroku-php-apache2 public /procfile
Heroku create 
Git push heroku master
````
--------------------
### Create a procfile :
````laravel
 web:vendor/bin/heroku-php-apache2 public /

git add.
Git commit -m “ “
Git push heroku master
````
--------------------
### In mysql workbench :
New connection, New schema
Also in .env file , edit ( Database , username , password)

--------------------


### Inside of Heroku cloud:
Go resource and do add-ons and chose clearDB
And then write :
````laravel
Heroku config|grep CLEARDB_DATABASE_URL
````
	And you have to copy (@... .net) and use it as hostname 
And edit .env file (Database , username , password , host)
````laravel
Php artisan migrate
````

If you found error ( key too long , max lenth …etc )
  1- Fo to migration both (create_users, create_password)
  2- Go to public function up()
Write 
````laravel
Schema::defultStringLenght(191);
````
  3- Go to workbench , Drop (migration , users)
  4- Then do 
````laravel
Php artisan migrate
Git add.
Git commit -m “”
Git push heroku master
````

--------------------
### To creat JWT , write in bash

````laravel
Composer require Tymon/jwt-auth
````
Inside in file config/app.php in providers , write:
````laravel
’Tymon\JWTAuth\Providers\JWTAuthServiceProvider’;
````
In aliases , write:
````laravel
‘JWTAuth’=> ‘Tymon\JWTAuth\Facades\JWTAuth’
‘JWTFactory’=> ‘Tymon\JWTAuth\Facades\JWTFactory’
````
 And write in terminal:
````laravel
Php artisan vendor:publish—provider=’Tymon\JWTAuth\Providers\JWTAuthServiceProvider’
````
 And write 
````laravel
Php artisan jwt:generate
````
   If you found erro in handle, do this:
Go to folder vendor , file Tymon >Src>commands>JWTGenerateCommand
Inside in class JWTGenerateCommand
Write 
````laravel
Public function handle(){
$this->fire();
}
````
And again to generate
````laravel
Php artisan jwt:generate
````
And it show Jwt-auth serect[-]
````laravel
Php artisan migrate
````


--------------------
### Lesson 7- Make controller 

Inside controller:
````laravel
Use App\Http\Controllers\Controller;
Use App\User;
Use JWTFactory;
Use Validator;
Use Response;

$request->get()
$request->all()
::first()
Validator::make()
JWTAuth::fromUser
Response::json(compact())
````

And also you need to connect controller to route (api.php)
--------------------
````laravel
Use Illuminate\Support\Facades\Auth

JWTAuth::attempt();
````
--------------------
Middleware
In File Http > Kernel:
In Protected $routeMiddleware:
````laravel
‘jwt.auth’=> ‘Tymon\JWTAuth\Middleware\GetUserFromToken’,
‘jwt.refresh=> ‘Tymon\JWTAuth\Middleware\refreshToken’,
````

In route(api.php)
````laravel
Route::middleware(‘jwt.auth’)
Return auth()->user()
````
--------------------
Migration 
````laravel
Php artisan make:migration ….
````
some syntax have to write :
````laravel
ToArray()
->fails()
->errors()
->all()
->save()
->delete()
:make
:create
::find()
Validator
````




