Project Darkstar's New World of Online Games: A Conversation With Jeff Kesselman
================================================================================

*By Janice J. Heiss, October 2007*

The huge popularity of video games, which rank second only to movies as a source of entertainment in industrialized countries, has created vast opportunities for developers. But the technical and economic challenges involved in creating and deploying online games that scale to thousands of users and dozens of platforms have -- until now -- been enormous, requiring not only expertise in multithreaded programming, distributed computing, and transactional processes but deep pockets to sustain back-end processing resources.

With the open-source release of Sun Labs' Project Darkstar -- which offers Java technology-based infrastructure software designed for latency-critical, massively scaled online applications such as online games -- not only will development costs go down, but the technical challenges of scaling, load balancing, data consistency, and failure recovery currently faced by developers of multiplayer games will be radically reduced or even eliminated. Project Darkstar, which is not to be confused with a game engine or a communications framework, is already being put to good use by leading companies in the games industry.

For an update on Project Darkstar, we met with Sun Labs' Jeff Kesselman, whose official title is "chief instigator" for Project Darkstar. Kesselman has a deep and abiding connection to video games. As an undergraduate at the University of Wisconsin, he crafted a major in computer science, art, and film production, which led to 15 years in the game and multimedia industry after he graduated in 1987.

During his time in the industry, he wrote the U.S. launch demo for the Philips CD-I player, contributed to such commercial games as The Horde, Titan, and Blazing Dragons, and was senior game integration engineer at the Total Entertainment Network, where he wrote Internet networking code for games such as DukeNukem3D, CivNet, Total Annihilation, and Dark Sun Online. In addition, he was co-designer, architect, and lead engineer for Dark Sun Online II: The Age of Heroes.

Kesselman joined Sun in 2001 to work on the JDK performance tuning team, where he concentrated on tuning JDK 1.3. Since 2004, he has focused on the application of Sun technologies in the game industry. He is the coauthor of Java Platform Performance: Strategies and Tactics.

Q: What is Project Darkstar, and why is it being open sourced?

A: It's a Sun Labs project to develop a piece of infrastructure software for latency-critical, massively scaled online applications, which translates, among other things, to massively multiplayer online games.

We've open sourced it to lower the entry barriers to encourage developers to work with it. We want to grow the online game space by reducing the risk and the work required to create games. Open sourcing Project Darkstar is a good way to drive developer adoption. It allows people to play with it without making a big up-front commitment, and it allows them to see better how the system works. They can grab the technology, see what it does, and, we hope, come on board.

Q: What are the details of the open-source licensing release?

A: There are two parts to Project Darkstar -- the server part, which is where most of the technology resides, and a little API on the client side that talks to the server and makes it easy to connect your clients. We've released the server under GPL version 2.0 and the client piece under a modified BSD license.

Q: Why two licenses?

A: It's due to our business goals. We want people to be able to build and redistribute their proprietary online game code freely, but we also want them to share any improvements they make to the Project Darkstar codebase itself. Licensing Project Darkstar server code under GPL supports these objectives.

The client side is different since the client API is a set of libraries that you embed into your own code. Using a modified BSD license here allows developers to use the Project Darkstar client SDK code as part of their game clients, and to relicense and redistribute that combined code however they want.



+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|                       |  Game developers have their own special language to describe their technology.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|dupe (duplication) bug | When an object in a game is in two places at once, in effect duplicating itself. A ball may simultaneously be on the floor and on the table. Dupe bugs reflect breakdowns in referential integrity and occur when back-end systems are not transactional. Project Darkstar is built on a transactional event-processing system that helps prevent dupe bugs.                                                                                                                                                                                                                                |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|rollback               | Current multiplayer online games hold the state of the game in active memory. A rollback is what happens when a game application fails during a game, losing that state and causing players to lose some of their past play, so they are rolled back to an earlier stage of a game or to the very beginning. With Project Darkstar, the entire virtual world persists to permanent storage in a server-side data store, so that your game state isn't lost when a server fails.                                                                                                             |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|disaster               | Worse than a mere failure that causes a rollback, a disaster occurs when the entire machine room goes down. Darkstar's database back end saves a historically accurate record of the game so that at most one or two seconds may be lost. Note: Disaster is a term with general application in computer science.                                                                                                                                                                                                                                                                            |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|lag, laggy             | Any delay after the user takes an action with an input device, such as a mouse or keyboard, before the effect is observed on the screen and/or through in-game sound effects.                                                                                                                                                                                                                                                                                                                                                                                                               |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|zone                   | A given area of a virtual world, such as the town of Bar or the forest of Foo. A zone is a play space. All players in a zone can potentially interact with everyone in that zone. Those outside of the zone cannot. Often, different zones are placed on different physical computers in the machine room, called zone servers.                                                                                                                                                                                                                                                             |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|shard                  | One cluster of zone servers that together describe a complete game world. In order to support large numbers of users, game developers today will replicate the entire world in many different shards. When a player starts a new character, they need to select what is called a server, which is really a cluster of servers, on which they will play with that character. Each of these so-called servers is really a shard, and characters on different shards can't play together. Project Darkstar makes possible shardless worlds, in which all players can interact with each other. |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+



