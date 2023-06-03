# nosql-challenge
## NoSQL_setup_starter

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. 
You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to
help their journalists and food critics decide where to focus future articles.

## Part 1: Database and Jupyter Notebook Set Up
Import the data provided in the establishments.json file from your Terminal. Name the database uk_food and the collection establishments.
Within this markdown cell, copy the line of text you used to import the data from your Terminal. This way, future analysts will be able to repeat your process.

e.g.: Import the dataset with mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json

## Part 2 Update the Database

 a) An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following restaurant "Penang Flavours" to the database.
         
         Create a dictionary for the new restaurant data
          new_restaurant = {
              "BusinessName":"Penang Flavours",
              
              
 inserted the new restaurant into the collection and verified the addition.
 
 b) Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.
 
          query = {'BusinessType': 'Restaurant/Cafe/Canteen'}
          fields = {'BusinessTypeID','BusinessType'}
          establishments.find_one(query, fields)
          
          {'_id': ObjectId('64792219f2ad2ec137f7eec9'),
          'BusinessType': 'Restaurant/Cafe/Canteen',
          'BusinessTypeID': 1}
          
  c) Update the new restaurant with the BusinessTypeID you found.
        
        establishments.find_one({'BusinessName':'Penang Flavours'})
        {'_id': ObjectId('6479221e5a2adec257765c4f'),
          'BusinessName': 'Penang Flavours',
          'BusinessType': 'Restaurant/Cafe/Canteen',
          'BusinessTypeID': '',
          
  d) The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Then, remove any establishments      within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.
  
    How many documents contain the Dover Local Authority?
      Number of localAuthorityName by Dover:  994
   
   Deleted all documents where where LocalAuthorityName is "Dover"
        
        establishments.delete_many(query)
   
   check that other documents remain with 'find_one'

        establishments.find_one()
        
  e) Some of the number values are stored as strings, when they should be stored as numbers.
      Use update_many to convert latitude and longitude to decimal numbers.
          
      Change the data type from String to Decimal for longitude and latitude
            
         establishments.update_many({}, [{'$set': {'geocode.longitude': {'$toDecimal': '$geocode.longitude'}, 
                                         'geocode.latitude': {'$toDecimal': '$geocode.latitude'}
                                         }
                                }
                               ]
                          )
   f) Use update_many to convert RatingValue to integer numbers and used pprint.
   
          pprint(establishments.find_one({}, {"geocode", "RatingValue"}))
          
          
 ## Part 3: Exploratory Analysis
 
 Which establishments have a hygiene score equal to 20?

  There are 41 establishments with a hygiene score of 20 from the uk_food dataset.

Which establishments in London have a RatingValue greater than or equal to 4?

  There are 33 establishments in London that have a RatingValue greater than or equal to 4 from the uk_food dataset.

What are the top 5 establishments with a RatingValue rating value of '5', sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

  The top 5 establishments with a RatingValue of '5' sorted by lowest hygiene score nearest to "Penang Flavours" are: "Volunteer", "Plumstead Manor Nursery",       "TIWA N TIWA African Restaurant Ltd", "Iceland", and "Howe and Co Fish and Chips - Van 17".

How many establishments in each Local Authority area have a hygiene score of 0?

  There are 55 rows in the DataFrame. 
  
  This is the preview of the first 5 rows:
      
   ![image](https://github.com/mcaro01/nosql-challenge/assets/125619215/a0994d4c-ce3c-4746-ab81-8b81a169f822)

 
 
## Please Note:
## In order to display the correct data I have to run the dataset "mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json" in the terminal every time I run the first part (NoSQL_setup_starter) of this challenge 
      How many documents contain the Dover Local Authority?
        Number of localAuthorityName by Dover:  994
