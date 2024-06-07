# Design and Implementation

## Frontend

We will use Kotlin to develop our app using the Model-View-ViewModel (MVVM) architecture, that we will build using Gradle. We decided to use Kotlin for two main reasons : it is particularly well-suited to Android app development, but also it has a very interesting technology named Kotlin Multiplatform. This technology allows developers to write shared common code between the Android and iOS apps while customizing each to its host system specifications. Furthermore, one can also write common shared UI with Compose Multiplatform.

We will use Kotlin only for the Model and ViewModel components, and we will write our UI using the Jetpack Compose framework for Android, and if we are not satisfied with the Compose Multiplatform framework we might also design a UI from scratch using SwiftUI for the iOS app. We will carefully code our app to take into account different screen sizes for each screen and making it robust enough to withstand different display configurations and adaptive changes to any logic change in our code logic.

## Backend

*Decompose the MVP into functional blocks.*

## Data Model

*What data are you collecting / managing?*

*How is it organised?*

*Where is it stored?*

*How is it shared/copied/cached?*

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