Q: What is Sun's interest in online games?

A: The online game space has huge potential for Sun. Games such as World of Warcraft, Lineage, RuneScape, Final Fantasy, EverQuest, and others serve millions of subscribers and run on thousands of network servers.

Sun sees this as a potential growth market for our servers and for services. The industry estimates that it currently costs about $30 million to create the basics for massively multiplayer online games such as World of Warcraft or EverQuest. By releasing software that reduces development costs, we hope to enable more developers to participate in the rapidly expanding online game market and to create growth opportunities for Sun hardware and service businesses there.

Q: Why are online multiplayer games so expensive to create?

A:  It costs about $10 million to create a traditional game. Multiplayer games require more artwork, but their biggest added expense is designing, developing, and coding your own online game server from the ground up. Your own crews must run the machine room, because everything is one-off and custom.

Project Darkstar solves the problem of building your own game server infrastructure and handles the scaling, load balancing, persistence, and other challenges. This makes it easier and faster to write robust, scalable, and highly performant online games.

Project Darkstar also provides a unified platform that games can be run on so that a single provider can run different games for different people in the same environment, just as you would on an app server. This improves resource utilization at deployment time, which lowers costs on that end too.



+----------------------------------------------------------------------------------------------------------------------------------------------------+
| "Darkstar solves the problem of building your own game infrastructure and handles the scaling, load balancing, persistence, and other challenges." |
|                                                                                                                                                    |
| -- Jeff Kesselman - Chief Instigator, Project Darkstar, Sun Microsystems                                                                           |
+----------------------------------------------------------------------------------------------------------------------------------------------------+ 



The Project Darkstar Server and Client
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Q: What do developers get with the Project Darkstar server and client SDK downloads?

A: By downloading the server today, they receive a single-node version of the server that runs on Windows, Solaris, Linux, even a Mac, and the APIs and documentation to write applications that run inside the server, plus a tutorial that teaches the basics and gives examples.

The client download provides them with client APIs, Javadocs for the client APIs, and another tutorial that explains all the client-side coding with examples.

Developers can sign up at the Project Darkstar community site, where we have an entire portal with downloads and forums. Working through both the server and client tutorials is a good way to start to understand the system. A very active community forum exists to answer questions.

No More Dupe Bugs
^^^^^^^^^^^^^^^^^

Q: Project Darkstar is touted as enabling online game developers to deal successfully with client failures, machine-room disasters, and race conditions. Tell us about those.

A: I'll address race conditions, which produce dupe bugs, first. The online game community has its own language for describing bugs, which they describe from the perspective of players and not in terms of what causes them. For instance, almost every online game has what's called a dupe bug, which refers to the ability to place an object in a game in two places at once. So, for instance, an object could be both on the ground and in my pocket simultaneously, or on the table and on the floor. So they are called duplication bugs.

From the point of view of a database programmer, that's a break in referential integrity. We know exactly what causes it: It's because the systems aren't transactional on the back end, so they can temporarily end up in states in which the referential integrity is not preserved. Darkstar is built on a transactional event-processing system that prevents this from happening.

Q: Give us some details on how dupe bugs occur.

A: This is an oversimplified example, but imagine I engage in the act of giving you a dollar.

You might code it in a way similar to this:

    1. Add $1 to your wallet. Increase your money variable by one. 

    2. Remove $1 from my wallet. Decrease my money variable by one. 

What happens if the machine does step one and then it crashes? It never finished. So it added a dollar to you but didn't take a dollar from me. We've just duplicated a dollar.

