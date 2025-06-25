## British Airways Data Science Project
Scenario:
Lounge access is a key part of the premium travel experience, and understanding lounge demand is crucial for British Airways (BA) to maintain high standards while optimizing space and resources. As the airline plans for future operations at Heathrow Terminal 3, it’s important to anticipate demand across different types of lounge access, each associated with varying levels of customer loyalty and travel class.

As BA plans for the future, especially with changes in flying schedules and fleet strategy, it's important to forecast how many passengers will be eligible to use each lounge on a typical day. However, future schedules can be unpredictable, which means we need a modeling approach that is both flexible and scalable.

Job is to create a lookup table that BA can use to estimate lounge eligibility percentages across different flight groupings. This will allow the business to anticipate lounge demand without needing exact flight or aircraft details.

Critically thinking about how to group flights in a meaningful way—by time of day, route type, or regional destination, for example, and applying logical assumptions to estimate how many travelers fall into each lounge tier, is what is needed. These estimates will help the Airport Planning team better understand where lounge investments may be needed as operations evolve.

In short, the table and justification will help translate data into decisions—and ensure BA continues to deliver a seamless experience for its most valued customers.

Task:
1. Modeling lounge eligibility at Heathrow Terminal 3
 - Understanding lounge eligibility:
     To understand who is typically eligible for lounge access. Lounge eligibility is generally based on customer loyalty status and travel class, with different access tiers offering varying levels of amenities.

   British Airways Lounge Tiers at Terminal 3:
   |Tier|Lounge Name   |Access Eligibility                     |
   |----|--------------|---------------------------------------|
   |1   |Concorde Room |- First class customers                |
   |    |              |- BA premier cardholders               | 
   |    |              |- BA Gold Guest List members           |
   |2   |First Lounge  |- BA Gold Members                      |
   |3   |Club Lounge   |- BA Silver cardholders                |
   |    |              |- Club World (business class) customers|

  Lounge capacity planning depends on forecasting how many eligible passengers fall into each of these categories.

 - Creating Eligibility assumptions:
    Goal: To create a lookup table that estimates lounge eligibility using clear, scalable categories.

    Grouping flights - common groups include:
    1. Time of day - Early morning, mid - day, evening departures
    2. Type of route - Short haul vs. Long haul
    3. Region or destination group - Europe, North America, Asia etc.

    Assumptions:
    1. People with the following conditions could be given priority for lounge access overall:
       -  People with long hauls in their journey.
       -  People with farther destinations booked.
       -  People travelling at night.
    2. After these conditions the passengers could then be divided based on the type of ticket and membership they hold.

- Applying assumptions to a flight schedule:
  
  
  

