# Kayak game

https://github.com/user-attachments/assets/1634c2b0-9b6f-4e23-bdf6-1d967aa9383c

### Description:
This is a kayak racing game set in space, where players race on a track they've likely never seen before — a long trail of floating water with waves. Players can ride up waves and soar through the sky before crashing down on the water with a speed boost. I started this personal project after taking inspiration from Rainbow Road in the Mario Kart series and the manta ray race in Mario Galaxy.

### Features:
- Procedural waves that affect not only the visual appearance but also the actual interaction with the player
- Toon shading with multiple light sources
- Physics simulation of buoyancy

### Challenges:
The biggest challenge I faced during development was creating the wave system. The original mesh of the track has no waves, and the vertices need to be displaced to create procedural waves. I used shader graph to create the procedural waves through noise functions. This gave the track waves; however, it was only visual, as shaders don't affect the colliders on the mesh. I tried extracting the vertex data in the shader onto a C# script so I could modify the collider on the track, but this was not possible. I believe the reason for this is that it's difficult to move data from the GPU to the CPU, and the shader runs after C# scripts.

After a couple of weeks, I realized that I could replicate the transformation done on each vertex in shader graph on my C# script to find the position of the wave, and what's better is that I don't have to update the collider mesh or even have a collider at all on my wave, which saves performance. This is because the buoyancy physics is simulated by sampling how deep in the water several points of the kayak are. For a given buoyancy point, I first found the closest point on the surface of the track mesh, then applied the same transformation that my shader did to get the true height. This allowed me to find how deep that buoyancy point is underwater.

<img width="50%" alt="image" src="https://github.com/user-attachments/assets/b869b06c-f602-41f9-8269-981cde2388dd" />

Diagram of how the depth of a buoyancy point is found.

Since the shader was created through shader graph, I had to translate the shader graph into hlsl code to see how noise is calculated. Then I translated that into C# so I can make a function that takes any mesh point and returns their transformed position.

<img width="1480" height="727" alt="image" src="https://github.com/user-attachments/assets/40d7fd43-206c-4e43-b42f-d50d6bb7085e" />
Photo of the track model in Blender.

### Game engine: Unity
### State: Incomplete prototype

# First mobile game

<img width="1614" height="904" alt="image" src="https://github.com/user-attachments/assets/3f7fe5a6-ad5a-4bf5-8341-6a1906a6502c" />

https://github.com/user-attachments/assets/3cc85c46-ea79-4cac-a4ae-d5479fbfdb36

### Description:
My first mobile game involved a character that could slam the ground to create rocks. The rocks can be used as a barrier to keep enemies away, or they can be hit to damage enemies. After each wave of enemies, a selection of stackable upgrades appears that increase survivability. Players need to swipe swiftly, make quick decisions, and use stamina wisely to keep enemies away.

The upgrades include:
- Stamina regeneration
- Knock-back
- Rock health
- Max health
- Piercing
- Double rock

### Features:
- Modular upgrade system to facilitate creation of new upgrades
- Smooth swipe controls

### Challenges:
I wanted to create a modular upgrade system that is easily scalable and manageable. Simply creating an upgrade script that handled the logic for each individual upgrade will quickly become difficult to debug and extend. By utilizing scriptable objects, I can state what every upgrade needs to define and save them in the project folder to be used by several scripts.

Things to define in an upgrade:
- Name
- Description
- Sprite
- Function to apply

Doing this separated the implementation of each upgrade from other scripts that made the system much cleaner and easier to handle.

### Game engine: Unity
### State: Incomplete prototype

# Climate manager
<img width="315" height="250" alt="Coverimage" src="https://github.com/user-attachments/assets/57a5a6ad-37e1-4a9a-984f-e1feec86b7a6" />
<img width="1920" height="1080" alt="unknown" src="https://github.com/user-attachments/assets/49e87a64-dfff-421a-8681-6df7eadb1592" />

### Description:
This game was created in 2 weeks for a game jam (an event where people gather to make games from scratch within a set time limit). The premise is to keep the population happy by controlling the weather using your mouse. Throughout the game, requests for certain weather will pop up. For example, rainy, sunny, windy, or snowy. You need to fulfil those requests to keep the satisfaction meter high. Once it hits 0%, the game is over.
The game can be played through this link (https://junbo.itch.io/climatemanager).

### Features:
- Cloud mechanic: By hovering the sun over water, clouds will appear that can be moved around using the mouse. These clouds are essential in fulfilling certain requests, such as rainy or snowy. Having the sun close to the cloud turns it into a rain cloud, and having it away turns it into a snow cloud.
- To increase the difficulty, satisfaction will start to deplete more quickly, and wind will blow occasionally to push clouds into undesirable locations.

### Challenges:
Since this was a game jam, I only had 2 weeks to complete the game, so time had to be managed wisely. After brainstorming ideas, I noted down things I needed to complete on Trello to prioritize tasks required for a minimum viable product. By doing this, I was able to stay on track, avoid scope creep, and complete the game on time. There are still many rooms for improvement, as the game lacked a proper tutorial and contained no audio.

### Game engine: Unity
### State: Completed
