# Simulation Architecture

## Overview

This project is inspired by the "Generative Agents" research codebase, but is reimagined for a simulation game that is easy to run, modify, and enjoy—no research lab required. The goal: create believable social agents in a paper office, with a strong focus on both agent behavior and visual presentation, but without the complexity and technical barriers of the original system.

---

## 1. The Original Architecture: Strengths and Weaknesses

### What Works Well

- **Agent Architecture:**  
  The original code's `Persona` class (see `reverie/backend_server/persona/persona.py`) models agents with a cognitive loop:  
  - `perceive` → `retrieve` → `plan` → `execute` → `reflect` → `move`  
  This loop enables rich, believable behaviors and is a great foundation for your own agents.

- **Frontend Presentation:**  
  The use of Phaser (see `main_script.html`) and a Tiled-designed map creates a visually appealing, game-like environment. The tilemap, sprites, and animation system are all strong points.

### What Gets in the Way

- **Two-Server Split:**  
  The original system separates the simulation backend (Python) and the frontend (Phaser/JS), communicating via JSON files and HTTP endpoints. This was likely for research modularity, but it adds complexity and makes the system harder to run and modify.

- **File-Based Communication:**  
  The backend and frontend exchange state via files, which is slow and brittle for a game. This is fine for research, but not for a user-friendly simulation.

- **Over-Engineered for Research:**  
  Many abstractions (e.g., step/phase loops, meta files, forking simulations) are designed for experiments, not for gameplay or ease of use.

---

## 2. A Simpler, Game-Oriented Architecture

### Your Use Case

- **Single Server:**  
  Run both the backend (Python agent logic) and the frontend (Phaser) from a single Python server (e.g., Flask, FastAPI, or even a simple websocket server).
- **Live Communication:**  
  Use websockets or REST APIs for real-time updates between backend and frontend, instead of file-based JSON.
- **Lay User Focus:**  
  Make the game easy to launch (e.g., `python app.py`), with minimal setup and clear instructions.

### Recommended Structure

#### Analogy

- **The Director and the Stage:**  
  - The Python backend is the *director*, deciding what each agent does.
  - The Phaser frontend is the *stage*, animating the agents and environment.
  - Communication is a *walkie-talkie* (websocket/API), not a pile of letters (files).

#### Suggested Flow

1. **Frontend (Phaser):**
   - Loads the map (Tiled JSON), sprites, and UI.
   - Renders agents and listens for user input (if any).
   - Requests agent updates from the backend at regular intervals or in response to events.

2. **Backend (Python):**
   - Maintains the state of all agents (using a class like `Persona`).
   - On each tick or request, runs the cognitive loop for each agent:
     - `perceive` the environment
     - `plan` and `decide` next action
     - `move` and update state
   - Sends updated agent positions and actions to the frontend.

3. **Communication:**
   - Use a websocket (e.g., Flask-SocketIO, FastAPI with websockets) for real-time, bidirectional updates.
   - Alternatively, use REST endpoints for simple polling.

#### Example File Structure

```
/app.py                # Python server (Flask/FastAPI)
  /agents/
    persona.py         # Persona class (agent logic)
  /static/
    /js/
      main.js          # Phaser game logic
    /assets/           # Tileset, sprites
  /templates/
    index.html         # Loads Phaser and connects to backend
  /maps/
    office_map.json    # Tiled map
```

---

## 3. Key Concepts to Keep

### Agent Architecture

- **Persona Class:**  
  Keep the cognitive loop from the original `Persona` class, but simplify as needed.  
  - Example:  
    ```python
    class Persona:
        def perceive(self, world): ...
        def plan(self): ...
        def act(self): ...
        def move(self): ...
    ```
- **Believability:**  
  Focus on simple, readable logic for agent decisions. You can always add complexity later.

### Frontend Presentation

- **Phaser + Tiled:**  
  Use Tiled to design your office map, export as JSON, and load in Phaser.
- **Sprites and Animation:**  
  Start with simple placeholder sprites; polish later.
- **UI/UX:**  
  Make controls and feedback clear for non-technical users.

### Communication

- **Websockets for Real-Time:**  
  This allows the frontend to send/receive updates instantly, making the simulation feel alive.
- **REST for Simplicity:**  
  If real-time isn't needed, simple polling works too.

---

## 4. What to Avoid

- **File-Based State Exchange:**  
  Don't use files to pass state between backend and frontend.
- **Over-Abstracted Phases:**  
  Unless you need to run experiments, keep the update loop simple.
- **Research-Driven Complexity:**  
  Only add features you need for gameplay and user experience.

---

## 5. References in the Original Code

- **Agent Logic:**  
  - `reverie/backend_server/persona/persona.py` (`Persona` class)
- **Simulation Loop:**  
  - `reverie/backend_server/reverie.py` (`ReverieServer`)
- **Map and Collision:**  
  - `reverie/backend_server/maze.py` (`Maze` class)
  - `environment/frontend_server/templates/home/main_script.html` (Phaser map setup)
- **Frontend Animation:**  
  - `main_script.html` (`preload`, `create`, `update`)

---

## 6. Roadmap for Your Project

1. **Prototype the Map and Agents:**
   - Build a simple Phaser map with a few agents.
   - Hardcode agent movement or use random walks to start.

2. **Implement the Agent Loop in Python:**
   - Port or adapt the `Persona` class.
   - Run the cognitive loop on each tick.

3. **Connect Frontend and Backend:**
   - Use websockets or REST to send agent positions/actions to the frontend.

4. **Iterate and Polish:**
   - Add more agent behaviors.
   - Improve visuals and UI.
   - Playtest for usability.

---

## 7. Example: Minimal Agent Update Flow

**Python Backend (Flask-SocketIO):**
```python
@socketio.on('request_update')
def handle_update():
    # Run agent logic
    update_agents()
    # Send new positions to frontend
    emit('agent_update', {'agents': agent_states})
```

**Phaser Frontend:**
```js
socket.on('agent_update', (data) => {
  // Update agent sprites with new positions
});
```

---

## 8. Final Advice

- **Start simple, iterate fast.**
- **Prioritize user experience and ease of setup.**
- **Keep the agent architecture modular for future expansion.**
- **Use the original codebase for inspiration, not as a blueprint.**

---

**You are building a simulation game, not a research platform.**  
Focus on fun, believability, and accessibility!
