# Articles-RecSys

## Objective and metric::

Working with the logs of the recommender system, where users are given their sessions - the documents that were shown to them, and the reaction to them (click or lack thereof). Also, for each document, its title, content and already prepared embedding for a picture from it are known. For each user, a test set of documents is given - you need to predict for each of them whether a click will be made or not.

The quality of the recommendations is assessed by NDCG @ 20.

## Data Description:

To download the data: kaggle competitions download -c recsys-iad-challenge

tems.json:

itemId - ID of publication
title - title of text
content - content of text
image - CNN embedding image (vector)

Example:

{"content": "Согласитесь...", "itemId": 0, "image": [-0.169, ...], "title": "Пять..."} {"content": " Контуры...", "itemId": 1, "image": [-0.158, ...], "title": "История..."}

train.json:

userId
trainRatings - dictionary with estimates like {itemId: 1 if click, 0 otherwise}; a score of 0 means that the user was shown the given document, but there was no click.

## Model and features:

In fact, despite the complexity of the task at first glance, lightfm showed a decent quality of the model (https://making.lyst.com/lightfm/docs/home.html). Previously, the text (titles and content) were vectorized using TfidfVectorizer. It is interesting to note that pictures only slightly affected the quality, while the training time for the model increased significantly. The model was trained in google colab with a time limit of 12 hours, so when choosing a larger number of epochs vs adding pictures to the model, the first option won. Another interesting point was the memory problem, for which the sparse matrix was used. So, despite a seemingly small laptop with lightfm out of the box, it took a long time to sort out the memory and timing issues.

The final quality is about 0.2 - a relatively decent result.
