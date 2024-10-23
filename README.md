# Reviews-of-UPI-Apps
Exploring User Feedback on UPI Apps in Google Play Store
# Project Overview

## Objective
The primary aim of this project is to analyze user reviews of digital payment apps (GPay, PhonePe, and Paytm) to derive insights into user satisfaction and areas for improvement. The analysis seeks to identify trends, common issues, and strengths of each app, ultimately providing recommendations for enhancing GPay's performance relative to its competitors.

## Dataset

### Description
The dataset consists of user reviews for three popular payment applications: GPay, PhonePe, and Paytm. The reviews include attributes such as user ratings, content of the review, user details, and timestamps.

## Schema

```sql
CREATE TABLE public.gpay_help (
    reviewid UUID PRIMARY KEY,
    username VARCHAR(255),
    userimage VARCHAR(255),
    content TEXT,
    score INT,
    thumbsUpCount INT,
    reviewCreatedVersion VARCHAR(50),
    at DATE,
    replyContent TEXT,
    repliedAt DATE,
    appVersion VARCHAR(50)
);

CREATE TABLE public.phonepe_help (
    reviewid UUID PRIMARY KEY,
    username VARCHAR(255),
    userimage VARCHAR(255),
    content TEXT,
    score INT,
    thumbsUpCount INT,
    reviewCreatedVersion VARCHAR(50),
    at DATE,
    replyContent TEXT,
    repliedAt DATE,
    appVersion VARCHAR(50)
);

CREATE TABLE public.paytm_help (
    reviewid UUID PRIMARY KEY,
    username VARCHAR(255),
    userimage VARCHAR(255),
    content TEXT,
    score INT,
    thumbsUpCount INT,
    reviewCreatedVersion VARCHAR(50),
    at DATE,
    replyContent TEXT,
    repliedAt DATE,
    appVersion VARCHAR(50)
);

```

## Business Problem

### Problem Statement
Despite the popularity of digital payment apps, user feedback reveals significant areas of concern, particularly for GPay. Understanding these concerns can lead to improved user satisfaction and retention.

## Analysis and Findings

1. **Review Counts**: Counted the total number of reviews for each app, indicating overall user engagement.
2. **Average Score**: Calculated the average scores to benchmark user satisfaction levels across the apps.
3. **Top Positive Reviews**: Identified the highest-rated reviews to understand what users appreciate about each app.
4. **Lowest Rated Reviews**: Analyzed the lowest-rated reviews to pinpoint common complaints and issues.
5. **Reviews with Replies**: Examined how many reviews received responses, which can indicate the app's customer support responsiveness.
6. **Reviews Over Time**: Analyzed trends in user feedback over time to identify patterns related to app updates or specific events.
7. **User Activity**: Identified the most active users across the platforms to understand user engagement.
8. **Sentiment Analysis**: Compared average scores of reviews with and without replies, providing insights into the effectiveness of customer service.
9. **App Performance**: Evaluated scores by app version to assess how updates impact user satisfaction.
   ## Analysis and Findings

### 1. Total Reviews for Each App
```sql
SELECT 
    COUNT(*) AS total_reviews, 
    'gpay' AS app_name 
FROM public.gpay_help 
UNION ALL 
SELECT 
    COUNT(*) AS total_reviews, 
    'paytm' AS app_name 
FROM public.paytm_help 
UNION ALL 
SELECT 
    COUNT(*) AS total_reviews, 
    'phonepe' AS app_name 
FROM public.phonepe_help;
```
### 2. Average Score for Each App
```sql
SELECT 
    AVG(score) AS average_score, 
    'gpay' AS app_name 
FROM public.gpay_help 
UNION ALL 
SELECT 
    AVG(score) AS average_score, 
    'paytm' AS app_name 
FROM public.paytm_help 
UNION ALL 
SELECT 
    AVG(score) AS average_score, 
    'phonepe' AS app_name 
FROM public.phonepe_help;
```
### 3. Top 5 Positive Reviews for Each App
```sql
SELECT * FROM (
    SELECT 
        reviewId, 
        content, 
        score, 
        'gpay' AS app_name 
    FROM public.gpay_help 
    ORDER BY score DESC 
    LIMIT 5
) AS gpay_reviews

UNION ALL 

SELECT * FROM (
    SELECT 
        reviewId, 
        content, 
        score, 
        'paytm' AS app_name 
    FROM public.paytm_help 
    ORDER BY score DESC 
    LIMIT 5
) AS paytm_reviews

UNION ALL 

SELECT * FROM (
    SELECT 
        reviewId, 
        content, 
        score, 
        'phonepe' AS app_name 
    FROM public.phonepe_help 
    ORDER BY score DESC 
    LIMIT 5
) AS phonepe_reviews;
```
### 4. Lowest Rated Reviews for Each App
```sql
SELECT * FROM (
    SELECT 
        reviewId, 
        content, 
        score, 
        'gpay' AS app_name 
    FROM public.gpay_help 
    ORDER BY score ASC 
    LIMIT 5
) AS gpay_reviews

UNION ALL 

SELECT * FROM (
    SELECT 
        reviewId, 
        content, 
        score, 
        'paytm' AS app_name 
    FROM public.paytm_help 
    ORDER BY score ASC 
    LIMIT 5
) AS paytm_reviews

UNION ALL 

SELECT * FROM (
    SELECT 
        reviewId, 
        content, 
        score, 
        'phonepe' AS app_name 
    FROM public.phonepe_help 
    ORDER BY score ASC 
    LIMIT 5
) AS phonepe_reviews;
```
### 5. Reviews with Replies Count for Each App

