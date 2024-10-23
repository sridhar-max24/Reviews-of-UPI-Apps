# Reviews-of-UPI-Apps
Exploring User Feedback on UPI Apps in Google Play Store
# Project Overview

## Objective
The primary aim of this project is to analyze user reviews of digital payment apps (GPay, PhonePe, and Paytm) to derive insights into user satisfaction and areas for improvement. The analysis seeks to identify trends, common issues, and strengths of each app, ultimately providing recommendations for enhancing GPay's performance relative to its competitors.

## Dataset

### Description
The dataset consists of user reviews for three popular payment applications: GPay, PhonePe, and Paytm. The reviews include attributes such as user ratings, content of the review, user details, and timestamps.

### Schema
Each app's review data is structured as follows:
- **reviewid**: Unique identifier for each review (UUID).
- **username**: Name of the user who wrote the review (VARCHAR).
- **userimage**: URL or path to the user's image (VARCHAR).
- **content**: The text content of the review (TEXT).
- **score**: User rating (INT).
- **thumbsUpCount**: Number of thumbs up received (INT).
- **reviewCreatedVersion**: Version of the app when the review was created (VARCHAR).
- **at**: Date the review was written (DATE).
- **replyContent**: Content of any replies to the review (TEXT).
- **repliedAt**: Date when the reply was made (DATE).
- **appVersion**: Version of the app reviewed (VARCHAR).

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

## Recommendations

- **Enhance Customer Support**: Improve response times and quality of replies to user reviews.
- **Address Common Issues**: Focus on fixing frequent complaints highlighted in the lowest-rated reviews.
- **Leverage Positive Feedback**: Use insights from high-rated reviews to bolster marketing strategies.
- **Regular Updates**: Maintain a cycle of updates based on user feedback to ensure continuous improvement.

## Conclusion
This analysis provides a clear picture of how GPay compares to its competitors and highlights actionable areas for improvement. By focusing on user feedback and addressing concerns, GPay can enhance its user experience and better compete in the digital payment market.

## GitHub Structure

