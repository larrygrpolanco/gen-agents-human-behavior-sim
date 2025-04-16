# Reverie: Generative Agent Human Behavior Simulation

## Overview
Reverie is a simulation framework for generative agents that models human-like behavior through cognitive architectures powered by large language models. Based on the research paper "Generative Agents: Interactive Simulacra of Human Behavior", this system creates autonomous agents that perceive, plan, act, remember, reflect, and interact in a simulated environment.

## System Architecture

### Backend Server
The core simulation engine that powers the agents and environment:

- **reverie.py**: Main simulation controller
- **maze.py**: Environment representation with locations and objects
- **path_finder.py**: Navigation system for agent movement
- **global_methods.py**: Utility functions used throughout the system

### Persona System
The cognitive architecture for generative agents:

- **persona.py**: Core agent class that integrates all cognitive modules
- **Cognitive Modules**: Functions that mimic human cognitive processes
  - **perceive.py**: Environmental perception and attention
  - **retrieve.py**: Memory access and relevance calculation
  - **plan.py**: Schedule generation and action planning
  - **execute.py**: Action implementation and movement
  - **reflect.py**: Insight generation and memory processing
  - **converse.py**: Inter-agent communication

- **Memory Structures**: Components that store agent knowledge
  - **associative_memory.py**: Long-term episodic and semantic memory
  - **spatial_memory.py**: Knowledge of the physical environment
  - **scratch.py**: Working memory for current state and activities

- **Prompt Templates**: Language model prompts for generating behavior
  - **v1/**, **v2/**, **v3_ChatGPT/**: Different versions of prompts
  - **safety/**: Guidelines for appropriate agent behavior
  - **run_gpt_prompt.py**: Interface with language models

### Utility Components
- **compress_sim_storage.py**: Optimizes simulation data for replays
- **test.py**: Testing framework for simulation components

## How It Works

### Agent Lifecycle
1. **Perception**: Agents observe nearby events and objects
2. **Memory Retrieval**: Relevant memories are accessed based on current context
3. **Planning**: Agents create daily schedules and next actions
4. **Execution**: Plans are translated into movements in the environment
5. **Reflection**: Experiences are processed to generate insights
6. **Conversation**: Agents interact with each other through dialogue

### Memory Systems
- **Associative Memory**: Stores events, thoughts, and conversations with importance scores
- **Spatial Memory**: Tracks knowledge about the environment's layout
- **Scratch Memory**: Maintains current state, plans, and immediate context

### Planning Mechanisms
- **Daily Planning**: Morning routine, work schedule, leisure activities
- **Task Decomposition**: Breaking large activities into specific steps
- **Action Selection**: Choosing appropriate locations and objects
- **Social Interaction**: Deciding when to talk to other agents

## Key Features

- **Autonomous Behavior**: Agents function independently without direct control
- **Memory Persistence**: Experiences influence future decisions
- **Poignancy Mechanism**: Emotional importance affects memory retrieval
- **Social Dynamics**: Agents form relationships and have conversations
- **Reflection System**: Agents generate insights about their experiences
- **Language Model Integration**: Uses LLMs to generate human-like behavior

## Technical Implementation

- **Environment**: Structured as a grid-based world with locations and objects
- **Agent Cognition**: Implemented through a modular system of Python functions
- **Memory**: Stored as embeddings and structured data for efficient retrieval
- **Planning**: Generated through language model prompts with contextual information
- **Interaction**: Agents can perceive each other and engage in conversations
- **Simulation Control**: Time progression and event management in reverie.py

The system demonstrates how large language models can be integrated into cognitive architectures to create autonomous agents that simulate human-like behavior in complex environments.