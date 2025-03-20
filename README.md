# MIST-4610-PROJECT-1

NCAA Football 
- 

**Team Members and Names**

Group 5
- Gisel Hernandez
- Ansley Hankinson
- Lukas Cornish
- Malhar Sethia
- Samuel White

**Problem Description**

Our team decided to model a database that administrates, schedules, handles operations of the NCAA Football. In our group’s projects, we made 12 entities that describe the scenario previously stated. The 12 entities also show the relationships between one another that helped build the complete data model. From our perspective, we decided that players, coaches, and the team aligned with one another for the managing aspect along with tracking player statistics with their corresponding season. While the NCAA does handle, these are only the championship tickets. From a backend perspective,we made a way to handle financial transactions of tickets and sponsorships for games not including championship. We also included a way to maintain stadium information and its ticket sales as well as its handling of broadcasting and broadcasters of each game. This model demonstrates how this key importance of handling regular game tickets is valuable for them and their operations.


**DATA MODEL**

<img width="623" alt="Image" src="https://github.com/user-attachments/assets/eb45cfc1-445b-414b-9123-13960efe1c76" />

Our team’s data model is based on different attributes for the NCAA. Each Team has many Players but one Player can only belong to one Team. A Team can also have multiple Coaches but each Coach only belongs to one Team.  A Team can have multiple Sponsorships but each Sponsorship is associated with only one Team. Sponsors can also have many Sponsorships with different Teams. There are many entities that tie to the Game entity. For instance, a Game can only have one winner, which is one Team. Each Game belongs to a certain season played in which a Season can have multiple Games. Each Game is also played in one Stadium but the Stadium can host multiple Games. Each Game is able to have multiple Statistics records for different Players but each Statistics record can only belong to each single Game. A similar concept applies for Players as a Player can have multiple Statistics records for different games but each Statistics record belongs to a single Player. Multiple Tickets are associated to one Game but each ticket belongs to a single Game. Multiple Broadcasts can be associated with one Game as well as a Broadcast can have multiple Games.

**Data Dictionary**


Ten Queries
- 


Query 1
- This query retrieves all players names along with their team name by joining Player and Team tables through the Team_teamID foreign key. It allows for a quick way to access and view the players and which team they belong to. This is also useful for general lookup of a player but alspo finding their correspodning teams and their rosters.

Query 2
- Though it may seem complex, this is actually a simple query because this is the joining of all of the tables together. By joining all of the tables that the database has created, we can retrieve all information related to the team, players, coaches, statistics, games, seasons, stadiums, sponsors, tickets, and broadcasts.

Query 3
- This query retrieves coaches and their perspective team through joining Coach and Team by the Tean_teamID foreign key. Thi query allows to provide a reference of their team. This also allows for team management and sports analysis for sports analysts who want to associate the coach to their team.

Query 4 
- This query retrieves game ID, game date and stadiym name for the games in a specfic stadium. In this case, we used Sanford Stadium by using Inner Join between Game and Stadium Tables. This ensures that only games hosted at the specific stadium are recorded. The WHERE clause was necessary to provide the games that took place in the specific stadium (Sanford Stadium). This is crcuial for analysts, managers, and fans to view where and when a specific game is to be held at the specific stadium.

Query 5 
- This query allows a structure of providing details of each game which includes their game date, home and away teams as well as their scores, location of the match and the season(year) it took place. This query also joined multi tables such as Game, Team, Stadium, and Season. By allowing the joining of this, it allows analysts to look over team performance and overall score. Through sorting the games in descending order allows to view the most recent game which is useful for up-to-date gamesights

Query 6
- This query is useful because it retrieves all the details of ticket sale information which includes game date, home and away teams, where the match took place and its ticket prices. This allowed for the joining of Game, Team, Ticket, and Stadium tables. Being able to view the seat category and it's price allows for financial reports in order to understand what ticket are sold the most and how to price these. Through sorting the game date in descending order ensures that the most recent game shows up first to make a more accurate report for the sales analysis.

Query 7
- This query retrieves the data and performance of the player for each game which shoes the passing tards, rushing yards, total tackles and sacks. Through the joining of Statistics, Player, Game, and Team tables, it is easier to track individual performance of players across their games and teams for analysts. Sorting by date allows for the most rceent performances to appear first.

Query 8 
- This query has an overview of each team and their sponsor name with the amount contributed. Through the joining of Team, Sponsorship, and Sponsor, it allows for teams and financial managers to view the funding sources and financial support of the different companies. By sorting in descending orders allows to highlight the team with the most financial support to the least.

Query 9
- This query allows for the average ticket per price of the game and ensures the count of all tickets sold per game. This also filters that the average ticket prices are above $120 and sorting the average prices from lowest to highest prices are shown. By not excluding any of the stadiums, it allows for a broader view of ticket pricing trends of stadiums with a average price greater than 120. This also helps to see which stadium has a cheaper average ticket to help with pricings. 

Query 10
- This query returns the game date, home and away identifiers as well as their stadiums and prices. This query ensures that games with tickets sold (EXISTS) are considered. This can prevent the listing of games with no tickets sold or have been canceled. This also shows that only stadiums with massive capacities of greater than 100,000 are shown. Tickets are also shown from lowest to highest ticket prices which determines affordable tickets for each game and attracts more fans.

