# Functional Requirements

## Personalized feed recipe recommendations

**Why :**

The FeedMe app relies on a well-trained and accurate recommendation algorithm to incentivize users to return and consult their feed as they would for a social media application. This algorithm must be able to take into account a wide array of user preferences to curate the best recipe list for the user's feed.

**Implementation :**

We will use the Collaborative Filtering approach to design a recommendation algorithm fitting enough for our recipes. The proposition implies that we may have a lower relevance at first for our recommendations but that we will scale up as our user base grows.

We will collect a few statistics for each user including search history, saved recipes, rated recipes, created recipes' tags. Those statistics will be transformed to a probability map with each tag and ingredients, where the algorithm will determine the most probable tags and ingredients that the user will like. A score will also be computed that will be stored along other users' score to determine how alike each pair of users are. 

Finally, the algorithm will use the probability map as well as the similar users' saved and created recipes to give a list of recommended recipes that may please the user.

The Figure 2 in appendix represent the inputs and outpur of our algorithm.

## Recommending recipe depending on ingredients

**Why :**

The FeedMe app flagship functionality is the recommendation of recipes using only available inputted ingredients. Therefore, it is vital to design a pertinent algorithm that recommends those recipes

**Implementation :**

We will implement 