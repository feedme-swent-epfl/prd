# Design and Implementation

## Frontend

We will use Kotlin to develop our app using the Model-View-ViewModel (MVVM) architecture, that we will build using Gradle. We decided to use Kotlin for two main reasons : it is particularly well-suited to Android app development, but also it has a very interesting technology named Kotlin Multiplatform. This technology allows developers to write shared common code between the Android and iOS apps while customizing each to its host system specifications. Furthermore, one can also write common shared UI with Compose Multiplatform.

We will use Kotlin only for the Model and ViewModel components, and we will write our UI using the Jetpack Compose framework for Android, and if we are not satisfied with the Compose Multiplatform framework we might also design a UI from scratch using SwiftUI for the iOS app. We will carefully code our app to take into account different screen sizes for each screen and making it robust enough to withstand different display configurations and adaptive changes to any logic change in our code logic.

## Backend

As mentioned during the frontend presentation, we will implement our application logic using Kotlin, which will handle among other things all transactions with our Firebase Firestore and Database. 

Kotlin will also be used to implement the control logic of our application and thus form the skeleton of our application. We will need to handle timely updates of the cache of the application with the most up-to-date database, and we will need to be extra careful when writing synchronization primitives using Kotlin coroutines to avoid a spinlock that doesn't return or data corruption in out database due to a change occuring by two parties at the same time. 

We will use data scraping to find new recipes and add them to our database. This will be primary used during the MVP development phase to repopulate our database and improve the quality of our recipes. We will use Python and more specifically Jupyter Notebook to handle the scrapping and filtering of the data collected. We will have multiple filtering scripts that will accommodate a number of different recipes format as input and will normalize them to fit well in our database.

## Data Model

We will need to collect and use a wide range of data for our app to function properly. We will need to juggle between the profiles, the recipes, the comments, and the ingredients data. 

We will use the Firestore Database to store the relevant data using NoSQL. Each component will be stored as a document with the relevant attributes, and we will use the Firebase Realtime Database to store any external media that will need to be linked in the document page. 

Below will be an exhaustive overview of the different repositories, components, and attributes, along with some specifications. Also, a diagram is available in the appendix (Figure 1) showing how each data class is linked with the others.

### Recipe

**Purpose** Contains information about various recipes.

**Fields**

- recipeId (Primary Key): Unique identifier for the recipe.
- title: Title of the recipe.
- description: Description of the recipe for the thumbnail.
- ingredients: List of ingredients with quantity and measure (references IngredientMetaData).
- steps: List of steps to prepare the recipe (references Step).
- tags: List of tags for the recipe.
- rating: Rating of the recipe.
- userid: User id of the recipe creator.
- imageUrl: Image URL of the recipe.
- searchItems: List of search items for the recipe.
- comments: List of comments for the recipe.

**Notes**
Aimed at providing detailed and structured information about recipes, including ingredients, preparation steps, and user interactions like ratings and comments.

### Step

**Purpose** 
Contains information about individual steps in the recipe.

**Fields**

- stepNumber: Order of the step in the preparation process.
- description: Description of the step.
- title: Title of the step.

**Notes**
Aimed at providing clear and sequential instructions for preparing the recipe.

### IngredientMetaData

**Purpose** 
Contains detailed information about the ingredients used in recipes.

**Fields**

- quantity: Quantity of the ingredient.
- measure: Measure unit of the ingredient (references MeasureUnit).
- ingredient: Ingredient object.

**Notes**
Aimed at providing precise information about the ingredients required for the recipe.

### Ingredient

**Purpose** 
Contains detailed information about individual ingredients used in recipes.

**Fields**

- name: Name of the ingredient.
- id: Unique identifier for the ingredient.
- vegan: Boolean indicating if the ingredient is vegan.
- vegetarian: Boolean indicating if the ingredient is vegetarian.

**Notes**
Aimed at providing comprehensive information about ingredients, including their dietary properties, to help users make informed choices when selecting or creating recipes.

### Comment

**Purpose** 
Contains information about user comments on recipes.

