# Bloodmoon: Sylas

<p align="center">
  <strong>A single-player browser action game set in a gothic fortress beneath a red moon.</strong><br>
  Choose a hero, enter the campaign, fight demons, and try to clear each stage.
</p>

<p align="center">
  <img alt="Angular host" src="https://img.shields.io/badge/Angular-app%20host-DD0031?logo=angular&logoColor=white">
  <img alt="React runtime" src="https://img.shields.io/badge/React-game%20and%20builder-149ECA?logo=react&logoColor=white">
  <img alt="Three.js and WebGL" src="https://img.shields.io/badge/Three.js-WebGL-111111?logo=threedotjs&logoColor=white">
  <img alt="Node and Express" src="https://img.shields.io/badge/Node.js-Express-43853D?logo=nodedotjs&logoColor=white">
  <img alt="MongoDB optional" src="https://img.shields.io/badge/MongoDB-optional-47A248?logo=mongodb&logoColor=white">
</p>

<p align="center">
  <img src="report_screenshots/23_complete_gameplay.png" alt="Actual Bloodmoon: Sylas gameplay with the hero, demons, fortress, and HUD" width="100%">
</p>

I developed this during my B.Tech 4-1 semester as a semester examination project. I built it while learning web technologies and working within the time and technology limits of a semester project.

## How I built it

I used an AI-assisted, iterative workflow often called **vibe coding**. I described a feature, used AI tools to help draft or change code, ran the game, looked at what happened, and then refined the instructions and implementation. I made the project decisions, reviewed the results, tested the game by playing it, and kept working on the parts that did not behave as intended. AI assistance was part of the process; it did not replace understanding or checking the code.

## What I learned about myself

I learn best when I can try an idea and see the result. During this project, I kept testing the game, noticed when the controls or characters did not feel right, and looked for ways to improve them. Some problems took more than one attempt, especially making image-based heroes and demons feel active. Working through those problems helped me practise patience and become more confident about trying unfamiliar things. I am still learning, but this project shows that I am curious about building and willing to keep improving when something is challenging.

One of my biggest challenges was creating heroes and demons. My project technologies did not include a full 3D modelling and character-rigging workflow, and that would have been too much to build within the semester. I chose pixel-art images for the characters instead.

A still image by itself cannot walk or fight. To make the characters feel active, the game places the pixel-art sprites in the 3D world and moves them through the game logic. The hero renderer changes the sprite's position and pose for actions such as walking, running, jumping, rolling, and attacking. It also flips the sprite when the hero changes direction. Three.js renders the sprite in the arena with shadows and other scene effects. The characters are still 2D artwork rather than fully modelled 3D figures, but this approach let me build an interactive game with the tools and time I had.

## Features

- Single-player campaign with 50 level and boss records
- Four selectable heroes with different stats, weapons, and abilities
- Gothic fortress courtyard rendered in the browser
- Keyboard and on-screen controls
- Demon movement, attacks, projectiles, and boss encounters
- Health, stamina, quest, enemy, radar, and combat information in the HUD
- Souls, level rewards, shrines, and chests
- Play, Builder, and Hybrid workspace modes
- Builder controls for the arena, combat settings, enemy waves, and live telemetry
- Game settings for camera view, language, sound, radar, and attack warnings
- Optional sign-in, registration, and guest entry

The project contains 50 named boss records and signature-move descriptions. The runtime uses a smaller set of reusable boss attack patterns with variations; the records should not be confused with 50 completely unique boss combat systems.

## Technology stack

- **Main application:** Angular and TypeScript
- **Embedded game and builder:** React and React DOM
- **3D arena:** Three.js and WebGL
- **Server:** Node.js and Express
- **Database option:** MongoDB
- **Local server storage:** JSON file at data/game_db.json when MongoDB is not configured or cannot connect
- **Development and build:** Vite

The course subject introduced Mean Stack Web Technologies. The final project is an Angular-led hybrid application: Angular starts the app and manages its main screens, while the existing React game and builder remain embedded components. Node.js and Express provide the server, and MongoDB is optional. This is not a pure MEAN implementation because selected React components are part of the final build.

The game keeps settings and some campaign choices, such as the selected hero, unlocked level, and souls, in browser storage. The server includes account and game-related API routes, but the current frontend primarily connects to the server for registration, login, and guest entry. Full account-based game progress synchronization is not implemented.

## How the parts fit together

