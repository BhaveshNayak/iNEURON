This is a real time dataset of the ineuron technical consultant team. You have to perform hive analysis on this given dataset.

Download Dataset 1 - https://drive.google.com/file/d/1WrG-9qv6atP-W3P_-gYln1hHyFKRKMHP/view

Download Dataset 2 - https://drive.google.com/file/d/1-JIPCZ34dyN6k9CqJa-Y8yxIGq6vTVXU/view

Note: both files are csv files. 


1. Create a schema based on the given dataset

--create database

create database hive_final_min_project_1;

use hive_final_min_project_1;

--create table AgentLogingReport

Create table AgentLogingReport
(
sr_no int,
Agent string,
Date date,
Login string,
Logout string,
Duration string
)
row format delimited
fields terminated by ','
tblproperties ("skip.header.line.count" = "1");


--create table AgentPerformance

Create table AgentPerformance
(
sr_no int,
Date date,
Agent_Name string,
Total_charts int,
Avg_Response_Time string,
Avg_Resolution_Time string,
Avg_Rating float,
Total_Feedback int
)
row format delimited
fields terminated by ','
tblproperties ("skip.header.line.count" = "1");


2. Dump the data inside the hdfs in the given schema location.

--load data into AgentLogingReport table
load data local inpath '/home/cloudera/AgentLogingReport.csv' into table AgentLogingReport;

--load data into AgentPerformance table
load data local inpath '/home/cloudera/AgentPerformance.csv' into table AgentPerformance;


3. List of all agents' names. 

select agent_name from AgentLogingReport;

Agent
Shivananda Sonwane
Khushboo Priya
Nandani Gupta
Hrisikesh Neogi
Mukesh
Sowmiya Sivakumar



4. Find out agent average rating.

select avg_rating from AgentPerformance;

4.11
3.14
4.55
4.71
3.67
4.62
5.0
5.0
4.38



5. Total working days for each agents 

select agent_name,count(login_time) as total_working_days from AgentLogingReport group by agent_name;

agent_name	total_working_days
Aditya Shinde	1
Aditya_iot	9
Agent	1
Amersh	4
Ameya Jain	10
Ankitjha	4
.
.
.


6. Total query that each agent have taken 

select agent_name,sum(total_chats) as Total_Query from AgentPerformance group by agent_name;

agent_name	total_query
Abhishek 	0
Aditya 	0
Aditya Shinde	277
Aditya_iot 	231
Agent Name	NULL
Amersh 	0
Ameya Jain	322
Anirudh 	81




7. Total Feedback that each agent have received 

select agent_name,sum(total_feedback) as Total_Feedback from AgentPerformance group by agent_name;

agent_name	total_feedback
Abhishek 	0
Aditya 	0
Aditya Shinde	153
Aditya_iot 	131
Agent Name	NULL
Amersh 	0
Ameya Jain	228
Anirudh 	39


8. Agent name who have average rating between 3.5 to 4 

select agent_name,avg_rating from AgentPerformance where  avg_rating > 3.5 and avg_rating < 4;

agent_name	avg_rating
Swati 	3.67
Manjunatha A	3.6
Prateek _iot 	3.75
Nandani Gupta	3.79
Jaydeep Dixit	3.95


select distinct(agent_name) as Agent_name,avg_rating from AgentPerformance where  avg_rating > 3.5 and avg_rating < 4;

agent_name	avg_rating
Aditya Shinde	3.54
Aditya_iot 	3.53
Aditya_iot 	3.83
Aditya_iot 	3.86
Anirudh 	3.77
Ayushi Mishra	3.8
Ayushi Mishra	3.86
Ayushi Mishra	3.88


9. Agent name who have rating less than 3.5 

select agent_name,avg_rating from AgentPerformance where  avg_rating < 3.5;

agent_name	avg_rating
Nandani Gupta	3.14
Hitesh Choudhary	0.0
Sanjeevan 	0.0
Anirudh 	0.0
Shiva Srivastava	0.0
Dibyanshu 	0.0
Ashish 	0.0
Uday Mishra	0.0
Aditya Shinde	0.0
Jayant Kumar	0.0


select distinct(agent_name) as Agent_name,avg_rating from AgentPerformance where  avg_rating < 3.5;

agent_name	avg_rating
Abhishek 	0.0
Aditya 	0.0
Aditya Shinde	0.0
Aditya_iot 	0.0
Aditya_iot 	2.67
Aditya_iot 	3.33
Aditya_iot 	3.4


10. Agent name who have rating more than 4.5 

select agent_name,avg_rating from AgentPerformance where  avg_rating > 4.5;

agent_name	avg_rating
Ameya Jain	4.55
Mahesh Sarade	4.71
Mukesh 	4.62
Saikumarreddy N	5.0
Sanjeev Kumar	5.0
Harikrishnan Shaji	4.57
Sowmiya Sivakumar	4.75
Boktiar Ahmed Bappy	4.75
Shivananda Sonwane	5.0
Ishawant Kumar	4.67
Deepranjan Gupta	4.8
Shivananda Sonwane	4.67
Muskan Garg	5.0
Aditya_iot 	4.6


select distinct(agent_name) as Agent_name,avg_rating from AgentPerformance where  avg_rating > 4.5;

agent_name	avg_rating
Aditya Shinde	4.53
Aditya Shinde	4.57
Aditya Shinde	4.67
Aditya Shinde	4.78
Aditya Shinde	4.89
Aditya Shinde	4.93
Aditya Shinde	5.0
Aditya_iot 	4.56


11. How many feedback agents have received more than 4.5 average

select agent_name,total_feedback,avg_rating from AgentPerformance where avg_rating > 4.5;

agent_name	total_feedback	avg_rating
Ameya Jain	11	4.55
Mahesh Sarade	7	4.71
Mukesh 	8	4.62
Saikumarreddy N	12	5.0
Sanjeev Kumar	6	5.0
Harikrishnan Shaji	7	4.57
Sowmiya Sivakumar	16	4.75
Boktiar Ahmed Bappy	4	4.75
Shivananda Sonwane	1	5.0
Ishawant Kumar	3	4.67

select sum(total_feedback) as Total_Feedback from AgentPerformance where avg_rating > 4.5;

total_feedback
3489


12. average weekly response time for each agent 

select agent_name,avg_response_time from AgentPerformance;

Agent Name	Average Response Time
Prerna Singh	0:00:38
Nandani Gupta	0:01:15
Ameya Jain	0:00:30
Mahesh Sarade	0:01:04
Swati 	0:01:11


13. average weekly resolution time for each agents 

select agent_name,avg_resolution_time from AgentPerformance;

agent_name	avg_resolution_time
Agent Name	Average Resolution Time
Prerna Singh	0:04:20
Nandani Gupta	0:28:25
Ameya Jain	0:11:36
Mahesh Sarade	0:15:46


14. Find the number of chat on which they have received a feedback 

select sum(total_chats) as Num_of_chats from AgentPerformance where total_feedback != 0;

num_of_chats
14702
