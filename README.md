# Matchmaking in DB
This exercise consists of these steps:
* creating a schema that allows us to store user data and match users to each other
* ingesting data from the file [data.json](data.json)
* creating a stored procedure (generate_matches) that can be called on a periodic basis that will add 2 matches to every user every time it is called (in case there are no more matches available for a specific user, no action should be taken)
* creating a stored procedure (get_matches) that will return matches for a specific user based on their name
* creating a stored procedure (reject_match)that allows us to mark a match as rejected
   
## Input data
The input data is provided as a well structured JSON file that can be found in this repository.

The format of the data is as follows:
```json
{
  "display_name": "Sharon",
  "age": 47,
  "job_title": "Doctor",
  "height_in_cm": 161,
  "city": {
    "name": "Solihull",
    "lat": 52.412811,
    "lon": -1.778197
  },
  "main_photo": "http://thecatapi.com/api/images/get?format=src&type=gif",
  "pokemon_catch_rate": 0.97,
  "cats_owned": 0,
  "likes_cats": false,
  "religion": "Islam"
}
```

## Matchmaking algorithm
For the matchmaking algorithm the following conditions should apply:
* the maximum distance between two users should be adjustable (a parameter to the `generate_matches` stored procedure, or a configuration table)
* users should be matched within an age difference of 5 years inclusive
* users who have cats should not be matched to users who do not like cats
* pokemon_catch_rates:
    * difference should not be more than 30%
    * if the catch rate for a user is above 70% the difference should be less than 15%
* users with same religions should have a higher chance of getting matched with each other
* users with the same job should have a lower chance of getting matched to each other

These conditions are listed in order of importance, so if you cannot fulfill all of them, start with the ones on the top.
