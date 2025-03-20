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

Problem Description
-

Our team decided to model a database that administrates, schedules, handles operations of the NCAA Football. In our group’s projects, we made 13 entities that describe the scenario previously stated. The 13 entities also show the relationships between one another that helped build the complete data model. From our perspective, we decided that players, coaches, and the team aligned with one another for the managing aspect along with tracking player statistics with their corresponding season. While the NCAA does handle, these are only the championship tickets. From a backend perspective,we made a way to handle financial transactions of tickets and sponsorships for games not including championship. We also included a way to maintain stadium information and its ticket sales as well as its handling of broadcasting and broadcasters of each game. This model demonstrates how this key importance of handling regular game tickets is valuable for them and their operations.


Data Model
-
<img width="629" alt="Image" src="https://github.com/user-attachments/assets/ee77062e-b8b0-4168-84be-7f30ed866277" />

Our team’s data model is based on different attributes for the NCAA. Each Team has many Players but one Player can only belong to one Team. A Team can also have multiple Coaches but each Coach only belongs to one Team.  A Team can have multiple Sponsorships but each Sponsorship is associated with only one Team. Sponsors can also have many Sponsorships with different Teams.There is a many-to-many relationship with Game and Team because a Team can play multiple games and a Game involves two teams(home and away). Each Game belongs to a certain season played in which a Season can have multiple Games. Each Game is also played in one Stadium but the Stadium can host multiple Games. Each Game is able to have multiple Statistics records for different Players but each Statistics record can only belong to each single Game. A similar concept applies for Players as a Player can have multiple Statistics records for different games but each Statistics record belongs to a single Player. Multiple Tickets are associated to one Game but each ticket belongs to a single Game. Multiple Broadcasts can be associated with one Game as well as a Broadcast can have multiple Games.

Data Dictionary 
- 


Ten Queries
- 


**Query 1**
- SELECT Player.firstNamePlayer, Player.lastNamePlayer, Team.teamName
FROM Player
JOIN Team ON Player.Team_teamID = Team.teamID;
<img width="636" alt="Image" src="https://github.com/user-attachments/assets/18178e75-0be7-4875-ade3-38cbb9afb2ac" />

- This query retrieves all players names along with their team name by joining Player and Team tables through the Team_teamID foreign key. It allows for a quick way to access and view the players and which team they belong to. This is also useful for general lookup of a player but alspo finding their corresponding teams and their rosters. It is beneficial for basic reports that can display the player-team relationship.

**Query 2**
- SELECT g.gameID, g.gameDate, t.teamName
FROM Game g
JOIN GameTeam gt ON g.gameID = gt.gameID
JOIN Team t ON gt.teamID = t.teamID
WHERE t.teamName = 'Alabama Crimson Tide';
<img width="524" alt="Image" src="https://github.com/user-attachments/assets/abdb402c-73d8-422d-b51f-ae6d64266f80" />

- This SQL query retrieves all games played by the Alabama Crimson Tide, displaying the game ID, game date, and team name. This query also joins several tables which are Game, GameTeam, and Team. It allows for analysts and reporters to see past and upcoming games for the specific team and allows for fans to look up a specific team and the game date since many fans look to only support a specific team.

**Query 3**
- SELECT t.teamName,
    MAX(st.recevingYards) AS maxReceivingYards,
    MAX(st.passingYards) AS maxPassingYards,
    MAX(st.rushingYards) AS maxRushingYards
FROM Team t
JOIN Player p ON t.teamID = p.Team_teamID
JOIN Statistics st ON p.playerID = st.Player_playerID
JOIN Game g ON st.Game_gameID = g.gameID
JOIN Stadium s ON g.Stadium_stadiumID = s.stadiumID
WHERE p.positionPlayer = 'Quarterback' 
GROUP BY t.teamName
ORDER BY MAX(st.passingYards), MAX(st.recevingYards) , MAX(st.rushingYards);
<img width="706" alt="Image" src="https://github.com/user-attachments/assets/fcd0a3a4-e98e-42fe-bc13-11e176fdc41a" />

- This query retrieves the maximum receiving, passing, and rushing yards that were achieved in each team. By viewing a very specific position which in this case was Quarterback, it allows managers, coaches, and analysts to see results from each team with the highest values of this particular position.  This is crucial for analyzing this particular role and where they are performing the highest. It also allows for comparison across the different teams to determine teams with highest performance.


**Query 4** 
- SELECT g.gameID, g.gameDate, s.stadiumName
FROM Game g
JOIN Stadium s ON g.Stadium_stadiumID = s.stadiumID
WHERE s.stadiumName = 'West Johnville Stadium';
<img width="656" alt="Image" src="https://github.com/user-attachments/assets/bb0b133d-1143-4c49-8e81-9b9f5bc66934" />

- This query retrieves game ID, game date and stadium name for the games in a specfic stadium. In this case, we used West Johnville Stadium by using Join between Game and Stadium Tables. This ensures that only games hosted at the specific stadium are recorded. The WHERE clause was necessary to provide the games that took place in the specific stadium (West Johnville Stadium). This is crcuial for analysts, managers, and fans to view where and when a specific game is to be held at the specific stadium.

**Query 5** 
- SELECT t.teamID, t.teamName, sp.sponsorName, s.sponsorshipAmount
FROM Sponsorship s
JOIN Team t ON s.Team_teamID = t.teamID
JOIN Sponsor sp ON s.Sponsor_sponsorID = sp.sponsorID
WHERE s.sponsorshipAmount > (SELECT AVG(sponsorshipAmount) FROM Sponsorship)
ORDER BY s.sponsorshipAmount DESC;
<img width="599" alt="Image" src="https://github.com/user-attachments/assets/d9b672b7-300d-4d5f-8602-13df482636fa" />

