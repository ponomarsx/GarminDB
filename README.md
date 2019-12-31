[![Screen shot of browsing the DB](https://raw.githubusercontent.com/tcgoetz/GarminDB/master/Screenshots/ScreenShot_browsing_sm.jpg)](https://github.com/tcgoetz/GarminDB/wiki/Screenshots)

[![Screen shot of a daily graph](https://raw.githubusercontent.com/tcgoetz/GarminDB/master/Screenshots/Screen_Shot_daily_graph.jpg)](https://github.com/tcgoetz/GarminDB/wiki/Screenshots)

[![Screen shot of a steps graph](https://raw.githubusercontent.com/tcgoetz/GarminDB/master/Screenshots/Screen_Shot_steps_graph.jpg)](https://github.com/tcgoetz/GarminDB/wiki/Screenshots)

# GarminDB

[Python scripts](https://www.python.org/) for parsing health data into and manipulating data in a [SQLite](http://sqlite.org/) DB. SQLite is a light weight DB that requires no server.

What they can do:
* Automatically download and import Garmin daily monitoring files (all day heart rate, activity, climb/descend, stress, and intensity minutes) from the user's Garmin Connect "Daily Summary" page.
* Extract sleep, weight, and resting heart rate data from Garmin Connect, store it as JSON files, and import it into the DB.
* Download and import activity files from Garmin Connect. A summary table for all activities and more detailed data for some activity types. Lap and record entries for activities.
* Copy daily monitoring and/or activities Fit files from a USB connected Garmin device.
* Import Fitbit daily summary CSV files (files with one summary entry per day).
* Import MS Health daily summary CSV files and MS Health Vault weight export CSV files.
* Summarizing data into `stats.txt` and a common DB with tables containing daily summaries, weekly summaries, and monthly summaries.
* Graph your data.
* Retain data as JSON files or FIT files so that the DB can be regenerated without connecting to Garmin.
* Export activities as TCX files.

Once you have your data in the DB, I recommend using a SQLite browser like [SQLite Studio](http://sqlitestudio.pl) or [DB Browser for SQLite](https://sqlitebrowser.org/) for browsing and working with the data. The scripts create some default [views](http://www.tutorialspoint.com/sqlite/sqlite_views.htm) in the DBs that make browsing the data easier.

# Using It

## Binary Release

I have just started offering a binary release for MacOS. Binary release for other platforms may be added. You can download releases from the [release page](https://github.com/tcgoetz/GarminDB/releases).
For the MacOS binary release:
* Download the zip file and unzip it into a directory.
* Follow the directions in the `Readme_MacOS.txt` in the zip file.

## From Source

The scripts are automated with [Make](https://www.gnu.org/software/make/manual/make.html). Run the Make commands in a terminal window.

* Git clone GarminDB repo using the SSH clone method. The submodules require you to use SSH and not HTTPS. Get the command from the green button on the project home page.
* Run `make setup` get the scripts ready to process data.
* Copy `GarminConnectConfig.json.example` to `GarminConnectConfig.json`, edit it, and add your Garmin Connect username and password and adjust the start dates to when your data starts from.
* Run `make create_dbs` for your first run.
* Keep all of your local data up to date by running only one command: `make`.
* Run `make backup` to backup your DBs.

More [usage](https://github.com/tcgoetz/GarminDB/wiki/Usage)

# Notes

* You may get a DB version exception after updating the code, this means that the DB schema was updated and you need to rebuild your DBs by running `make rebuild_dbs`. Your DBs will be regenerated from the previously downloaded data files. All of your data will not be redownloaded from Garmin.
* The scripts were developed on MacOS. Information or patches on using these scripts on other platforms are welcome.
* Running the scripts on Linux should require little or no changes. You may need to [install](https://github.com/tcgoetz/GarminDB/wiki/Usage) `git` and `make`.
* There are two ways to use this project on Windows. Installing the [Ubuntu subsystem](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) on Windows 10 is one way. Using a Linux container or VM is also possible.
* If you have issues, file a bug here on the project. See the Issues tab at the top of the project page. Run `make bugreport`and include bugreport.txt in your bug report.
* When a database update finishes, a summary of the data in the DB will be saved to stats.txt. The output includes the date ranges included in the downloaded daily monitoring files and activities. It includes the number of records for daily monitoring, activities, sleep, resting heart rate, weight, etc. Use the summary information to determine if all of your data has been downloaded from Garmin Connect. If not, adjust the dates in GarminConnectConfig.json and runt he download again.
