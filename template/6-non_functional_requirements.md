# Non-Functional Requirements

## Security, privacy, and data retention policies

*Which are the applicable laws and regulations?*\
Our authentication services are done using Google Authentication. Since our servers won't be communicating with Google's servers on the user's behalf, we do not have to handle saving any user credentials on the backend (such as passwords or refresh tokens). We only need to make sure the users' email adresses are savely stored in our database.

*What are your internal policies?*\
In the eyes of our real customer, we should be viewed simply as an information facilitator. This means that we need to keep a strict and well-defined policy around what user data we retain. For example, in the context of generation of recipes, our app could be viewed as favoring some recipes over others if we collect and retain all reviews and user preferences to use in the recommendation algorithm. Therefore, we should define clear data retention policies, like anonimyzing reviews of recipes for training.

*Which privacy features do you need from the phone?*\
Our backend should be so designed that we should not save/extract or infer any personally identifiable information about a user, such as Name, Age, Gender, Address, etc. Moreover, our application should not be able to use the camera to extract sensitive information outside of what it can scan.

## Adoptions, Scalability and Availability

#### What kind of traffic patterns do you expect to see?
The MVP should be able to support traffic of generation of recipes that can happen at certain times of the day : 
- Noon: around lunch time, people are more prone to ponder about what to cook since it would be the first high-intake meal of the day.
- 7-9PM: around dinner time, people come home hungry after work / school and are more susceptible to cook a hearty meal, also enabeling them to keep some leftovers for next day's lunch. It would be important to choose the right meal, and thus a high traffic to get some inspiration on what to cook.
- The weekend: people have the most time to cook during the weekend since they are off work/school. This can cause more traffic in general, that is more spread out during the day since users' days are more flexible, causing a more random cooking time.