You might think you could reverse the order, but that doesn't help. If we do it this way:

    1.Remove $1 from my wallet. 

    2. Add $1 to your wallet 

If we crash between steps one and two, a dollar vanishes to the twilight zone! That's not any better.

Such a trade is what computer scientists call an atomic action. We can't do just half of it and preserve a sensible situation -- that's what we mean when we talk about referential integrity, that the data is in a sensible state.

Transactional processing allows you to group multiple actions together and call them atomic, so that either they all happen or none of them do.

A sudden crash such as I described earlier is rare, but I used it as a simple illustration. Multithreaded code sometimes has what are called race conditions, which are bugs that result from doing two incompatible things at once. I can demonstrate a race condition by breaking the action down and adding a thief in the crowd while I'm giving you a dollar.

The action looks something like this:

    1. Get how much money I have as X. 

    2. Get how much money you have as Y. 

    3. If (X < 1) stop. I don't have any money to give. 

    4. Set your money to y + 1. 

    5. Set my money to x - 1. 

Let's say I only have one dollar in my wallet. The thief's pickpocket algorithm looks like this:

    * Get how much money I have as TX. 

    * Get how much money the thief has as TY. 

    * If (TX < 0), then stop. I don't have any money to steal. 

    * Set my money as TX - 1. 

    * Set thief's money as TY + 1. 

Each of these actions works well alone, but if they occur simultaneously, problems can arise. Let me walk through what happens to X,Y, TX, and TY when the two routines race.

Imagine I have one dollar in my wallet, everyone else has zero, and the following things happen:

    1. Get how much money I have as X. X now equals 1. 

        * Get how much money I have as TX. TX now equals 1.

    2. Get how much money you have as Y. Y now equals 0. 

        * Get how much money thief has as TY. TY now equals 0.

    3. If (X < 1), stop. X is 1, so I go on. 

        * If (TX < 0), then stop. TX is 1, so the thief continues.

    4. Set your money to y + 1. You now have one dollar. 

        * Set my money as TX - 1, I now have zero dollars.

    5. Set my money to x-1. X is still 1, so I get set to zero dollars. (again) 

        * Set thief's money as TY + 1. Thief now has one dollar.

At the end, I have zero dollars, but you and the thief each have one dollar, so there are now two dollars in the world. We just duplicated a dollar!

Transactions enforce isolation. They have rules to make sure races such as these can't happen. Race conditions are the number-one cause of dupe bugs.

Rollbacks
^^^^^^^^^

Q: Tell us about rollbacks in the context of online games.

A: A rollback is what happens when a game application fails during a game, causing players to lose some of their past play. For example, consider the classic EverQuest dragon. To take down a dragon, you and about 50 other players might have to beat the dragon for two or three hours. Imagine that you were part of a group that had been beating on a dragon for 90 minutes, only to have the server then fail. If the state was carried in the server's memory with no backup, then when the application was restored, the dragon would get all of its hit points back. Ninety minutes of play could have been destroyed, and you're back to square one. That's a rollback -- something that players hate.

Project Darkstar allows the entire virtual world to asynchronously persist back to a central server. It's possible to lose up to a second or two of game play, due to the asynchronous nature of the data that is saved. That's a small price to pay for performance. You shouldn't ever lose 20 minutes or two hours worth of work.

It's important to understand the state of the industry today. Load balancing is performed in a primitive fashion in which worlds are broken into what are called zones, areas of space in the virtual world. So the town of Foo or the forest of Bar might be zones on different physical servers. In the town of Foo, you connect to the server of the town of Foo. When in the forest of Bar, you connect to that particular server.

This would be a perfect load-balancing scheme if people spread themselves evenly across the virtual world -- but they don't. People are social and tend to clump together, and the spaces become overloaded and laggy, while other spaces are sitting idling and unused. And if everyone's in the town of Foo, and the town of Foo crashes, you're out of the game. In the worst case, you're stuck until the town of Foo's server comes up.

Some games, after a certain period of time, will move you somewhere else in the game after a crash, so you can get back in the game, but you still can't return to what you were doing.

With Project Darkstar, all the data in the virtual world is held in what we call the data store, which you can think of as a persistent cloud of objects that exists above the servers.

