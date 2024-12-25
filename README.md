# MongoDB Aggregation Pipeline Bug
This repository demonstrates a common error in MongoDB aggregation pipelines: using the `$limit` stage after a `$group` stage that produces a large number of groups. This can lead to unexpected and incorrect results because `$limit` operates on the stream of documents before they are fully processed.

## Bug Description
The provided JavaScript code shows an aggregation pipeline designed to find the top 10 most frequent values in a field. However, if the grouping stage produces more than 10 unique values, the `$limit` stage will arbitrarily select the first 10 groups, leading to inaccurate results.

## Solution
The solution involves using the `$sort` stage *before* the `$limit` stage to ensure that the top 10 groups are correctly identified.  This ensures the most frequent groups are considered before the limiting takes place.
