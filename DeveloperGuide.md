## Source Code
Our current development branch is **dev**. All relevant source code is located here, in the directories listed in this document.

## Layout 
The following is an overview of our projects layout and relevant directories:

* **/app** includes our controllers, per our model-view-controller architecture.
   * **/Controller** includes Filter.php, a deprecated version of ApplyFilters.php.
   * **/Http/Controllers** contains our core controller logic. 
      * **ApplyFilters.php** receives a list of filter criteria from our View and applies them to the user's playlists.
      * **SpotifyController.php** handles our authentication and ORM, by connecting to Spotify, retrieving playlists and saving tracks to our internal database.
   * **/Jobs** is a list of basic Jobs performed by our controllers.
      * **GatherPlaylists.php**, when given an access token, gathers the user's playlists into our Model.
      * **GatherSinglePlaylist.php** handles the creation of new GatherPlaylists.php instances.
   * **/Models** includes the blueprints for our database objects, and defines the relationships between artists, tracks, playlists and users.
   * **/Providers** includes our [Service Providers](https://laravel.com/docs/12.x/providers), which act as blueprints for our OAuth system. 
   * **/Repositories** includes **SpotifyRepository.php**, which translates Spotify playlist data into our internal schema and stores it in our database.
   * **/View/Components** includes **TrackListItem.php**, which builds and supplies Track objects to our view component.
* **/bootstrap** includes basic setup configs. These are unlikely to be modified.
* **/config** defines necessary access variables for our OAuth system.
* **/database** is the core of our Model component. This includes our database, seeders and factories.
   * **database.sqlite** is our central database. This is gitignored, and must be populated in each build by our seeders or OAuth.
   * **/seeders** contains a list of "dummy" data for our database, which fills the database during tests.
   * **/factories** contains one [factory](https://laravel.com/docs/12.x/eloquent-factories#main-content), **UserFactory.php**, which creates a fake user and fills in data that would otherwise be sensitive.
* **/public** includes **index.php**, our homepage. 
* **/reports** holds only our weekly reports. There is no functional code here.
* **/resources** includes our CSS, Javascript and view components.
* **/routes** contains a list of handlers for external requests. More information on routes can be found [here](https://laravel.com/docs/12.x/routing).
* **/storage** is not used in a dev environment, but provides space for cache, cookie and session data.
* **/tests** contains our feature and unit tests.
   * **/tests/Feature** contains the four major automated tests performed by our CI/CD.
   * **/tests/Unit** is infrequently used, as the highly integrated nature of our project limits the usefulness of individual unit tests.
* **env.example** is our example environment config for our production branch. During a build, this is transformed into .env
* **env.testing** is our environment config for testing.
* **composer.json** is the config for Composer, our dependency manager.
* **composer.lock** is another piece of our Composer config, but includes links to our dependencies and vendors.
* **package.json** is a dependency list for NPM, which handles our Node.js dependencies.
* **phpunit.xml** is a list of environment configs for PHP.
* **README.md** provides a high-level overview of our functions, build instructions, use cases and tests.

## Build Instructions 
Detailed build instructions can be found on our [Spotify Playlist Sorter User Guide](https://github.com/MRU-F2025-COMP3504/3504-term-project-spotify-playlist-sorter/blob/feedback/Spotify%20Playlist%20Sorter%20User%20Guide.md).

## Testing 

### Testing via Github Actions CI/CD
Our test suite runs automatically with each commit. 

To perform tests via Github Actions, make a commit to the project and navigate to the ACTIONS tab of the Github repo. Our tests will run and the results will be displayed.


### Testing in Command Line via Artisan CLI
With the project built on your device, open up command line via Herd. To do this:
1. Open the Herd interface
2. Navigate to the **Sites** tab on the left-hand menu
3. Herd should display 3504-term-project-spotify-playlist-sorter on the right-hand menu. There, you will find a **terminal** button. Press this to open the CLI.
4. With the CLI open, verify that you are in the 3504-term-project-spotify-playlist-sorter directory. If this is not the case, navigate to this directory with **cd**.
5. Once in the 3504-term-project-spotify-playlist-sorter directory, run **php artisan test --env=testing**. It is vital to use the testing environment, as this ensures you are operating with a seeded test database.


### Adding New Tests 

Are there any naming conventions/patterns to follow when naming test files? Is there a particular test harness to use?
Setting up a new test is simple. Testing in Pest is natively supported by Laravel, which hosts extensive documentation on the creation of unit tests.
Note: this requires composer to be installed on the user’s computer.

1. Download the latest package from the repository.
2. Open command line
3. Verify composer’s presence by running **composer -v**
4. Verify Laravel’s Artisan tool’s presence by running **php artisan**
5. If both function, create a new test with **php artisan make:test testName**
5.5 (optional) by default, make:test creates a feature test. To save your test to **tests/Unit/**, run **php artisan make:test testName --unit**
6. This will create a blank test file in **tests/Unit/** or **tests/Feature/** (preferred)
7. To modify this to work with an existing function, follow the documentation [here](https://pestphp.com/docs/writing-tests).
8. For instance, a test of the imaginary function **addThese($a,$b)** will appear as:
   
```
test('addTheseTest', function () {
   $result = addThese(1, 1);
   expect($result)->toBe(2);
});
```

Of note is the name **addTheseTest**, which will be invoked in testing. The test calls addThese() and returns the value to result, which is compared with the desired output via an **expect()->toBe()** statement.

