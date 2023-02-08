### Getting ready

#### Install Choco
This can be found [here](https://chocolatey.org/install)

* Launch `Powershell` as Admin
* Run: `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))`
* Run: `choco -?`

#### Install Composer
Installs PHP as well, regardless of existing XAMP installation
It will also tell you WHERE it installed it, mine was installed to `C:\tools\php82`

* Launch `Powershell` as Admin
* Run: `choco install composer`

#### Install NodeJS and NPM

* Launch `Powershell` as Admin
* Run: `choco install -y --force nodejs-lts`
* Run: `npm i -g npm`

#### Create the Laravel project with TailwindCSS
This can be found [here](https://tailwindcss.com/docs/guides/laravel)

It will create a subdirectory where you are with the name of `project_name`

* Launch `Powershell` as Admin
* Run: `composer create-project laravel/laravel project_name`
* Open the created directory in your IDE as a project
* Your IDE also has a terminal option which is `Powershell` (but not as admin)
* Go to where PHP was installed and open `php.ini` find `;extension=fileinfo` and replace it with `extension=php_fileinfo.dll` and then save the file
* Run: `composer install`
* Run: `npm install`
* Run: `npm install -D tailwindcss postcss autoprefixer`
* Run: `npx tailwindcss init -p`
* Make `tailwind.config.js` look like this:
```
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
      "./resources/**/*.blade.php",
      "./resources/**/*.js",
      "./resources/**/*.vue",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}

```
* Make `resources/css/app.css` look like this:
```
@tailwind base;
@tailwind components;
@tailwind utilities;

```
* Delete `welcome.blade.php` in `resources`
* Make a new file called `app.blade.php` inside `resources` and put the following content in it:
```
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  @vite('resources/css/app.css')
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```
* Open `web.php` inside `routes` and change `welcome` to `app`

#### Running the code locally
You need 2 Terminal sessions, luckily your IDE allows you to run multiple in one screen

In one of them you need to run: `php artisan serve`

In the other you need to run: `npm run dev`

PHP Artisan will run the code on `http://localhost:8000` by default, quick link [here](http://localhost:8000)