Players are assigned a seat on a server. As they pick up an object or fight a creature, the data comes down to their server from the data manager and data store. The idea is that if that server fails, we can reconnect them to another server, because the servers have no state. The state is all in the cloud. The cloud is probably the most whiz-bang "researchy" thing in the Project Darkstar system and the focus of much of our ongoing R&D.

Essentially, what we're building is a transactional database tuned for massive scalability at a 50 percent read-50 percent write data load. And of course, like any back-end database, the Project Darkstar data store will also be made highly available.

Many databases can scale up, and some are even quite fast, but most of them scale through replication, which is duplication of the data across multiple servers. This scheme assumes that data is mostly read and seldom written. That's not our case, so we've had to research our own solutions to the problem.

The data store is a transactional database, but it's not a relational database. We do no querying, so we don't need SQL or any other query support. All our access is based off of primary keys. It's simply a very fast place to read and write data in a transactional manner.



+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| "The cloud is probably the most whiz-bang 'researchy' thing in the Project Darkstar system and the focus of much of our ongoing R&D.; Essentially, what we're building is a transactional database tuned for massive scalability at a 50% read-50% write data load." |
|                                                                                                                                                                                                                                                                      |
| -- Jeff Kesselman - Chief Instigator, Project Darkstar, Sun Microsystems                                                                                                                                                                                             |
+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+



Q: How does rollback protection differ from disaster protection?

A: Two situations can potentially cause a rollback: failures and disasters. When an individual server goes down, which is a failure, Project Darkstar can completely hide it. At most, players will see a little more load on the games because they're running on one less server.

Disaster refers to the entire machine room going down. Project Darkstar has a real database back end that saves a historically accurate record of the game up to a couple of seconds before it went down. So even if we lose the machine room, once the machine room is restored, we can still bring the game back up, without losing anything except a second or two.

Q: No other technology on the market offers this?

A: Game developers, by and large, are not server developers, so they focus on their clients. They generally attend minimally to what's needed on the server side -- just enough to make sure their game will work. We're bringing Sun's considerable knowledge and expertise in scalable network systems to the online multiplayer game industry. Nobody else in the game industry has that expertise, and nobody else is approaching online game development with that focus.



+----------------------------------------------------------------------------------------------------------------------------------+
| "We're bringing Sun's considerable knowledge and expertise in scalable network systems to the online multiplayer game industry." |
|                                                                                                                                  |
| -- Jeff Kesselman - Chief Instigator, Project Darkstar, Sun Microsystems                                                         |
+----------------------------------------------------------------------------------------------------------------------------------+



Shardless Architecture
^^^^^^^^^^^^^^^^^^^^^^

Q: Project Darkstar enables a shardless architecture. Why is that important?

A: As I said earlier, load balancing is performed in today's massively multiplayer online games through breaking worlds into zones, which are areas of space in the virtual world, like the town of Foo or the forest of Bar. 

Developers build clusters of zone servers, each of which serves one or more zones, and call that a shard, which game developers and players both think of and refer to as servers. So when you start a game, you choose a server -- a shard -- to start your character on.

So when I play in City of Heroes, I choose the Virtue server to start my character on, but I have friends who play on other shards, so we can't play together, which severely limits the number of players who can interact. Shards split up the user base, which really hurts the networking effect.

Each shard has a limit on the number of players it can support simultaneously. This puts a hard limit on the number of players who can play together. Each shard is its own dedicated cluster and cannot use resources from other shards to extend its own capacity, even if they are sitting idle, which wastes server resources.

What's further challenging is that each shard has to be overbuilt by an order of magnitude because the vast majority of the time you have 5 percent to 10 percent of your total shard's user population online at once. But if you only built out for this small number, you would invite trouble because during critical times in a game's life, generally referred to in the industry as events, which are promotional events like Halloween or Christmas parties, 90 percent of your users could be online at once. If you can't handle that, your customers become unhappy. Games have failed in the market because they were underbuilt.

Project Darkstar changes the economics. Games no longer need to be split up. We will run shardless in one instance of the game world, so everyone with an account can play together. Furthermore, we can share resources on the back end across multiple games. Promotional events are driven by deliberate developer actions and are thus highly predictable. A Darkstar machine room can have a single pool of event servers that any game in that room can use.

Q: How many players could Project Darkstar potentially accommodate?

A: That will depend on many factors that will be specific to each game. Given the loads that we generally expect, though, we believe that Project Darkstar can accommodate thousands of players on a machine.

