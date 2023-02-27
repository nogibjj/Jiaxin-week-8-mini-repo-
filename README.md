# Jiaxin-week-8-mini-repo-

This is a description of a weather forecast module for Polybar that requires the Weather Icons and Material Icons fonts to work properly. 
<img width="497" alt="Screen Shot 2023-02-27 at 3 58 42 PM" src="https://user-images.githubusercontent.com/112274822/221684205-c162bfdb-f65e-4a5d-ba5a-4a756131c58b.png">

## Create a weather forecast module for Polybar
Here are the steps to use this module:

1. Install the Weather Icons and Material Icons fonts: You need to download and install the Weather Icons and Material Icons fonts in your system. These fonts are usually available in the official package repositories of most Linux distributions. Alternatively, you can download the fonts from the official websites and install them manually.

2. Write a script to fetch weather data: Write a script that fetches weather data from a weather API, such as OpenWeatherMap or Weather Underground. The script should parse the data and extract the information you need, such as current temperature and forecast data.

3. Write a script to format the output: Once you have the weather data, you need to format it for display in Polybar. You can use a scripting language such as Python or Bash to format the output. The output should contain the current temperature and the 3-hour forecast, along with the appropriate weather icons from the Weather Icons font.

4. Configure the Polybar module: Finally, you need to configure the Polybar module to use the weather script you created. You can do this by adding a new module to your Polybar configuration file, specifying the script and the output format.

Here's an example of what the Polybar configuration file might look like:
```
[module/weather]
type = custom/script
exec = /path/to/weather_script.sh
interval = 600
format = <label>
label-font = 2

[bar/top]
modules-left = weather
```
Replace "/path/to/weather_script.sh" with the actual path to the weather script you created. The "interval" option sets the update interval to 600 seconds (10 minutes). The "format" option specifies the output format using Handlebars syntax. Replace "<label>" with the actual label you want to display, which should contain the formatted weather data. The "label-font" option sets the font index for the label to 2, which corresponds to the Weather Icons font.

Finally, the "modules-left" option specifies the modules that should be displayed on the left side of the Polybar. In this example, only the "weather" module is displayed.

## An example TOML configuration file
```
# Register at https://openweathermap.org to get your API key
# If you don't want to write your key here, you can delete this line and use the OWM_API_KEY environment variable instead
api_key = "YOUR_API_KEY"

# This is for Montreal, find your city at https://openweathermap.org
# The id will be the last part of the URL
city_id = "6077243"

# Output format, using Handlebars syntax, meaning variables should be used like {{ this }}
# Available tokens are:
# - temp_celcius
# - temp_kelvin
# - temp_fahrenheit
# - temp_icon
# - trend
# - forecast_celcius
# - forecast_kelvin
# - forecast_fahrenheit
# - forecast_icon
display = "{{ temp_icon }} {{ temp_celcius }}°C {{ trend }} {{ forecast_icon }} {{ forecast_celcius }}°C"
```

Above is a Python script for fetching weather data from the OpenWeatherMap API and formatting the output for display in Polybar. Here are the steps to use this script:

1. Sign up for an OpenWeatherMap API key: You need to create an account on the OpenWeatherMap website and obtain an API key. This key will be used to authenticate your requests to the API.

2. Replace "YOUR_API_KEY" with your actual API key: In the first line of the script, replace "YOUR_API_KEY" with the API key you obtained in step 1. Alternatively, you can set the OWM_API_KEY environment variable to your API key, and the script will automatically pick it up.

3. Set your city ID: In the second line of the script, replace "6077243" with the ID of your city. You can find your city ID by searching for your city on the OpenWeatherMap website and looking at the URL.

4. Customize the output format: In the third line of the script, you can customize the output format to your liking using Handlebars syntax. The available tokens are listed in the comment.

5. Run the script: Save the script to a file with a ".py" extension, and run it using the Python interpreter. The script should output the weather data in the format specified in the "display" variable.

6. Integrate the script with Polybar: Finally, you need to integrate the script with Polybar. You can do this by adding a new module to your Polybar configuration file, specifying the path to the script and the output format. For example:
```
[module/weather]
type = custom/script
exec = python /path/to/weather_script.py
interval = 300
format = <label>
```
Replace "/path/to/weather_script.py" with the actual path to the script, and "<label>" with the Handlebars syntax for the label you want to display.

## Install polybar-forecast 
Instructions for building and installing the polybar-forecast binary for Polybar. Here are the steps to use this binary:

1. Download the pre-built binary or build it from source: If you want to use the pre-built binary, download it from the release page and make it executable by running "chmod +x polybar-forecast". If you want to build it from source, run "cargo build --release" in the project directory. This will generate a binary file named "polybar-forecast" in the "target/release" directory.

2. Copy the binary to your desired location: You can copy the "polybar-forecast" binary to any directory you want. It is recommended to place it in a directory that is included in your system's PATH variable.

3. Create a configuration file: Create a configuration file named "config.toml" in either the same directory as the binary or in "$HOME/.config/polybar-forecast/". The configuration file should contain the necessary options for the binary to work, such as the API key, city ID, and output format.

4. Add a module to your Polybar configuration file: Finally, add a new module to your Polybar configuration file that points to the "polybar-forecast" binary and specifies the path to the configuration file. For example:
```
[module/weather]
type = custom/script
exec = /path/to/polybar-forecast -c /path/to/config.toml
interval = 300
format = <label>
```
Replace "/path/to/polybar-forecast" with the actual path to the "polybar-forecast" binary, and "/path/to/config.toml" with the actual path to the configuration file. Also, replace "<label>" with the Handlebars syntax for the label you want to display.
  
## Creating a new weather module
These are instructions for creating a new weather module in Polybar using the polybar-forecast binary. Here are the steps to use this module:

1. Install polybar-forecast: Follow the instructions in my previous response to build or download the polybar-forecast binary and place it in a directory that is included in your system's PATH variable.

2. Configure the weather module: Create a new module in your Polybar configuration file named "weather" with the following options:
```
[module/weather]
type = custom/script
exec = /path/to/polybar-forecast
exec-if = ping openweathermap.org -c 1
interval = 600
label-font = 3
```
Replace "/path/to/polybar-forecast" with the actual path to the "polybar-forecast" binary. The "exec-if" option makes sure that the module only runs if there is an internet connection. The "interval" option sets the update interval to 600 seconds (10 minutes). The "label-font" option sets the font size for the label to 3.

3. Add the Weather Icons font: Make sure to add the Weather Icons font to your Polybar configuration file, otherwise the weather icons will not render correctly. You can add the font using the "font-X" option, where X is a number that corresponds to the font index. For example:
```
font-2 = Weather Icons:size=12;0
```
This sets the second font to the Weather Icons font with a size of 12.

4. Add the weather module to your Polybar: Finally, add the "weather" module to your Polybar configuration file. For example:
```
modules-left = date time weather
```
This adds the "weather" module to the left side of the Polybar, along with the "date" and "time" modules.

**Reference**: 
https://forum.archlabslinux.com/t/polybar-weather/1357/8

https://github.com/kamek-pf/polybar-forecast
