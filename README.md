# COMP-3504-Project
* Creation date: Fall 2025 (Year 4) 

### Communication channel:
https://discord.gg/UCVpZKRjWD

### Shared Drive:
https://drive.google.com/drive/folders/0ABiLUBbjGoZKUk9PVA

### Contributors:
* Adam Pefanis
* Xavier Yick
* Joey Tada
* Peter Berndtsson

### Systems:
#### Framework, Language and Dependencies:
- PHP 8.4.14
- [Laravel 12](https://laravel.com/docs/12.x/releases)
  - Artisan command line - command line for executing Laravel and composer commands for building, testing and using our project.
  - Eloquent ORM framework - Laravel framework for ORM and database handling.
- [Composer](https://getcomposer.org/) PHP/Laravel command-line dependency handling.
- [HERD](https://herd.laravel.com/windows) Windows Laravel development environment.

#### CI/CD:
- [Pest](https://pestphp.com/docs/installation) PHP Testing Framework
- [Github Actions](https://github.com/features/actions) CI/CD system

### To Build:
Please check the [user guide](https://github.com/MRU-F2025-COMP3504/3504-term-project-spotify-playlist-sorter/blob/feedback/Spotify%20Playlist%20Sorter%20User%20Guide.md) for more information regarding how to build the software.

### To Test:
Please check the [developer guide](https://github.com/MRU-F2025-COMP3504/3504-term-project-spotify-playlist-sorter/blob/feedback/DeveloperGuide.md) for more information regarding how to test the software.

#### Our Tests:
* **AccessTest.php** - Confirms that our tests are able to access ApplyFilters.php
* **fetchPlaylistTest.php** - Confirms that ApplyFilters.php can access and parse data from our model (database.sqlite)
* **filterByArtistTest.php** - Confirms that ApplyFilters.php can retrieve only songs with a "Fly By Nightcore" artist tag.
* **filterByExplicitTest.php** - Confirms that ApplyFilters.php can retrieve only songs without an "explicit" tag.

### Operational Use Cases:
* **Sign-In** - Users are able to provide their Spotify credentials by entering this data into our interface, with which our program authenticates with Spotify and retrieves a list of the user's playlists and favorited songs.
* **ORM** - Given Spotify playlist data selected from a list of playlists obtained in the previous use case, the user can select a playlist to manipulate in our interface. With this interaction, our program is able to retrieve, index and parse track items for the given playlist. 
* **Playlist Filtering** - Given a parsed playlist (per our ORM use case), our program is able to apply a list of user-supplied filters added from our interface, to build a playlist subset only including tracks that match the user filter.
