Milestone 1
MVP Overview
One player hosts the game/room
Host a server to make sure that data is consistent
Title screen 
Lobby screen
Position detection screen

Title Screen
Players must input their username before hosting/joining a room
Game Hosting and Room Connection
Host a game
Create a new room, generate a code for players to join
Start the game


Join a game
Enter a room code to join the game

Show list of players
Position Detection
Goes this screen after the host joined the game
Host has control of the screen, other players see what’s on the host’s screen but can’t interact with it
Screen shows a circle, with dots representing the players labelled by their username
Using UWB, auto detect player’s positions to place them in the circle appropriately, this triggers only once the screen renders. Player positions are “Snapped” into the position of a circle
Add a button that re-detects player’s positioning
Give the player the ability to spin/rotate the circle 
Give the host the ability to manually drag players into the correct position
Milestone 2
Additional Screens: 
Event screen: in case there are any events announced to all players
Each phase should have a different screen
Seating arrangement screen: Allow players to reference the seating arrangement of players in the current round

On each screen: show the time remaining in the round, have a button that navigates to the seating arrangement screen if its not currently using shown

Phase timings:
Passive abilities: 3 minutes
Active discussion: 5 minutes
Nomination period: 3 minutes
Give the host the ability to end a round early
Role Distribution
Randomly assign roles to the players, each player only sees the role they are assigned
Insurgency players get their teammate names
Includes a screen/pop up that shows the role name, description of abilities, etc
Include a confirm button
Once everyone confirms their roles go to the next screen
Passive Abilities
Show the results of the player’s passive abilities
Active Discussion
Include a button to activate active ability
Show a list of players in range of the user (within 2 meters) that the player can select

Nominations
Players are shown the results of their active ability
A random player is picked as the leader
The leader picks a direction (clockwise/counter clockwise)
The player next to the leader in the chosen direction gets 30s to speak (show a speaker icon on their phone)
After their 30s, the next player in the chosen direction goes until it goes back the leader
Button that allows players to nominate themselves for the voting round, except the current leader cannot nominate themselves
Players must self nominate before the end of the leader’s speaking period

Voting
Players get 1 minute to vote for a player, given a list of players that self nominated
Votes are anonymous
Show the results of the votes to all players, including the number of players that voted for each player but not who voted for them

Swapping Players
Leader gets to swap # of players given the round number
Use UWB position detection to auto detect position of players (add a button that re detect once the leader confirms they had the swaps)
Similar to the initial position detection screen, allow the leader to manually move players and confirm the swaps
Detect that an appropriate number of swaps was made

Game Loop
After the leader confirms the players swapping, repeat the game loop with the passive ability. During the passive ability phase, win conditions should be checked
During the next nomination phase, the current leader is the leader and is not randomly picked


Milestone 3
Note taking
Mention usernames (@ username)
Keywords “claim”, or role
Show the seating arrangement of the players in the current round
Customizable Game Length
At the lobby creation, the host has the abilities to tweak the length of each round
Handling Disconnects
When a player disconnects or backgrounds the app, announce to all players who disconnected
Persistence User Accounts
Store game history on a persistent user account
Win/loss, what roles they played, game summaries etc
Game Summaries
Event log of what happened during the game
Bonus stats such as how accurate each player was with their note taking
Wiki
Game rules/manuals
Role book and tips on how each role could be played

Technical Considerations
Nearby Interaction creates pairwise UWB connections, i.e. each device knows its relative distance and direction to each other device. So technically, each phone has its own internal representation of where people are. Will this create problems for a server-hosted game, since which device determines our “ground truth” that is reported to the server? What if many devices have slightly inconsistent distances? This could create weird tiebreaker edge cases where unintended events happen in the game
UWB reporting becomes very restricted after the app moves to the background: so what do we do when a player closes the app? Do we punish them, since it would make them invisible to the network for a period? How do we prevent these minor exploits?


