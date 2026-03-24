# Spotify Playlist Sorter User Guide
### Adam Pefanis, Joey Tada, Peter Berndtsson, Xavier Yick

## What does it do?
Spotify Playlist Sorter takes your playlists on your Spotify account, pulls them through the system, and lets you apply different filters to it. You can then export your filtered playlist to your Spotify account\!

## How do you install it?
Note 1: this requires a few things to be installed on your computer. If you have these installed, skip [here](#spotify-playlist-sorter-install). If not, see below:
* [PHP 8.4 Installation Instructions w/ Download Link](#php-84-installation-download-here)  
* [Composer 2.8.12 Installation Instructions w/ Download Link](#composer-2812-installation-download-here)  
* [NodeJS 24.11.0 Installation Instructions w/ Download Link](#nodejs-24110-installation-download-here)
  
Note 2: the setup is quite lengthy, and there will be a lot of back and forth. I did my best to make it as detailed as possible.  
Note 3: this guide will be updated regularly with each fix. Some steps may change between versions.  
Note 4: The bugs and issues section will be updated regularly. When we come across either a new bug/issue or a fix for an old one, we will keep you updated.

### PHP 8.4 Installation: [Download Here](http://www.php.net/downloads.php)
* NOTE: PHP 8.5 WILL NOT WORK. PLEASE DOWNLOAD PHP 8.4 BY DOING THE FOLLOWING:
  * Visit the link above.
  * Select your operating system.
  * Leave "ZIP Downloads" as is.
  * Click on "OS Default Version" and select "version 8.4".
  * This will allow you to download PHP 8.4.15. This is what you'll need for the install.
* Download the "Thread Safe" Zip for your computer.  
* Extract all to "C:\php". Create this folder if you do not have it already.  
* Rename "php.ini-development" to "php.ini".  
* Open the "php.ini" file, and use CTRL-F to search for the following items.   
  * There will be a semi-colon before each of the items. Remove the semi-colon, and save the file.  
  * ```
    extension=openssl
    extension=curl
    extension=fileinfo
    extension=mbstring
    extension=pdo_sqlite
    extension=sqlite3
    extension=zip 
    ```
* Add "C:\php" to your system variables by doing the following:  
  * Open Windows Search, and type "Edit the system environment variables".  
  * Click on "Environment Variables" at the bottom.  
  * In "System Variables", find "Path" and click on "Edit".  
  * Click on "New", then type "C:\php".  
  * Click on "OK" and then "OK" again.  
* PHP should now be installed. Verify by running ```php -v```.
  ```
  C:\Users\userName>php -v
  PHP 8.4.14 (cli) (built: Oct 21 2025 19:37:18) (ZTS Visual C++ 2022 x64)
  Copyright (c) The PHP Group
  Zend Engine v4.4.14, Copyright (c) Zend Technologies

  ***This should appear after running php -v.***
  ```

### Composer 2.8.12 Installation: [Download Here](https://getcomposer.org)
* Download the "Composer-Setup.exe" from the link above.
* Select either "Install for all users" or "Install for me only", whichever applies to you.
* Leave the "Developer mode" option unchecked, and click "Next".
* If you have PHP installed already, it should auto-fill the path with "C:\php\php.exe".
* Check off "Add this PHP to your path?", then click "Next".
* Leave "Use a proxy server to connect to internet" unchecked, and click "Next".
* You can then verify all of the information, and go through with the install.
* Composer should now be installed. Verify by running ```composer -V``` in a new command line.
  ```
  C:\Users\userName>composer -V
  Composer version 2.8.12 2025-09-19 13:41:59
  PHP version 8.4.13 (C:\php\php.exe)
  Run the "diagnose" command to get more detailed diagnostics output.

  ***This should appear after running composer -V.***
  ```

### NodeJS 24.11.0 Installation: [Download Here](https://nodejs.org/en/download)
* Download the appropriate installer for your application.  
* Ensure that "Add to PATH" is enabled.  
* NodeJS should now be installed. Verify by running ```node -v``` and ```npm -v``` in a new command line.
  ```
  C:\Users\userName>node -v
  v24.11.0
 
  C:\Users\userName>npm -v
  11.6.1

  ***This should appear after running node -v and npm -v.***
  ```

  
### Laravel Herd Installation (WINDOWS ONLY): [Download Here](https://herd.laravel.com/download/latest/windows)
Herd is a Laravel-based integrated PHP development environment for Windows. 
1. Download Herd from the link above.
2. Run the provided ``Herd-x.x.x.x-setup.exe``
3. Follow the prompts provided by the installer
4. Once the installation is complete, open the Herd application.


### Spotify Playlist Sorter "Install"
1. Open Command Line
1.5 (WINDOWS ONLY) Using `cd /filepath`, navigate to C:/users/*username*/Herd
2. In your command line, run the following commands:
   ```
     git clone https://github.com/MRU-F2025-COMP3504/3504-term-project-spotify-playlist-sorter
     cd 3504-term-project-spotify-playlist-sorter
     git switch dev
   ```
3. Install Composer Packages by running ```composer install```.   
4. Verify Laravel’s Artisan tool’s presence by running ```php artisan```.   
5. Install Vite by running ```npm install```.  
6. Visit https://developer.spotify.com/, log into your Spotify account, then head to the dashboard.  
7. Click on "Create app", and give it a name and description.  
8. Add "http://127.0.0.1:8000/auth/callback" under "Redirect URIs".  
9. Select "Web API" and "Web Playback SDK" under the "Which API/SDKs are you planning to use?" section.  
10. Agree and save.
11. Open your Spotify application on the dashboard.
12. Locate your "Client ID" and "Client Secret". We'll use these soon.
13. In the repository, locate the ".env.example" file, and create a copy named ".env".  
14. Take those values found in step 12, and enter them into their respective space in the ".env". Save the file.
    * Note: Make sure there are no spaces between the key and the value. It should look like this below:
       ```
       SPOTIFY_CLIENT_ID=enterYourClientIDHere
       SPOTIFY_CLIENT_SECRET=enterYourClientSecretHere
       SPOTIFY_REDIRECT_URI=http://127.0.0.1:8000/auth/callback
       ```
15. Run ```php artisan key:generate```. This should fill in the ```APP_KEY=``` field in the ".env" file.
16. Verify that ```APP_KEY``` in the ".env" file is not empty.
17. That's it for the "install"!

## How do you run it?
1. In a command line, navigate to the repository and run ```composer run dev```.  
   1. You may run into some issues here, depending on which operating system you are on.  
   2. If you are on Linux or macOS, skip to step 2\.  
   3. If you are on Windows, complete steps a-e:  
      1. Navigate to the "composer.json" file in the repository.  
      2. Use CTRL-F and search for the following: ```"npx concurrently -c \"#93c5fd,#c4b5fd,#fb7185,#fdba74\" \"php artisan serve\" \"php artisan queue:listen --tries=1\" \"php artisan pail --timeout=0\" \"npm run dev\" --names=server,queue,logs,vite --kill-others"```
      3. Remove ```\"php artisan pail --timeout=0\"```.  
      4. Save and close the file.  
      5. Run the composer command again.  
2. If you run into database-related errors, run ```php artisan migrate``` 
3. You're all good to go! Navigate to "http://127.0.0.1:8000".

## How do you use it?
Using the Spotify Playlist Sorter is easy\! Here are some steps that you can follow:
1. Click on the “Login with Spotify” button. This will bring you to the Spotify login page, where you can login to your account.   
2. Once you enter your credentials, you will need to click on “Agree”. This will grant us the ability to create, edit, and follow your playlists.  
3. Once you are logged in, you’ll be greeted with a homepage that contains your playlists.  
4. Select the playlist that you want to filter.  
5. You’ll have a few filters that you can apply to your selected playlist. Once you are happy with the applied filters, click on “Apply Filters”.   
6. If you are satisfied with this playlist, click on “Export Playlist”. This will save it to your Spotify library.  
7. If you want to go back and change something, click on “Back to filters”.  
8. You’re done!

## How can you report an issue or bug?
If you come across an issue or bug, you can report it to us at https://github.com/MRU-F2025-COMP3504/3504-term-project-spotify-playlist-sorter/issues
* Ideally, this template below would be great as it allows us to know exactly what happens and where. If you can’t fill in a section, you can just put “N/A” or “Unknown”.  
* When filling out the template, please add as much detail as you can. This would be greatly appreciated, and makes it easier for us to pinpoint what went wrong.  
* Attachments are not necessary, but would be very helpful.

### Issue/bug reporting template
What happened?:   
Where does this happen?:   
What steps did you take to encounter this issue/bug?:   
Operating System:   
Browser:   
Attachments: 

## Known issues and bugs
1. Currently, there is a bug that prevents Spotify Playlist Sorter and Spotify from syncing everything perfectly. You may not be able to sync your playlists currently.
2. When setting up the software, navigating to http://127.0.0.1:8000/auth/callback may bring you to a 404 page. This can be alleviated by removing "/login" from the URL.
3. After logging in, you may be brought to a page with a PHP dump. This can be alleviated by removing "/login" from the URL.
