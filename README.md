# Hindustan-Unilever-BFS-Hackathon
This repository contains our approach to Hindustan Unilever BFS Hackathon help at Unilever Offices in Bangalore.There were 2 parts of the hackathon. The online part was held on skilleza and one needed to be in the top 50 to qualify for the onsite hackathon.
<p align="center">
<img width="1400" height="300" src="https://github.com/Sreyan88/Hindustan-Unilever-BFS-Hackathon/blob/master/Extra/HUL BFS.png">
</p>

There were a total of 6 problem statements.We were assigned problem statement 1. The description of the exact problem statement is given below.

### Preventing Revenue Leakage and datasets
HUL have 436 Lakme salons: company run salon or franchise salon. Revenue leakage happens from underbilling, wrong discounts, bypass system and double discounts or discounts to customers who are not eligible.
- Audit every single salon all through the year (manual bill book, card statement reconciling with bank, any appointments have been deleted, expired products and stock counting, etc.
- Power BI to throw outliers in certain matrix (eg if same service has been given to a customer in a single day, calling customer)

The actual problem statement had 3 parts to it:
1. Detect anomaly from sales data.
2. Detect under-usage and over-usage of material from inventory data.
3. Count footfall in a store from CCTV data.

## Important Disclaimer: The data has been not published. It has also been hidden from the code due to security concerns. The code just describes our methodology and can be used as an effective way for anomaly detection from sales data.
### Part 1 Solution:
The data hasn't been published or shown due to privacy issues. However the data can be thought of as row wise sales data where every row represented sale of a particular product or service with it's corresponding invoice number and other details about the sales such as price, date, etc.
The other dataset consisted of materials used for a corresponding service with its invoice number.
Steps followed:
1. Only individual rows corresponding to individual sales obviously wasn't enough to deetct anomaly. Therefore rigorous feature engineering was required. Features generally included aggregation of sale related features on invoice, date, store, etc.
2. Standardizing the data.
3. Dimesionality reduction using PCA (Numerical features and categorical features seperate).
4. Training Isolation Forest for anomaly detection. (DBSCAN was also tried but results were not good).
5. Training VAE to learn anomalies for deployment.

Below is a glimpse of how our model performed and visualization on 3 dimensions. Yellow signifies normal and brown signifies anomaly.

<p align="center">
<img width="480" height="270" src="https://github.com/Sreyan88/Hindustan-Unilever-BFS-Hackathon/blob/master/Extra/Anomaly Plot.png">
</p>

### Part 2 Solution:
Code for solution of part 2 wasn't included due to privacy issues. However, Part 2 was nothing special and just needed us to plot actual usage of inventory products and what should have been used according to the sales data to detect over-usage and under-usage of products and thereby detecting revenue leaks. We had about 5 datasets which included how much a particular store ordered a certain product and how much of a particular product should have been used for a particular service, etc. Additionally with the sales data from part 1,which had data about how many of a particular service was offered in a particular month, we just had to do some clever joining to get the desired plots.

### Part 3 Solution:
We used OpenCV to detect and count every person entering and leaving the store.(Only one counter was maintained for the total count).
Steps followed:
1. Detect every individual person using object detection and find out the centroids of the person.
2. We then assign an ID to each object with the help of its centriod and store it.The centroid tracking algorithm makes the assumption that pairs of centroids with minimum Euclidean distance between them must be the same object ID.
3. Make a vertical line near the door.
4. Count the person if it crosses the vertical line.

Below is the actual working implementation of our algorithm on a CCTV footage of an actual Lakme store provided to us in the competition.

<p align="center">
<img width="480" height="270" src="https://github.com/Sreyan88/Hindustan-Unilever-BFS-Hackathon/blob/master/Extra/In.gif">
</p>
<p align="center">
<img width="480" height="270" src="https://github.com/Sreyan88/Hindustan-Unilever-BFS-Hackathon/blob/master/Extra/Out.gif">
</p></br>

Our code is inspired from people counter implemented in pyimagesearch.

