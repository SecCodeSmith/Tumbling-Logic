# TumblingLogic

## Project Overview
TumblingLogic is a 3D grid-based logic puzzle game developed in Unreal Engine 5 using a hybrid architecture of C++ and Blueprints. The game is heavily inspired by classics like Bloxorz and Devil Dice.

## Core Gameplay & Mechanics

### Grid-Based Movement
The game relies on a strict X/Y coordinate grid. Characters do not use physics-based rolling; instead, they move by pivoting 90 degrees on their bottom edges to snap to adjacent tiles.

### Player Entities
* **Standard Cube:** A 1x1x1 Cube.
* **Block:** An irregular 1x1x2 Block (takes up 2 tiles when lying flat, 1 tile when standing upright).
* **Multiple Actors:** Support for multiple actors on the grid at once, with the player able to switch control (possess) between them.

### Level Mechanics
* **Target Hole:** A hole the block must fall into to complete the level.
* **Face Tracking:** Specific face tracking (e.g., the cube must land on a specific tile with the red face pointing up).
* **Fragile Tiles:** Safe when the 1x1x2 block lies flat and distributes weight, but breaks if it stands upright on it.
* **Interactables:** Buttons and bridges.

## Technical Architecture (The Hybrid Approach)

### C++ (The Brain)
All core logic, mathematics, state tracking, and grid management are handled in C++. This includes:
* Validating if a move is legal (checking bounds, holes, obstacles).
* Tracking the entity's orientation (standing vs. lying).
* Calculating the pivot point for the 90-degree rotation.
* Managing the active faces.

### Blueprints (The Body)
C++ classes are exposed to Blueprints using `UCLASS()`, `UPROPERTY()`, and `UFUNCTION(BlueprintCallable)`. Blueprints are responsible for:
* Visual interpolation (using Timelines for smooth 90-degree rotation animations).
* Playing sounds and particle effects.
* Assigning static meshes and materials.

## Current State & Next Steps
We are setting up the foundational C++ classes. The main entity will likely inherit from `APawn` (or `AActor` controlled by a custom `APlayerController`).

## Instructions for the Agent
* **Clean & Optimized:** Prioritize clean, optimized C++ code for Unreal Engine.
* **Expose to BP:** Always use appropriate Unreal Engine macros (`UPROPERTY`, `UFUNCTION`) to expose necessary variables and functions to Blueprints.
* **No Hardcoding:** Avoid hardcoding visual or audio assets in C++; leave those exposed for Blueprint implementation.
* **Coordinate Systems:** When providing movement or math logic, account for the difference between the visual 3D space (Unreal units) and the logical 2D grid space (Tile X, Tile Y).
