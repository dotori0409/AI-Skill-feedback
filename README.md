# AI-feedback-system

This project aims to develop an Artificial Intelligence-based solution that detects users’ skills in the virtual world, analyzes their performance, and provides personalized feedback to improve their reasoning and overall performance. By coaching them according to their situation, shortcomings and potential, the solution will help improve their skills and optimize their learning experience in Virtual Reality (VR) training software. 

**Assumptions:**
1. Data is accurate.
2. Data consists of only the completed results of each scenario.
3. Individual skills can be evaluated from a number ranging from 0 to 100 with 2 decimal precision.
4. There is an AI feedback system already created that provides personalized feedback when the skill history data is given as input.

**Final Design**
The final design for characterizing an individual's skills and suggesting AI-generated improvements relied on 6 predominant steps as outlined in the figure below. 
Initially, a detailed user action and response case table was established to define the flow of events within the VR environment for each scenario. In this table, all of the alternate flows and options available to the user were presented as well as the ‘optimal’ path as defined by Inmerzum’s initial recommendations. The user would be prompted in the VR world to complete the scenario and re-do each sub-flow if the incorrect answer is selected. The incorrect selection of each answer is recorded and the AI system is used to provide personalized feedback using the Chat GPT API module. 

A total of six parameters are gathered from the user during their completion of a scenario within the VR environment. These consist of:
  1. User ID: Identifier variable that is unique for each user (INTEGER)
  2. Average Time Response: The absolute value of the average difference in time between the actual time taken by the user during the scenario and the optimal/recommended time table (INTEGER in seconds)
  3. Tool Correct: Did the user select the most appropriate tool for the activity? (BOOLEAN true/ false value)
  4. Percentage of Wrongs: How many percent of questions the user got wrong during their completion of a particular scenario? (INTEGER as a percentage)
  5. Completion Status: Was the entire scenario completed by the user? (BOOLEAN true/ false value)
Excess Button Press Amount: How many times did the user press the buttons on the VR controller unnecessarily? (STRING in the form of which button was pressed, how many times it was pressed)

The algorithm then outputs an integer percentage between 0 and 100% for each target based on the user's performance in the scenario. If the user had not completed the exercise before, the scores are fed into the chat GPT API to generate personalized improvement responses in the form of text. Else, if the user had previously attempted the exercise, their results are compared with their previous results as stored in an SQL database to generate a different personalized improvement response also in text format. The data is continually stored in the SQL database using the following schema: 

Figure 1. Database Schema
<img width="390" alt="Screen Shot 2023-07-20 at 9 50 20 am" src="https://github.com/dotori0409/AI-feedback-system/assets/71887438/9da67064-2608-4723-9ed5-68da0d19390a">

If the user reaches 100% completion status in all of the skills required in the scenario, their entries are removed from the SQL database to optimize performance and storage on the server. 

**Results and Discussion**
_Regression AI Implementation_
To evaluate the effectiveness of our AI assessment module, we conducted a thorough analysis using purposely generated data with a decreasing trend. The primary goal was to determine if our system would yield increasing numbers as a result. As expected, the outcome of the assessment revealed that all skills showcased a consistent upward trendline. These findings align with our initial expectations and provide evidence of the module's capability to generate favorable outcomes even when presented with valid data. This outcome affirms the robustness and reliability of our AI assessment module in delivering accurate and reliable assessments.

Figure 2. AI Skill Assessment Output
<img width="490" alt="Screen Shot 2023-07-20 at 9 52 49 am" src="https://github.com/dotori0409/AI-feedback-system/assets/71887438/49e90676-cc7c-475d-8a93-7704f0362107">

Figure 3. Input Error Data Trend
<img width="320" alt="Screen Shot 2023-07-20 at 9 53 32 am" src="https://github.com/dotori0409/AI-feedback-system/assets/71887438/7e932142-f63e-47e4-a517-c93fde5fd1aa">

Figure 4. Output Data Trend
<img width="620" alt="Screen Shot 2023-07-20 at 9 53 03 am" src="https://github.com/dotori0409/AI-feedback-system/assets/71887438/43daa41c-4a2a-4b25-9c67-c4216c0860b2">

_Storing in Database_
To ensure the precision and correctness of our MySQL schema and code, we utilized pgAdmin, an open-source administration and development platform specifically tailored for PostgreSQL. By leveraging the capabilities of this platform, we were able to rigorously test our implementation and validate the accuracy of data storage within the database.
Throughout the testing process, we conducted various assessments and examinations to ascertain that the data were appropriately stored. We meticulously verified the integrity of the database by performing checks on the consistency, completeness, and accuracy of the stored information.
The accompanying figures presented below provide visual evidence of the successful storage of all data in the database. These figures serve as concrete proof that our MySQL schema and code effectively perform their intended function of storing data accurately and reliably.

Figure 5. Data Stored in Database
![YdNNaS68j35Skhl0ebbQiAttqkdkDa7-xKUJSYoHgwCKllyDBEyyp9rv52qDRrvSDvbR5T8hi3e31-L-KDaVHcDUricHNkWeWWvYh6E-kfimjTmu_2iw15odVzXu](https://github.com/dotori0409/AI-feedback-system/assets/71887438/bc08e64f-1294-4fbd-99e4-cb28e769506b)

_AI feedback_
We have achieved successful integration of the ChatGPT API into our system, enabling us to provide personalized feedback. By utilizing this API, we have implemented a mechanism to deliver customized responses and tailored suggestions based on user interactions. This integration has allowed us to enhance the user experience and provide more relevant and accurate feedback to our users.

Figure 6. AI Feedback Based on Increasing Trend
<img width="1063" alt="Screen Shot 2023-07-20 at 10 06 22 am" src="https://github.com/dotori0409/AI-feedback-system/assets/71887438/c4cd580e-0a0a-4175-b6e3-15b2ea28fbad">

**Design Iteration**
1. The first design iteration is a type of binary classifier to classify if the user has a certain job-specific soft skill or not. These skills include stress management, decision-making, and adaptability. The initial input attributes include time response, tool correction, number of errors, user button press amount, and task completion status. The classifiers used include decision tree, random forest, and K-Nearest neighbors (KNN). It only demonstrates iteration to show the whole process to the client, so there are no additional processing methods to improve the classification performance. The classification output is binary, which means it only indicates if the user has the skills or not. Can use regression method to indicate skill level next time.
<img width="247" alt="Screen Shot 2023-07-20 at 9 45 52 am" src="https://github.com/dotori0409/AI-feedback-system/assets/71887438/e5ed1c19-6f2f-41eb-ab4b-6e92d13c5177">

2. The second design iteration is a type of regression predictor to quantify how many percents of the user has a certain job-specific soft skill or not. To easily demonstrate we only use stress management as an example. The initial input attributes are the same as the first design iteration. Three regression models used include linear regression, ridge regression, and polylinear regression.
<img width="285" alt="Screen Shot 2023-07-20 at 9 46 35 am" src="https://github.com/dotori0409/AI-feedback-system/assets/71887438/681aac53-852a-41a9-a6f6-bb23c575f376">