Making Better Games
^^^^^^^^^^^^^^^^^^^

Q: So how can Project Darkstar facilitate developers in creating better games?

A: Many game developers don't focus on persistence because they generally are inexperienced with databases. So all they persist is the player characters and information about them. The rest of the world is in memory and must remain the same from a restart. For instance, if you stand around, you'll notice an odd effect when playing Matrix Online, in which doors close autonomously. You'll watch a door that's been open for a few minutes shut itself. They do this because when they restart from ground zero, all the doors are closed, and they want it to be as close to that as possible. So they force the doors closed to make it easier to restart. 

Persistence in Project Darkstar is under the hood and automatic, so everything that the developer writes is persistent. Every monster, every door, everything is automatically persisted by the system. Without this kind of persistence, certain kinds of game play are simply not possible.

But with Project Darkstar, now I can, for instance, build a castle and know that the castle will be present even if the server or whole back end goes down. One problem with games today is that players feel more like spectators than participants. Structures and entities remain static because they can't create games that grow and develop. We're going to change all of that.

Imagine a game in which you are an explorer or trader. By moving goods, you affect the state of the world. For example, farms appear near a town because you're bringing in more farm implements. Now let's say you get tired of trading and want to start a town of your own. You clear the land of monsters, and over time it becomes a safe area. You cut down the trees, create farm land, and build structures. Eventually you get someone to haul rocks to your land with which to build a castle. You raise an army and become a warlord.

Meanwhile, the monsters you ran out of your area have been forced into overpopulation nearby. Because there isn't enough game for them all, they go through behavioral evolution and selective breeding, and after many generations become much tougher and smarter. They return to see if they can take back the land.

None of this is rocket science. We know how to mathematically model economies and populations today. We know how to build genetic artificial intelligence that evolves. But all of this depends on the game having a memory. Imagine you went through all the changes described earlier, became a fierce warlord, and then the server crashed, and when it came back up, all the doors were closed. All the changes you made to the world were gone!

I don't think you'd play that game much after that. We play to be entertained, not to become frustrated.

The Project Darkstar Playground: A Hosted Game Server Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Q: What's the Playground?

A: The Playground is an online game hardware and software infrastructure that we're making available to selected game developers that include some very well-known names as well as some exciting new faces. I can't name names yet due to confidentiality issues, but it's a very exciting list. 

The Playground provides these developers with an environment that they can use to test the scalability of their online games. It gives us the opportunity to work closely with these developers too, so that we can use real games to help us with our own benchmarking and performance analysis work.

The Playground offers a taste of what we envision for the industry, which is hosting providers that take the load in building and running the game room off of the shoulders of the developer.



+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| "The Playground offers a taste of what we envision for the industry, which is hosting providers that take the load in building and running the game room off of the shoulders of the developer." |
|                                                                                                                                                                                                  |
| -- Jeff Kesselman - Chief Instigator, Project Darkstar, Sun Microsystems                                                                                                                         |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+



Not Just for Java Programmers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Q: Is Project Darkstar only for Java programmers?

A: On the server side, the game-specific code that will run on top of the Project Darkstar server has to compile down to the JVM* byte code. We assume that the game's server-side logic will be written in Java code for various reasons, but many languages compile down to the JVM, from Python to C compilers. So theoretically, developers can code their game logic in any of these languages. 

We are agnostic on the client side. As a group, we have a Java SE API and a C API we've just finished, and we're doing a Java ME API as well.

We hope to see the community build more APIs for the system. One community group has already built a Flash API to share with others. We ultimately want to support as many kinds of clients as people want to write games for.

The Future of Project Darkstar
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Q: Where do you think Project Darkstar is headed?

A: We've been thrilled with the response to date. Most major players or would-be major players in this space are talking with us. It's an exciting time. We are very optimistic. Project Darkstar creates a great opportunity for small players, who could not afford to compete in this space, to come into the game, as well as a way for big players to do more with smaller budgets. 

We think the result is going to be a renaissance in the online games market. Right now, all massively multiplayer online games pretty much play the same. That's because they are all chasing the same well-known, existing large markets. Today, it just costs too much to risk building games for unknown markets.

Darkstar will enable game developers to build massively multiplayer online games on smaller budgets that will be more risk-taking, more experimental, and ultimately will expand the market into entirely new areas.

All of which will be great for Sun!