**Fields**

- commentId: Unique identifier for the comment.
- userId: User ID of the person who made the comment.
- recipeId: Recipe ID to which the comment belongs.
- photoURL: URL of the photo associated with the comment.
- rating: Rating given to the recipe.
- title: Title of the comment.
- content: Content of the comment.
- creationDate: Date when the comment was created.

**Notes** 
Aimed at providing feedback and reviews on recipes, allowing users to share their experiences and rate recipes.

### Profile

**Purpose** 
Manages detailed user-specific data and interactions within the platform, focusing on user profiles, preferences, and activity.

**Fields**

- id: Unique identifier for the user profile.
- name: Name of the user.
- username: Username of the user.
- email: Email address of the user.
- description: Bio or description of the user.
- imageUrl: URL of the user's profile image.
- followers: List of user IDs following this user.
- following: List of user IDs this user is following.
- filter: List of allergy settings or other user preferences.
- recipeList: List of recipe IDs created by the user.
- savedRecipes: List of recipe IDs saved by the user.
- commentList: List of comment IDs made by the user.

**Notes**
This model ensures that user data is managed with a focus on privacy and user preferences, allowing for a personalized experience while maintaining security and anonymity.

Most of this data is cached at the application level for access during offline mode, especially all saved components by the profile. The database will also be replicated on local media to avoid loss of data and/or for recovery in case of data corruption for example.

## Security Considerations

Firebase handles all security considerations regarding the authentication, with its seamless integration with other sign-in providers. We currently use Google as our primary authentication means, which uses the Google ID Token to check if the user possesses an account on our app, and if not creates another account.

The communication with the Firestore database is established over the HTTP/2 protocol, which is secure for information exchange and possesses the TLS protocol for network communications.

## Infrastructure and Deployment

We will continue using Firebase Firestore and Realtime Database to store our data. We expect to remain on the free plan for as long as possible before moving to a paid plan to accomodate more calls to the databases. We estimate that for the beta testing phase of our app and the first two months, we will have at most 3000 registered users, with approximately a third of these users being DAU. Taking that into account and supposing an underestimation on our part concerning the DAU, we will have for 1250 users approximately 40 read calls per day, which is more than enough per our estimation for regular use of our application with all user flows, which we don't expect every user to do. We will however need to scale up our API calls as soon as the threshold of 1000 DAU is reached to avoid exhausting our API calls.

We also plan on hosting our recommendation algorithm and the recognition modules algorithms on one of our server units. This will allow to avoid any failure or limitation incurred by the host machine and provide users a consistent experience with these modules accross all devices.

Finally, we plan to have local copies in our server of our Firebase and Firestore databases in case any failure or corruption by a write access is done, that we plan to do at 3 to 4 hours intervals.

## Test Plan

We plan to pursue testing regularly our application using Github Actions workflows to identify early on any possible error or bug that needs to be addressed before pushing our code to our main branch, that should ideally always remain bug-free. However, we will be more exhaustive in our checks and we plan on configuring multiple pipelines instead on having only one containing all our tests. This will help us to identify better and faster where our issue might be and will also help us avoid a very long waiting time during our CI runs and optimize waiting times by re-running failed jobs only.

We plan on testing the frontend using the  AndroidJUnitRunner test runner and the mockk library to check the correct display of information on the screen, and we will implement backend testing by performing resource injection in our pipelines to test our API calls to the ML kit libraries for example or the correct functionality of some ViewModel elements. 

Another important element we need to test thoroughly is the recommendation algorithm. We plan on having multiple iterations of the algorithm with different values and parameters to achieve the best results possible. The plan will be to plot the values used, execution time, and any other relevant data, obtained on a given database of recipes and a user with a given profile.

Finally, we plan on implementing multiple end-to-end tests focusing on all of the main user flows, that will test the navigation paths inside our apps, the frontend display and the backend functionality.

As our app will near completion, we will also perform load testing at expected peak traffic hours to monitor the number of crashes and bugs, so we can address them before the beta etsting phase of our app.
