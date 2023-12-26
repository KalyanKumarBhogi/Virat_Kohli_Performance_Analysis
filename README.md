Analyzing a player’s performance is one of the Data science use cases in sports analytics. Virat Kohli is one of the most famous cricketers in the world. In this project, I am analyzing the Batting Performance of Virat Kohli. <p>

# Virat Kohli Performance Analysis <p>
Virat Kohli is one of the most famous cricketers in the world. The dataset contains of all the ODI matches played by Virat Kohli from 18 August 2008 to 22 January 2017. Here I am analyzing the performance of Virat Kohli in ODI matches. <p>

Below is the complete information about all the columns in the dataset:  <p>

1. Runs: Runs in the match  <p>
2. BF: Balls faced in the match <p>
3. 4s: number of 4s in a match <p>
4. 6s: number of 6s in a match <p>
5. SR: Strike Rate in the match <p>
6. Pos: Batting Position in the match <p>
7. Dismissal: How Virat Kohli got out in the match <p>
8. Inns: 1st and 2nd innings <p>
9. Opposition: Who was the opponent of India <p>
10. Ground: Venue of the match <p>
11. Start Date: Date of the match <p>

# Virat Kohli Performance Analysis using Python <p>

**I will start this task by importing the necessary Python libraries and the dataset:** <p>
 
import pandas as pd <p>
import numpy as np <p>
import plotly.express as px <p>
import plotly.graph_objects as go <p>

data = pd.read_csv("Virat_Kohli.csv") <p>
print(data.head()) <p>

**Let’s have a look at whether this dataset contains any null values or not before moving forward:** <p>

print(data.isnull().sum()) <p>

The dataset contains matches played by Virat Kohli between 18 August 2008 and 22 January 2017. So let’s have a look at the total runs scored by Virat Kohli: <p>

**Total Runs Between 18-Aug-08 - 22-Jan-17** <p>
data["Runs"].sum() <p>

**Now let’s have a look at the average of Virat Kohli during the same period:** <p>

**Average Runs Between 18-Aug-08 - 22-Jan-17** <p>
data["Runs"].mean() <p>

**In ODIs, the batting average of 35-37 is considered a good average. So Virat Kohl’s batting average is good. Now let’s have a look at the trend of runs scored by Virat Kohli in his career from 18 August 2008 to 22 January 2017:** <p>

matches = data.index  <p>
figure = px.line(data, x=matches, y="Runs",  <p>
                 title='Runs Scored by Virat Kohli Between 18-Aug-08 - 22-Jan-17') <p>
figure.show() <p>

**In so many innings played by Virat Kohli, he scored over 100 or close to it. That is a good sign of consistency. Now let’s see all the batting positions played by Virat Kohli:** <p>


**Batting Positions**  <p>
data["Pos"] = data["Pos"].map({3.0: "Batting At 3", 4.0: "Batting At 4", 2.0: "Batting At 2",  <p>
                               1.0: "Batting At 1", 7.0:"Batting At 7", 5.0:"Batting At 5",  <p>
                               6.0: "batting At 6"}) <p>
Pos = data["Pos"].value_counts() <p>
label = Pos.index <p>
counts = Pos.values <p>
colors = ['gold','lightgreen', "pink", "blue", "skyblue", "cyan", "orange"] <p>

fig = go.Figure(data=[go.Pie(labels=label, values=counts)]) <p>
fig.update_layout(title_text='Number of Matches At Different Batting Positions') <p>
fig.update_traces(hoverinfo='label+percent', textinfo='value', textfont_size=30, <p>
                  marker=dict(colors=colors, line=dict(color='black', width=3))) <p> 
fig.show() <p>

**In more than 68% of all the innings played by Virat Kohli, he batted in the third position. Now let’s have a look at the total runs scored by Virat Kohli in different positions:** <p>

label = data["Pos"]  <p>
counts = data["Runs"] <p>
colors = ['gold','lightgreen', "pink", "blue", "skyblue", "cyan", "orange"] <p>
 
