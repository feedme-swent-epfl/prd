# Timeline/Resource Planning

The MVP development is planned to be executed over a 21-week time period. This includes setup, development, testing, rollout, and feature iteration to find product-market fit. We envision several intermediate milestones that will help us assess our progress with a team of 7 people that dabbled in several roles such as frontend development, backend development, UI/UX designing, and software testing.

Our schedule was seperated in 5 seperate milestones, each having a specific goal to help us work towards developing the best application possible.


## Development resouces

The primary cost of development of the product comes from developer cost. We estimate the need to secure 5 months of cash for a 7-person team to meet planned and unplanned scenarios. Realistically, this project would need 4 full-time developers (2 on frontend, 2 on backend+devops), along with 3 part time contractors for UI design and testing. 

We overprovision cash for a total of 7 person-months to meet unexpected deviations from our envisioned roadmap.

| **Function** | **Required person-months** |
| --- | --- |
| Frontend Kotlin/Jetpack Compose Developer | 10 |
| Backend Kotlin Developer | 5 |
| Backend Compose Multiplatform | 5 |
| UI/UX Designer | 5 |
| Software Tester | 3 |
| Surplus Cash Reserves | 7 |


## Execution Roadmap

### Milestone 1:
Infrastructure and design completion
- Development of wireflows and UI/UX using Figma
- Deciding on tools and infrastucture needed
- Development of the architecture diagram
- Development of data model
- Research on the migration Android <--> iOS

| **Sprint Number** | **Objective** | **Outcomes** |
| --- | --- | --- |
| Sprint 1 | Kickoff and Documentation| Deciding on tools and infrastructure to use, and Documentation of the migration Android <--> iOS |
| Sprint 2 | Design and Documentation | Initial wireframes, and user flows created, started UI mockups with UI elements for plugins. Documentation and prototyping iOS migration |
| Sprint 3 | Design Finalization & Application Skeleton | Finalized UI/UX designs, setup data model, and finalised first version of architecture diagram  |

### Milestone 2:

Core feature development
- Better integration of fridge button
- Work on the recommendation algorithm
- Work on ratings of recipes inside of the database
- Better setup of the database content (contents of the recipes, ingredients list...)
- Amelioration of the image, text and barcode recognition algorithms

| **Sprint Number** | **Objective** | **Outcomes** |
| --- | --- | --- |
| Sprint 4 | Fridge button | Better integration of the fridge button in the application, along with development of basic frontend-backend integration, began unit testing. |
| Sprint 5 | Recommendation algorithm and better setup of database content | Work on more cohesive recommendation algorithm for landing page and generation of recipes, fix the database content (recipe content, ingredients list), and continued integration and unit testing |
| Sprint 6 | Ratings of recipes & setup of database content | Work on ratings of recipes inside of the database, finish the polishing of database of recipes and ingredients. |
| Sprint 7 | Amelioration of recognition | Work on barcode, text and image recognition of ingredients, integrated all features in frontend, internal testing. |
| Sprint 8 | Unit and Integration Testing | Write all remaining unit tests, check frontend-backend integration with Integration tests. |


### Milestone 3:
Internal testing
- Check UI and UX of Compose Multiplatform
- Make sure that all camera features work
- Test extensively the recommendation algorithm
- Test extensively the generation of recipes algorithm

| **Sprint Number** | **Objective** | **Outcomes** |
| --- | --- | --- |
| Sprint 9 | Compose Multiplatform | Work on the compatibility of the application across multiple platforms |
| Sprint 10 | Camera features | End-to-end testing of the camera features, make sure they work on all possible platforms. |
| Sprint 11 | Recommendation algorithm testing | Extensively test the recommendation algorithm. |
| Sprint 12 | Generation of recipes algorithm testing | Extensively test the generation of recipes algorithm. |


### Milestone 4:
Beta and prelaunch
- Set up Google Analytics to track user events, setup analytics dashboard, and ensure correct tracking behavior.
- Firebase FCM for notifications
- Rollout app for beta testsers
- Fix bugs found in beta testing

| **Sprint Number** | **Objective** | **Outcomes** |
| --- | --- | --- |
| Sprint 13 | Internal Testing & Analytics/Monitoring pipelines | Thorough internal testing, load testing, feedback collection, bug fixing, performance testing |
| Sprint 14 | Pre-Launch Preparations | Final bug fixes and optimizations, prepared app store and launch materials. |
| Sprint 15-16 | Rollout application for beta testers | Make the application available for beta testers. Fix bugs when found using analytics and feedback |


### Milestone 5:
Rollout and feature iterations
- Rollout app for alpha testers on both android and IOS platforms

| **Sprint Number** | **Objective** | **Outcomes** |
| --- | --- | --- |
| Sprints 17-18 | Initial Rollout / Alpha Testing | Deployed app to production, monitored app performance, and gathered user analytics/insights and feedback. Active hotfixes as needed. |
| Sprint 19 | Feature Iteration 1 | Identifying drop-off points, optimizing user experience, rollout updates, improving UI, possibly |
| Sprint 20 | Beta Testing | Initiate marketing, getting users on the app, promptly addressing feedback to gain trust |
| Sprint 21 | Full Rollout | Press marketing pedals, offering incentives to join the app |

