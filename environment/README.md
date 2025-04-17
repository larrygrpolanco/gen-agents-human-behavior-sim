# Generative Agents Human Behavior Simulation Environment

This directory contains the environment for simulating and visualizing generative agents that mimic human behavior. The system implements the architecture described in the research paper "Generative Agents: Interactive Simulacra of Human Behavior."

## Overview

The environment consists of a Django-based web application that visualizes AI agents in a virtual world called "The Ville." These agents have cognitive architectures with memory, planning, and decision-making capabilities that allow them to simulate realistic human behavior.

## Directory Structure

- `frontend_server/` - Django web application for visualization
  - `frontend_server/` - Core Django configuration
  - `translator/` - Controller layer for the visualization
  - `templates/` - HTML templates for the user interface
  - `static_dirs/` - Assets like images, CSS, and character data
  - `storage/` - Complete simulation data
  - `compressed_storage/` - Optimized simulation data
  - `temp_storage/` - Temporary simulation data

## Key Features

- **Agent Visualization** - 2D game-like interface showing agent movements and interactions
- **Conversation Simulation** - Agents can converse with each other based on their memories and goals
- **Memory System** - Agents maintain memories with importance-based recall
- **Planning and Decision Making** - Agents create plans and make decisions based on their goals
- **Replay System** - View and analyze recorded simulations

## How It Works

1. Agents are initialized with personas, memories, and goals
2. The simulation runs in timesteps, with agents making decisions at each step
3. Agent decisions are translated into movements and interactions
4. The visualization system renders these as animations in the web interface
5. Agent memories are updated based on their experiences
6. Users can observe, replay, and analyze agent behavior

## Getting Started

1. Install requirements: `pip install -r frontend_server/requirements.txt`
2. Run the Django server: `python frontend_server/manage.py runserver`
3. Access the interface at `http://localhost:8000`

## Simulation Data

The system includes pre-recorded simulations in `storage/` and `compressed_storage/`, organized by simulation run identifiers (e.g., `July1_the_ville_isabella_maria_klaus-step-3-10/`). These contain complete records of agent positions, movements, and cognitive states throughout the simulation.

## More Information

For more details on the generative agents architecture, refer to the paper:
"Generative Agents: Interactive Simulacra of Human Behavior"