fig = go.Figure(data=[go.Pie(labels=label, values=counts)]) <p>
fig.update_layout(title_text='Runs By Virat Kohli At Different Batting Positions') <p>
fig.update_traces(hoverinfo='label+percent', textinfo='value', textfont_size=30, <p>
                  marker=dict(colors=colors, line=dict(color='black', width=3))) <p>
fig.show() <p>

**More than 72% of the total runs scored by Virat Kohli are while batting at 3rd position. So we can say batting at 3rd position is perfect for Virat Kohli.** <p>

**Now let’s have a look at the number of centuries scored by Virat Kohli while batting in the first innings and second innings:** <p>

centuries = data.query("Runs >= 100")  <p>
figure = px.bar(centuries, x=centuries["Inns"], y = centuries["Runs"],  <p>
                color = centuries["Runs"], <p>
                title="Centuries By Virat Kohli in First Innings Vs. Second Innings") <p>
figure.show() <p>

**So most of the centuries are scored while batting in the second innings. By this, we can say that Virat Kohli likes chasing scores. Now let’s have a look at the kind of dismissals Virat Kohli faced most of the time:**  <p>

# Dismissals of Virat Kohli <p>
dismissal = data["Dismissal"].value_counts() <p>
label = dismissal.index <p>
counts = dismissal.values <p>
colors = ['gold','lightgreen', "pink", "blue", "skyblue", "cyan", "orange"] <p>

fig = go.Figure(data=[go.Pie(labels=label, values=counts)]) <p>
fig.update_layout(title_text='Dismissals of Virat Kohli') <p>
fig.update_traces(hoverinfo='label+percent', textinfo='value', textfont_size=30, <p>
                  marker=dict(colors=colors, line=dict(color='black', width=3))) <p>
fig.show() <p>

**So most of the time, Virat Kohli gets out by getting caught by the fielder or the keeper. Now let’s have a look at against which team Virat Kohli scored most of his runs** <p>

figure = px.bar(data, x=data["Opposition"], y = data["Runs"], color = data["Runs"], <p>
            title="Most Runs Against Teams") <p>
figure.show() <p>

**According to the above figure, Virat Kohli likes batting against Sri Lanka, Australia, New Zealand, West Indies, and England. But he scored most of his runs while batting against Sri Lanka. Now let’s have a look at against which team Virat Kohli scored most of his centuries:** <p>

figure = px.bar(centuries, x=centuries["Opposition"], y = centuries["Runs"],  <p>
                color = centuries["Runs"], <p>
                title="Most Centuries Against Teams") <p>
figure.show() <p>

**So, most of the centuries scored by Virat Kohli were against Australia. Now let’s analyze Virat Kohli’s strike rate. To analyze Virat Kohli’s strike rate, I will create a new dataset of all the matches played by Virat Kohli where his strike rate was more than 120:** <p>

strike_rate = data.query("SR >= 120") <p>
print(strike_rate) <p>

**Now let’s see whether Virat Kohli plays with high strike rates in the first innings or second innings:** <p>

figure = px.bar(strike_rate, x = strike_rate["Inns"],  <p>
                y = strike_rate["SR"],  <p>
                color = strike_rate["SR"], <p>
            title="Virat Kohli's High Strike Rates in First Innings Vs. Second Innings") <p>
figure.show() <p>

**So according to the above figure, Virat Kohli likes playing more aggressively in the first innings compared to the second innings. Now let’s see the relationship between runs scored by Virat Kohli and fours played by him in each innings:** <p>

figure = px.scatter(data_frame = data, x="Runs",  <p>
                    y="4s", size="SR", trendline="ols",  <p>
                    title="Relationship Between Runs Scored and Fours") <p>
figure.show() <p>

**There is a linear relationship. It means that Virat Kohli likes playing fours. The more runs he scores in the innings, the more fours he plays. Let’s see if there is some relationship with the sixes:** <p>

figure = px.scatter(data_frame = data, x="Runs", <p>
                    y="6s", size="SR", trendline="ols",   <p>
                    title= "Relationship Between Runs Scored and Sixes") <p>
figure.show() <p>

**There is no strong linear relationship here. It means Virat Kohli likes playing fours more than sixes. So this is how you can analyze the performance of Virat Kohli or any other cricketer in the world.**




