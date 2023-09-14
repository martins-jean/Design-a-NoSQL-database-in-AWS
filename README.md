# Design a NoSQL database in AWS

## Contextual overview

<p align="justify">
The CTO of a gaming company has performance issues with the top players' scoreboard and requests a solution that can improve data access performance.
</p>

## Architecture diagram

![Screenshot 2023-09-04 at 19 31 15](https://github.com/martins-jean/Design-a-NoSQL-Database-in-AWS/assets/118685801/36df7d16-c24f-4060-bc75-a008fa7bb0e5)

## Project objectives

<p align="justify">
1. To design an Amazon DynamoDB NoSQL database well, we should give the most importance to the data access pattern. Every read and write that is made to a DynamoDB table has its Read usage or Write usage computed. <br>
2. To provide access to alternate query patterns and speed up queries, we will create secondary indexes. A global secondary index (GSI) contains a selection of attributes from the base table, but they are organized by a primary key that is different from that of the table. Whenever a table write occurs, all of the table's indexes must be updated. In a write-heavy environment with large tables, this can consume large amounts of system resources. <br>
</p>

## Reproducibility guidelines

<details>
  <summary>Required setup</summary>
  1. Create a DynamoDB table called "player_score" with sample game leaderboard data: <br>
  - Sort key: game_timestamp (number). <br>
  - Partition key: player_name (string). <br>
  - Capacity mode: on-demand. <br>
  2. Create a Cloud9 environment with the following configurations: <br>
  - Environment type: EC2 instance. <br>
  - Platform: Amazon Linux 2. <br>
  - Instance type: t2.small. <br>
</details>

<details>
  <summary>Review the Amazon DynamoDB table structure</summary>
  1. Navigate to the DynamoDb console and click on the table you created. <br>
  2. Click on explore table items and review the items returned. <br>
</details>

<details>
  <summary>Compare the Scan and Query Operations</summary>
  1. Scroll up and select Query next to the Scan selection. <br>
  2. Type a player name from your sample data, click run and review the read capacity units consumed. <br>
  3. Click Scan and expand the filters: <br>
  - Attribute name: badge. <br>
  - Value: Champs. <br>
  4. Click run and review the read capacity units consumed. <br>
  5. Add a filter: <br>
  - Attribute name: game. <br>
  - Value: Kart Brothers. <br>
  6. Click run and review the results. <br>
</details>

<details>
  <summary>Explore the filter expression and limit parameters</summary>
  1. Navigate to the Cloud9 environment you created before and open the IDE. <br>
  2. Open a new terminal and type the following command: <br>
  git clone https://git-codecommit.us-east-1.amazonaws.com/v1/repos/dynamoDB-tests <br>
  3. Change the directory by using: cd dynamoDB-tests. <br>
  4. Install the necessary modules with: sudo pip3 install -r requirements.txt <br>  
  5. Expand the DynamoDB tests folder and open the "player_score_get_item.py" file. <br>
  6. Run the code (the script will get a specific item from the table) and review the output. <br>
  7. Open the "player_score_query.py" file, click run (the script will get data for a specific player) and review the consumed capacity. <br>
  8. Navigate to line 52 in the code and uncomment it, then save the file. <br>
  9. Click run (the script queries a specific player and searches for games where he has received the champs badge). <br>
  10. Review consumed capacity and duration. <br>
  11. Within the same script, uncomment line 53 to see the effects of the limit parameter. <br>
  12. Save the file and run the code once more to verify that zero records are returned. <br>
</details>

<details>
  <summary>Create a global secondary index (GSI) to optimize the search</summary>
</details>

<details>
  <summary>Compare the query performance using the created GSI</summary>
</details>