```sql
SELECT 
    COUNT(*) AS reviews_with_replies, 
    'gpay' AS app_name 
FROM public.gpay_help 
WHERE replyContent IS NOT NULL
UNION ALL 
SELECT 
    COUNT(*) AS reviews_with_replies, 
    'paytm' AS app_name 
FROM public.paytm_help 
WHERE replyContent IS NOT NULL
UNION ALL 
SELECT 
    COUNT(*) AS reviews_with_replies, 
    'phonepe' AS app_name 
FROM public.phonepe_help 
WHERE replyContent IS NOT NULL;
```
### 6. Reviews Over Time for GPay
```sql
SELECT 
    DATE_TRUNC('month', at) AS review_month, 
    COUNT(*) AS review_count 
FROM public.gpay_help 
GROUP BY review_month 
ORDER BY review_month;
```
### 7. Top 5 Users with Most Reviews
```sql
SELECT 
    userName, 
    COUNT(*) AS review_count 
FROM (
    SELECT userName FROM public.gpay_help
    UNION ALL 
    SELECT userName FROM public.paytm_help
    UNION ALL 
    SELECT userName FROM public.phonepe_help
) AS all_reviews 
GROUP BY userName 
ORDER BY review_count DESC 
LIMIT 5;
```
### 8. Average Score of Reviews with and without Replies for GPay
```sql
SELECT 
    AVG(score) AS average_score, 
    CASE 
        WHEN replyContent IS NOT NULL THEN 'With Reply' 
        ELSE 'Without Reply' 
    END AS reply_status 
FROM public.gpay_help 
GROUP BY reply_status;
```
### 9. App Performance by Version
```sql
SELECT 
    appVersion, 
    AVG(score) AS average_score, 
    'gpay' AS app_name 
FROM public.gpay_help 
GROUP BY appVersion 
UNION ALL 
SELECT 
    appVersion, 
    AVG(score) AS average_score, 
    'paytm' AS app_name 
FROM public.paytm_help 
GROUP BY appVersion 
UNION ALL 
SELECT 
    appVersion, 
    AVG(score) AS average_score, 
    'phonepe' AS app_name 
FROM public.phonepe_help 
GROUP BY appVersion;
```

## Recommendations

- **Enhance Customer Support**: Improve response times and quality of replies to user reviews.
- **Address Common Issues**: Focus on fixing frequent complaints highlighted in the lowest-rated reviews.
- **Leverage Positive Feedback**: Use insights from high-rated reviews to bolster marketing strategies.
- **Regular Updates**: Maintain a cycle of updates based on user feedback to ensure continuous improvement.
 
 ## Author : SRIDHAR

I am a self-taught data analyst currently honing my skills through YouTube tutorials and a Coursera course. In this project, I utilized data analysis techniques along with SQL, Python, and ChatGPT to enhance my understanding and capabilities in the field. I am also in my final year of pursuing a BCA degree through correspondence, which I expect to complete soon. This experience has significantly improved my skills, and I am actively seeking internship opportunities to further develop my expertise and gain practical experience in data analysis.
  

## Conclusion
This analysis provides a clear picture of how GPay compares to its competitors and highlights actionable areas for improvement. By focusing on user feedback and addressing concerns, GPay can enhance its user experience and better compete in the digital payment market.


