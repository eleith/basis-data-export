# Basis Data Export

Utility that exports and saves your Basis Health Tracker (B1/Peak) uploaded sensor data, as described at [https://www.quantifiedbob.com/2013/04/liberating-your-data-from-the-basis-b1-band/](https://www.quantifiedbob.com/2013/04/liberating-your-data-from-the-basis-b1-band/)
You can learn more about Basis at [http://www.mybasis.com/](http://www.mybasis.com/)

> UPDATE AUGUST 3, 2016 -

> Intel (who acquired Basis) has notified users that they will be discontinuing all Basis devices and services on December 31, 2016. Make sure to download all of your data before then! See [http://www.mybasis.com/safety/](http://www.mybasis.com/safety/) to learn more.

## Instructions

In order to use this script, you must already have a Basis account

### Usage:

```
$ php basisdataexport.php
-------------------------
Basis data export script.
-------------------------
Enter Basis username [me@somewhere.com]: me@somewhere.com
Enter Basis password [********]: 
Enter data export start date (YYYY-MM-DD) [2016-08-22] : 
Enter data export end date (YYYY-MM-DD) [2016-08-22] : 
Enter export format (json|csv|html) [json] : 
```

1. Open a terminal window and cd to this script's directory
2. Type `php basisdataexport.php`
3. Follow the prompts (hit ENTER to use default values)
4. Your data will be saved to `/data/basis-data-[YYYY-MM-DD].[format]`

## Saving Your Data
If the script runs successfully, your data will be saved in the `data/` folder. Files are saved in the format `basis-data-[YYYY-MM-DD].[format]` (i.e., `basis-data-2014-04-04.json`).

That's it! (for now).


## Biometric Data

Basis currently returns the following biometric data points. They each represent an average (i.e., for heart rate, GSR, skin/air temperature) or sum (i.e., steps, calories) over the previous 1-minute period:

- Time - time reading was taken
- Heart Rate - beats per minute
- Steps - number of steps taken
- Calories - number of calories burned
- GSR - Galvanic skin response (i.e., sweat/skin conductivity. Learn more about GSR here - [http://en.wikipedia.org/wiki/Skin_conductance](http://en.wikipedia.org/wiki/Skin_conductance))
- Skin Temperature - skin temperature (degrees F)
- Air Temperature - air temperatute (degrees F)

There are some other aggregate metrics included in the reponse such as min/max/average/standard deviation metrics for each set of data.

## Sleep Data

Basis currently returns the following sleep data points (it's in a different format than the metrics data because it's a newer version of their API):

- Start Time - local timestamp in MM/DD/YY HH:MM format
- Start Time ISO - user timestamp in ISO format
- Start Time Time Zone - user time zone, i.e., America/New_York
- Start Time Offset - minutes offset from GMT (i.e., -240 for America/New_York)
- End Time - user timestamp in MM/DD/YY HH:MM format
- End Time ISO - user timestamp in ISO format
- End Time Time Zone - user time zone, i.e., America/New_York
- End Time Offset - minutes offset from GMT (i.e., -240 for America/New_York)
- Light Minutes - number of minutes in "light sleep" stage
- Deep Minutes - number of minutes in "deep sleep" stage
- REM Minutes - number of minutes in "REM sleep" stage
- Interruption Minutes - number of minutes interrupted (i.e., woke up, went to bathroom, etc.)
- Unknown Minutes - number of minutes unknown (i.e., device wasn't able to take readings)
- Tosses and Turns - number of tosses and turns that occurred
- Type - always returns 'sleep'
- Actual Seconds - total sleep time recorded, in seconds
- Calories - number of calories burned
- Average Heart Rate - beats per minute
- Minimum Heart Rate - beats per minute (currently this always returns null)
- Maximum Heart Rate - beats per minute (currently this always returns null)
- State - returns 'complete' if event was completed at time of export
- Version - API version used (i.e., 2)
- ID - internal id for given sleep event

Sleep data is often broken into multiple segments - Basis treats each sleep activity as a separate 'event' if there is a 15-minute gap in readings (i.e., sensors couldn't detect anything).

## Activity Data

Similar to sleep data, Basis currently returns the following activity data points (walking, biking, running):

- Start Time - local timestamp in MM/DD/YY HH:MM format
- Start Time ISO - user timestamp in ISO format
- Start Time Time Zone - user time zone, i.e., America/New_York
- Start Time Offset - minutes offset from GMT (i.e., -240 for America/New_York)
- End Time - user timestamp in MM/DD/YY HH:MM format
- End Time ISO - user timestamp in ISO format
- End Time Time Zone - user time zone, i.e., America/New_York
- End Time Offset - minutes offset from GMT (i.e., -240 for America/New_York)
- Type - activity type (i.e., walk, run, bike)
- Actual Seconds - total activity time, in seconds
- Steps - number of steps taken
- Calories - number of calories burned
- Minutes - actual number of minutes activity was performed (excludes time not moving?)
- Average Heart Rate - beats per minute (currently this always returns null)
- Minimum Heart Rate - beats per minute (currently this always returns null)
- Maximum Heart Rate - beats per minute (currently this always returns null)
- State - returns 'complete' if event was completed at time of export
- Version - API version used (i.e., 2)
- ID - internal id for given sleep event
