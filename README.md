# Project

* This is a dataset that is about a list of categorised meteorites. 

* Firstly, as with any new dataset, it is important to get an idea of the data you are working with, column types, how much cleaning of the data will be required, etc...

* After reading in the data, I ran some code that gathers the structure, and then also took a section from the top 20 observations. 

str(meteorite_landings)

head(meteorite_landings, 20)

* The next step is to initialise in cleaning the data.

* First changing the variable names 

renamed_meteorite <- meteorite_landings %>%
  rename(
    meteorite_id = id,
    meteorite_name = name,
    mass_in_grams = 'mass (g)',
    geo_location = GeoLocation
  )

* Next separating the column GeoLocation into two (latitude and longitude).

meteorite_wider <- renamed_meteorite %>%
  separate(geo_location, c("latitude", "longitude"), sep = ",")

head(meteorite_wider)

* After separating into latitude and longitude, I cleaned up the data in these two variables, firstly by removing uneccessary brackets.

remove_meteorite <- meteorite_wider %>%
  mutate(latitude = str_remove_all(latitude, "\\(")) %>%
  mutate(longitude = str_remove_all(longitude, "\\)"))

remove_meteorite

* And removing NA values from the two columns and replacing them with the value 0 

zero_meteorite <- remove_meteorite %>%
  replace_na(list(latitude = 0, longitude = 0))
zero_meteorite

* Next we wanted to filter the data to only show meteorites over 1000g and save it to a new object.

thousand_meteorite <- zero_meteorite %>%
  filter(mass_in_grams > 1000)
thousand_meteorite



* The next stage of this project is to take this cleaned up tibble and gather some information.

* First 