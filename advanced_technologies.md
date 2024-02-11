# CSC8503 - Advanced Game Technologies

---

This project includes the tutorials and coursework submission for the CSC8503 - Advanced Game Technologies module at Newcastle University.

A small heist game was created, using C++.

The aim of the game is to explore the maze, collect orbs, avoid enemies and steal an item (the golden goat!). Return the goat to your starting position to win.


Code for this whole project [can be found here.](https://github.com/AdSand/CSC8503)

Key files:

[Game code](https://github.com/AdSand/CSC8503/blob/master/CSC8503/TutorialGame.cpp)

[Behaviour tree and pathfinding](https://github.com/AdSand/CSC8503/blob/master/CSC8503/AStarEnemy.cpp)

[State Machine](https://github.com/AdSand/CSC8503/blob/master/CSC8503/EnemyStateObject.cpp)

[Main - game mangement and pushdown automata](https://github.com/AdSand/CSC8503/blob/master/CSC8503/Main.cpp)

---

## Implemented Features

#### Physics

##### Collision detection
Ray - Capsule collision. This used ray - plane collision detection to find the closest point on a line representation of the capsule, and creating a temporary sphere volume at that position. Then running ray - sphere, it can be determined if the ray is hitting the capsule.

<p align="center">
<img src="images/AdvancedGames2.png?raw=true"/>
</p>

Sphere - OBB. This was implemented by creating temporary AABB and sphere tranforms and volumes, and running AABB - Sphere detection, with the sphere tranform oritentation set to that of the AABB. This collision was used to create ramps in the game.

<p align="center">
<img src="images/AdvancedGames1.png?raw=true"/>
</p>

##### Grapple Hook

Using ray casting and forces, I implemeted a grapple hook into the game. The grapple hook will lock onto the centre of the object that is in front of the player, and pull them towards it.

<p align="center">
<img src="images/AdvancedGames3.png?raw=true"/>
</p>

##### Tag System

I created a tag system that could be used to trigger different game actions, depending on the tag of the other object in the collision.

Each game object has a tag associated to it that is set in the constructor of the game object.

Some game objects, such as the player, use inheritance so that their OnCollision functions can be overwritted. At this point, the tag of the object collided with can be checked, to perform some action.

Here is some example code of a key detecting if the player (tag = 1) has collided with it, and if so, opening the connected door.
```C++
void OnCollisionBegin(GameObject* otherObject) override {
	if (otherObject->GetTag() == 1)
	{
		linkedDoor->GetTransform().SetPosition(linkedDoor->GetTransform().GetPosition() + Vector3(0, 8, 0));
		linkedDoor->GetRenderObject()->SetColour(Debug::GREEN);
		g->RemoveGameObject(this);		}
	}
```

##### Constraints

I create a hinge constrain that allowed for gates to be added in the game. The gates are able to move in a full 360 range, but will not change their y-position in the world. They will also remain at a constant distance from the gate posts.

<p align="center">
<img src="images/AdvancedGames11.png?raw=true"/>
</p>

```C++
void HingeConstraint::UpdateConstraint(float dt) {

	Vector3 direction = (objectA->GetTransform().GetPosition() - objectB->GetTransform().GetPosition()).Normalised();
	float newAngle = RadiansToDegrees(atan2f(-direction.z, direction.x));

	objectA->GetTransform().SetOrientation(Quaternion::EulerAnglesToQuaternion(0, newAngle, 0));
	objectB->GetTransform().SetOrientation(objectA->GetTransform().GetOrientation());

	Vector3 temp = objectA->GetTransform().GetPosition();
	temp.y = objectB->GetTransform().GetPosition().y;
	objectA->GetTransform().SetPosition(temp);
}
```



---

#### AI / State Machines

##### Simple state machines
State machine enemies that will patrol the world until the player is nearby. If player is within a certain distance, they will chase the player.

<p align="center">
<img src="images/AdvancedGames4.png?raw=true"/>
</p>

##### Behaviour Tree

Behaviour tree goose enemy using different selectors and sequences.

It has a root that will select between a sequence for chasing the player, or a selection for waiting for the player. While waiting for the player to grab the heist item, it will select between changing colour or facing the direction of the player.

<p align="center">
<img src="images/AdvancedGames5.png?raw=true"/>
</p>

##### Pathfinding

When the player grabs the item the chase sequence will run, updating the path finding.
The goose enemy will then chase the player using A* pathfinding, recalculating the path only when the player enters a different node on the graph. The enemy will also destroy anything in its path, removing it from the world.

An improvement to the pathfinding would be to use forces to move the enemy, instead of setting the position. This would eliminate possible errors in collision detection.

<p align="center">
<img src="images/AdvancedGames6.png?raw=true"/>
</p>

##### Pushdown Automata

Pushdown Automata was used to create the menu system, with appropriate states for each section of the game.

The game has a main menu, with different options to select from. The game can also be paused and unpaused.

<p align="center">
<img src="images/AdvancedGames7.png?raw=true"/>
</p>




---

#### Networking
##### Client - server high score table
The game can be started in single player, as a server or as a client.

Starting as a server will clear the current leader-board file, ready to store high scores.

<p align="center">
<img src="images/AdvancedGames8.png?raw=true"/>
</p>

When a client finishes the game, the score is sent in a packet to the server. The server receives the packet and writes the score to the high score file. Client players can send a request packet to the server, asking for the high score. The server will then return a packet with the score to the individual client that sent the request (not broadcasting to all connected clients).

Multiple clients can join the server to share the same leader board (currently set to four maximum).

<p align="center">
<img src="images/AdvancedGames9.png?raw=true"/>
<img src="images/AdvancedGames10.png?raw=true"/>
</p>

With longer to work on the project, I would have liked to implemented a full multiplayer mode, with players simulatenously in the same game world. This project emphasised to me the importance of considering networking from the start of the project - and the difficulties of trying to add networking at a later stage of the coding.

---

*Click the image below to view on YouTube.*


[![YouTube link to video](https://img.youtube.com/vi/dKY4Tihnjyg/0.jpg)](https://www.youtube.com/watch?v=dKY4Tihnjyg)
