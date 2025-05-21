# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
The scope of this project was to demonstrate the ability to apply statistical modelling techniques using Python. This was done by demonstrating proficent use of APIs to acquire data, parsing the data into a workable database, using SQL (within Python) to clean/manipulate the data, and finally generate a statistical model of the data in Python to draw analytical conclusions from. By doing so, this would produce a project wherein different aspects of the data statistical analysis pipeline would be exhibited over the process of each section.

## Process
### Part 1: CityBikes API
The first part of this project works with the CityBikes API to demonstrate the ability to retrieve data and parse the desired information into a Pandas DataFrame. The corresponding script can be found in the "notebooks" folder of this repo under the file name ["city_bikes_completed.ipynb"](https://github.com/Jtng647/LHL-DAFlx-Python-Proj2025/blob/main/notebooks/city_bikes_completed.ipynb).

#### Step 1:
The CityBike API was explored to understand its structure and the syntaxt for sending requests to it. Once this was done, a Python script to retrieve said data for the city of Osaka, Japan (city of choice) was written using the Python API commands. This data was then stored in a JSON. Of note, since the city of Osaka has multiple Bike Share networks, the Docomo Bike Share network was chosen as the representative network for Osaka.

#### Step 2:
To demonstrate the ability to parse the data, the information from the JSON in Step 1 was parsed using the .append loop to add the corresponding dictionary value to the list, to the corresponding heading (for name, latitude, longitude, bikes available).

#### Step 3:
Finally, the parsed data was put into a Pandas DataFrame, using the "json_normalize" function to flatten the data into a nicer table to work with in the future. An additional print output was also implemented to preview a sample of the data.

#### Step 4 (Optional):
An "optional" section to download/save the data as a JSON/CSV into a stored local file was added. This is especially useful for the purposes of this project as it will mean not having to send multiple pull requests each time the script is run in the future, when performing analytical functions. The data can then be analyzed (cleaned, manipulated, etc.) as a "snapshot" of when the initial retrieve request was sent. It can be commented out or skipped (if running in a notebook). Please see the files in the directory path Data > Part 1 > osaka_docomo_stations.json and osaka_docomo_stations.csv for these output date files.

### Part 2: Foursquare and Yelp APIs
The second part of this project is similar to the first in that it requires retrieving information from an API, except this time it will demonstrate retrieving data from 2 separate APIs: Foursquare and Yelp. The corresponding script can be found in the "notebooks" folder of this repo under the file name ["yelp_foursquare_EDA_completed.ipynb"](https://github.com/Jtng647/LHL-DAFlx-Python-Proj2025/blob/main/notebooks/yelp_foursquare_EDA_completed.ipynb).

#### Step 1:
First, we establish the imports that will be required for this envrironment for our purposes. The libraries "OS", "requests", "pandas", and "json" are all imported here. We then also establish the environmental variables - in this case, API keys - that will be used to call the APIs for data. Finally, the JSON from Part 1 - "osaka_docomo_stations.json" (seen in the "data" directory of this repo) is loaded into the processing environment so that the bike station coordinates can be pulled in the API calls.

***PLEASE NOTE*** - Unfortunately my account application with Foursquare has been stuck in "processing and review". As such I was unable to generate an API key as the Foursquare platform prevents any such requests until the application has been approved. The intended Python script, had the Foursquare API key been accessible is still included. But do note that no calls were made or data able to be retrieved as a result of not having an API key. This has been communicated with a mentor over Assistance Request and has been noted withe Student Success Coordinator team.

#### Step 2:
Secondly, the actual calls to the APIs are sent. While the structure between Foursquare and Yelp APIs differ slightly, both require the standard call to the appropriate endpoints for the data to be retireved. (The following applies to both APIs.) By using the Latitude and Longitude values from Part 1, POIs of the requested categories (restaurants and bars) can be called withing the 1000m radius parameter. At this point - for the purposes of this project - a limit of the first 10 listings is added on to prevent exceeding call limits to the APIs, and to make for a more mangeable dataset for our purposes. However, should the datapool need to be expanded, this parameter in the script can be adjusted accordingly (or even removed).

#### Step 3:
Once the data has been retrieved, we then parse the data for the specific information we need (in practice of DATA WRANGLING). The venue name, corresponding bike station name, venue category, lat & long for the location, address, and rating. These results are then parsed into a DataFrame for future analysis.

#### Step 4 (Optional):
Similar to in Part 1, the resulting DataFrame can be exported as JSON and CSV for ease of perusal, and also use in later analysis.

### Part 3: Joining the Data
The third part of this project requires taking the data from Part 1 & 2, and joining them together to create a new DataFrame and to visualize it to explore the data. A custom database can be created at this point as well for processing and analysis use later. The corresponding script can be found in the "notebooks" folder of this repo under the file named ["joining_data_completed.ipynb"](https://github.com/Jtng647/LHL-DAFlx-Python-Proj2025/blob/main/notebooks/joining_data_completed.ipynb).

#### Step 1:
The data from PArt 1 & 2 are joined together to form it's own DataFrame. The "Station Name" column of data is used as the primary key for both as it is the data that is present in both sets of data.

#### Step 2:
Applying the Exploratory Data Analysis (EDA) process, the data (which was already cleaned in the previous section) was applied to generating graphical vizualiations of different relationships between the data for analysis. The Matplotlib and Seaborn libraries were used to do so.

#### Step 3:
The data was then used to create our very own SQLite database via SQLite3 in Python. The 2 dataframes became their own tables in the database. Both sets of data were then validated by being queried and JOINed to ensure the data would output and could be manipulated as expected.

### Part 4: Building a Model
The fourth part of this project is to take the data and analyze it using statistical methods and analysis. Namely a regression model to grade and interpret correlation between the number of bikes at a station and the characteristics of the restaurants in that location. In this case, the restaurants rating was used. The corresponding script can be found in the "notebooks" folder of this repo under the file named ["model_building_completed.ipynb"](https://github.com/Jtng647/LHL-DAFlx-Python-Proj2025/blob/main/notebooks/model_building_completed.ipynb).

#### Step 1:
A regression model was built using the statsmodels/api library in Python. Using the joined DataFrame created in Part 3, it was loaded into the model with the Number of Bikes ("free_bikes") data as the Dependent Variable, and the Restaurant Ratings ("venue_rating") data as the Independent Variable.

#### Step 2:
The regression output was presented and an interpretation of the values was done. It would seem in this case that the correlation of these 2 variables was not quite definitive of much correlation. However, it is good to note that all the key values (R-Squared, P-Value, and Coeff.) pointed towards the same conclusion.

#### Step 3 (Stretch):
An additional stretch goal was considered with the purpose of transforming this regression model into a classification model. The key difference between the two was highlighted: to ensure that the Number of Bikes variable would be used to define DISCRETE categories to be used as the variable. A rough approach was outlined to this idea as well.

## Results
The final result of this project proved that there are indeed various sections, methods, and techniques that need to be applied to be able to demonstrate statistical analysis of data with visualization in Python. From the collection of data, to the EDA process to clean, manipulate, analyze and interpret it, to applying that processed data into a statistical regression model, all forms a lengthy pipeline.

Nevertheless it would seem that based on the results of that final model, the comparative quality of the API coverage in the chosen area of Osaka, Japan, was of poor quality. At the very least, the data and correlation that was used would seem to suggest so. While the APIs and the data obtained were valid, the efficacy of some sort of relationship between the number of bikes at a station and the ratings of the restaurants in their vicinity was not evident.

## Challenges 
Some challenges that were encountered in the process of this project were:

- The calling of APIs - Most APIs require a paid subscription as a service, or were very limited in the number of calls that could be done in a set period of time. This limited opportunities to test and experiment with what sort of calls and data could be pulled. Case in point - the Foursquare API could not even be called in this instance as their API Key would only be accessible to applicants who have had their request submissions reviewed and approved (of which mine is still pending).

- The right characteristic to choose for correlation - While the Yelp (and Foursquare) APIs provided a variety of characteristics of the restaurants in the vicintiy, none of them seemed quite right to correlate with the number of bikes. This is related to the next challenge as well.

- Assumptions in the presented scenario - Many assumptions had to be made about this scenario whereing there may be a correlation between the number of bikes and the restaurants/venues/POIs within a 1 km radius from the bike stations. There are too many unaccountable factors as to why bikes may be at that station. We had to assume a "vacuum" scenario where the main/only mode of transportation would be the bikes, ignoring all other modes of transporation and other motivations. (Such as convenience, place of employment, combination with other modes of transportation, etc.)

## Future Goals
If there was more time (and more calls available to the APIs) there could be a more extensive correlation model analysis for the other characteristics of the restaurants around the bike stations. More time with the data would allow for more considerations and combinations of the variables to model and draw interpretations from.