- This shows the teams with above-average sponsorship deals and the name of their sponsor, orders the list from highest to lowest. It joins the Team, Sponsorship, and Sponsor tables to display team name, sponsor name, and sponsorship amount. The subquery calculates the average sponsorship amount across all teams. It is the most helpful for identifying teams with large funding and their key sponsors, helping analysts understand which sponsors contribute the most, and supporting teams in negotiating sponsorship deals.

**Query 6**
- SELECT P.firstNamePlayer, P.lastNamePlayer, S.year, ST.passingYards
FROM Statistics ST
JOIN Player P ON ST.Player_playerID = P.playerID
JOIN Season S ON ST.Season_seasonID = S.seasonID
WHERE ST.passingYards > 4700
ORDER BY ST.passingYards DESC;
<img width="610" alt="Image" src="https://github.com/user-attachments/assets/1993b994-2732-430d-a953-3e7a28546157" />

- Lines of players’ first and last names are returned with this query as well as the season and their passing yards, which is sorted from highest passing yards to lowest.  This query also specifically grabs players with more than 4700 passing yards. This is a multi join through three different tables which are Statistics, Player and Season. By specifically seeing those who have a high number of passing yards, coaches can identify top-performing players. This is also crucial for player recognition, strategy planning, and potential scouting. 

**Query 7**
- SELECT G.gameDate, S.stadiumName, MAX(T.price) AS highestTicketPrice
FROM Ticket T
JOIN Game G ON T.Game_gameID = G.gameID
JOIN Stadium S ON G.Stadium_stadiumID = S.stadiumID
GROUP BY G.gameDate, S.stadiumName
ORDER BY highestTicketPrice DESC;
<img width="618" alt="Image" src="https://github.com/user-attachments/assets/20374aab-38e9-4c0f-b6c3-adc73287d0de" />

- This query retrieves the most expensive ticket price of each game along with the date of the game and the stadium at which the game occurred. It sorts the ticket pricing from the highest to lowest using the descending order. This is beneficial for financial and revenue analysis and being able to see what specific game date and stadium brought the highest selling tickets. It allows managers to view what locations drive the most popularity to assist in future pricing strategies.

**Query 8** 
- SELECT T.teamName, SUM(GT.isWinner) AS totalWins,
COUNT(GT.gameID) AS totalGamesPlayed,ROUND((SUM(GT.isWinner) / COUNT(GT.gameID)) * 100, 2) AS winPercentage
FROM GameTeam GT
JOIN Team T ON GT.teamID = T.teamID
GROUP BY T.teamName
ORDER BY totalWins DESC, winPercentage DESC;
<img width="638" alt="Image" src="https://github.com/user-attachments/assets/92113ac9-8413-417f-88b4-8896de27226a" />

- This retrieves the teams, the wins the team has, and calculates the win percentage of the team. The query also sorts the table in descending order by total wins and win percentage. This is highly critical to coaches, managers, and analysts in tracking performance of entire teams. This also permits analysts to observe in which position every team can be placed in terms of their wins and win rate. This also gives a scope for teams with higher wins to form more sponsorship agreements, which will earn them more money. 

**Query 9**
- SELECT g.gameID, s.stadiumName, COUNT(t.ticketID) AS totalTicketsSold, 
       AVG(t.price) AS avgTicketPrice
FROM Game g
JOIN Stadium s ON g.Stadium_stadiumID = s.stadiumID
JOIN Ticket t ON g.gameID = t.Game_gameID
WHERE s.stadiumName REGEXP '^B'  -- stadium starts with letter B
GROUP BY g.gameID, s.stadiumName  -- Group by each game and stadium
HAVING AVG(t.price) > 120  -- Ensure only games with an avg ticket price > 120
ORDER BY avgTicketPrice ASC;
<img width="562" alt="Image" src="https://github.com/user-attachments/assets/9d079e40-1280-4970-beb6-166287ecf6b9" />

- This query allows for the average ticket per price of the game and ensures the count of all tickets sold per game. This also filters that the average ticket prices are above $120 and sorting the average prices from lowest to highest prices are shown. By not excluding any of the stadiums, it allows for a broader view of ticket pricing trends of stadiums with a average price greater than 120. This also helps to see which stadium has a cheaper average ticket to help with pricings. 

**Query 10**
- SELECT 
    g.gameID, 
    g.gameDate, 
    s.stadiumName, 
    t.price
FROM Game g
JOIN Stadium s ON g.Stadium_stadiumID = s.stadiumID
JOIN Ticket t ON g.gameID = t.Game_gameID
WHERE s.capacity > 50000  
AND EXISTS (
    SELECT 1
    FROM Ticket tk2
    WHERE tk2.Game_gameID = g.gameID
    AND tk2.price >= (
        SELECT AVG(tk3.price) 
        FROM Ticket tk3 
        WHERE tk3.Game_gameID = tk2.Game_gameID
    )
)
ORDER BY t.price DESC;
<img width="600" alt="Image" src="https://github.com/user-attachments/assets/60635bae-b1dc-41aa-8640-d7e92cc92712" />

- This query is helpful for showing patterns in ticket pricing for large stadiums. By focusing on games in stadiums with a capacity larger than 50,000, it makes sure that at least one ticket for each game is priced at or above the game's average ticket price. This insight helps teams, event planners, and analysts evaluate premium pricing strategies, see demand for high-profile matches, and maximize revenue. By using exists the query shows games where premium-priced tickets are available and how ticket prices change across different events and venues.


Matrix
-

