# Hindustan-Unilever-BFS-Hackathon
This repository contains our approach to Hindustan Unilever BFS Hackathon help at Unilever Offices in Bangalore.

We were assigned problem statement 1. The description of the exact problem statement is given below.

### Preventing Revenue Leakage and datasets
HUL have 436 Lakme salons: company run salon or franchise salon. Revenue leakage happens from underbilling, wrong discounts, bypass system and double discounts or discounts to customers who are not eligible.
- Audit every single salon all through the year (manual bill book, card statement reconciling with bank, any appointments have been deleted, expired products and stock counting, etc.
- Power BI to throw outliers in certain matrix (eg if same service has been given to a customer in a single day, calling customer)

The actual problem statement had 3 parts to it:
1. Detect anomaly from sales data.
2. Detect under-usage and over-usage of material from inventory data.
3. Count footfall in a store from CCTV data.

## Important Disclaimer: The data has been not published. It has also been hidden from the code due to security concerns. The code just describes our methodology and can be used as an effective way for anomaly detection from sales data.

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
