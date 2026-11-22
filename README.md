# DalHive
Dalhousie Dalplex busyness tracker 
# Dalplex Busyness Meter

A small website that shows how busy the Dalplex (Dalhousie University's athletic facility) is right now. It displays a speedometer-style gauge that updates based on the current day and hour.

## How It Works

1. The page loads and runs the JavaScript.
2. The JavaScript asks dalplex.php for the busyness data.
3. dalplex.php sends back dalplex.json. If that file is 30+ days old (or missing), it first gets fresh data from the BestTime API (https://besttime.app).
4. The JavaScript finds the value for the current day and hour and moves the gauge needle.
5. The gauge label shows one of three levels:
   - Low (0-35): plenty of space
   - Moderate (36-70): moderately busy
   - High (71-100): very crowded

## Technologies Used

- HTML, CSS, and JavaScript (ES modules)
- Bootstrap
- PHP (for the data endpoint)
- BestTime API (for busyness forecasts)

## Project Files

- dalplex.php: serves the busyness data and refreshes it from BestTime when it is old
- dalplex.json: the saved busyness data (created automatically)
- busynessData.js: loads the data and has helper functions to look up a day/hour
- Gauge script: reads the current day/hour and updates the gauge and status text
- CSS file: styling for the page, using Dalhousie's black and gold colours
- config.example.php: example config file for the API key
- .htaccess: blocks web access to private files like config.php

## Setup

1. Get a private API key from BestTime (https://besttime.app).
2. Copy config.example.php to a new file called config.php.
3. Open config.php and replace PRIVATE_KEY with your real key:

   return [
       'besttime_api_key' => 'your-key-here',
   ];

4. Do not share config.php or upload it to GitHub (it should be in .gitignore).

## Running It Locally

You need PHP installed. In the project folder, run:

   php -S localhost:8080

Then open http://localhost:8080 in your browser.

Note: The page must be run through a server (not by double-clicking the HTML file), because it uses JavaScript modules and a PHP file.

## Notes

- If the BestTime request fails, the site keeps showing the old data and tries again after an hour.
- The first time you run it, dalplex.json will be created automatically as long as your API key works.
- The busyness numbers are forecasts, not live counts.

## Credits

- Busyness data from BestTime (https://besttime.app)
- Colours inspired by Dalhousie University branding
- Made for a school project