~~~mermaid
flowchart LR
    player[Player] --> app[Angular application]
    app --> game[React game canvas]
    app --> builder[React builder]
    game --> world[Three.js and WebGL world]
    builder -->|updates arena and combat settings| game
    app -->|registration, login, guest entry| api[Node.js and Express API]
    api --> mongo[(MongoDB optional)]
    api --> json[(Local JSON fallback)]
    app --> storage[(Browser localStorage)]
~~~

The builder and game share arena and combat settings. Campaign choices and preferences are kept in the browser. MongoDB is optional for the server's data store.

## Run locally

### Requirements

- Node.js 20.19 or newer in the 20.x series, or Node.js 22.12 or newer
- npm

### Start the development server

Open a terminal in the project folder and run:

~~~powershell
npm install
npm run dev
~~~

Open the local URL printed in the terminal. The default is http://localhost:3000.

MongoDB is optional for local play. Without a working MongoDB connection, the server uses local JSON storage.

### Build and checks

~~~powershell
npm run build
npm run lint
npm test
~~~

- **build** creates the production client bundle.
- **lint** runs the Angular/TypeScript compiler without emitting output.
- **test** runs the Academy curriculum and progress tests. The game runtime does not yet have a dedicated automated gameplay test suite.

### Optional MongoDB configuration

Copy .env.example to .env, then set MONGODB_URI and, if needed, MONGODB_DB. Keep real credentials private and never commit .env.

## Controls

| Action | Control |
| --- | --- |
| Move | W, A, S, D or arrow keys |
| Look around | Click the game view and move the mouse; press Esc to release the mouse |
| Run | Hold Shift |
| Jump | Space |
| Attack | J or the on-screen Attack button |
| Heavy attack | K or its on-screen button |
| Dash / roll | R or its on-screen button |
| Guard | Hold B or use the Guard button |
| Magic | E or the on-screen Magic button |
| Bloodmoon Fury | Q when charged or use the Fury button |
| Health potion | P or the potion button |
| Lock target | F or the Lock button |
| Pause / resume | Esc |

Movement is relative to the camera direction. On-screen controls can also be clicked or tapped.

## Project structure

~~~text
src/
  angular/       Angular app screens and the React integration bridge
  components/    React game canvas and builder
  data/          Boss records, lessons, and learning catalogue data
  services/      Three.js world, pixel animation, audio, and progress logic
  types/         TypeScript types and level configuration
public/assets/   Game artwork and audio
server.ts        Express server, API routes, and storage fallback
tests/           Cybersecurity Academy curriculum and progress tests
docs/            Student guide, project report, roadmap, and learning resources
report_screenshots/ Actual screenshots captured from the running game
~~~

## Screenshots

These are screenshots captured from the running game.

<table>
  <tr>
    <td align="center"><img src="report_screenshots/02_adventure_hub.png" alt="Adventure Hub" width="480"><br><strong>Adventure Hub</strong></td>
    <td align="center"><img src="report_screenshots/03_hero_selection.png" alt="Hero selection screen" width="480"><br><strong>Choose a hero</strong></td>
  </tr>
  <tr>
    <td align="center"><img src="report_screenshots/06_fortress_environment.png" alt="Fortress arena during gameplay" width="480"><br><strong>Fortress arena</strong></td>
    <td align="center"><img src="report_screenshots/22_enemy_defeat_result.png" alt="Level result screen" width="480"><br><strong>Level result</strong></td>
  </tr>
</table>

The full screenshot set is in the report_screenshots folder.

## Additional module in this repository

Hunter Camp also contains a separate, browser-local Cybersecurity Learning Academy. It has seven foundation records, a catalogue of 122 tools, and 12 project outlines. Complete 16-stage lessons are currently available for computer and operating-system fundamentals and Nmap; other learning units are marked in progress. Academy progress is stored in browser localStorage. The Academy does not run commands or inspect the student's computer.

## Limitations and future work

This is a learning prototype, not a production-hosted game. It is single-player and has no measured performance results or user-study results. Before public deployment, account security and authorization need more work, and the game should be tested across its intended browsers and devices.

Possible future improvements include more distinct boss behaviours, additional environments and characters, stronger account and save support, more gameplay tests, and expanded browser and device testing.

## Project documents

- [Student guide](docs/STUDENT_GUIDE.md)
- [Development roadmap](docs/DEVELOPMENT_ROADMAP.md)
- [Mini project report](docs/Project_Report.docx)
- [Cybersecurity Learning Academy overview](docs/Cybersecurity-Learning-Academy-Overview.pdf)
