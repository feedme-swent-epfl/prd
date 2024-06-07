# Functional Requirements

## Personalized feed recipe recommendations

**Why :**

The FeedMe app relies on a well-trained and accurate recommendation algorithm to incentivize users to return and consult their feed as they would for a social media application. This algorithm must be able to take into account a wide array of user preferences to curate the best recipe list for the user's feed.

**Implementation :**

We will use the Collaborative Filtering approach to design a recommendation algorithm fitting enough for our recipes. The proposition implies that we may have a lower relevance at first for our recommendations but that we will scale up as our user base grows.

We will collect a few statistics for each user including search history, saved recipes, rated recipes, created recipes' tags. Those statistics will be transformed to a probability map with each tag and ingredients, where the algorithm will determine the most probable tags and ingredients that the user will like. A score will also be computed that will be stored along other users' score to determine how alike each pair of users are. 

Finally, the algorithm will use the probability map as well as the similar users' saved and created recipes to give a list of recommended recipes that may please the user.

The Figure 2 in appendix represent the inputs and outputs of our algorithm.

## Recommending recipe depending on ingredients

**Why :**

The FeedMe app flagship functionality is the recommendation of recipes using only available inputted ingredients. Therefore, it is vital to design a pertinent algorithm that recommends those recipes, taking into account user preferences and ingredients, and which mode he chooses between strict (there needs to be an exact match) or extra (most ingredients of the user combined with other ingredients).

**Implementation :**

We need to first establish the difference between the strict and extra modes. 

The strict mode will simply go through all recipes and select the ones that match, before ordering them by most likely to less likely to be liked by the user (using the personnalized feed algorithm for ranking them).

The extra mode however will need to be a bit more elaborated, as we need to set a threshold for the ingredients differential : naturally, we should prefer recipes needing less ingredients than more. However, we should take into account the user preferences when performing such a choice, as users may prefer a recipe with more unavailable ingredients but more suited to their palates instead of a recipe missing only one ingredient but not to their liking.

Therefore, we propose to design a function that will begin by filtering all recipes using the available ingredients, with a margin of 2 ingredients available but not used. After this first filtering, we will assign points to each function that will increase the most matching ingredients and the less unavailable ones there are. Points will also be assigned using the recommendation algorithm and the most likely recipes to be appreciated by the user. 

Finally, we will compute an average of all values and rank the recipes using this order, ensuring that the recipes are displayed in a meaningful order.