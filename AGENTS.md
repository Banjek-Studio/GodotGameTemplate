# Godot Project Guidelines

## Build, Lint, and Test

### Run Project
- **Run Editor:** Open `project.godot` in Godot Engine v4.5+
- **Run Game:** F5 or Play button in editor
- **Run Specific Scene:** F6 or "Play Scene" button while scene is open

### Testing
- **Framework:** No dedicated testing framework (Gut/GdUnit) is currently installed.
- **Manual Testing:**
  - Run the project (`F5`) to test the main game loop.
  - Run specific scenes (`F6`) to isolate mechanics.
- **CI/CD:** GitHub Actions workflow (`.github/workflows/job_export.yml`) handles Linux/Wine export verification.

### Linting
- Use the built-in Godot script editor warnings.
- Ensure no errors/warnings in the "Debugger" > "Errors" tab during runtime.

## Code Style & Conventions

### General
- **Language:** GDScript (Godot 4.x)
- **Indentation:** Tabs (standard Godot convention)
- **Line Length:** ~100 characters generally acceptable, but no hard limit.

### Naming Conventions
- **Classes:** `PascalCase` (e.g., `GameState`, `LevelManager`)
  - Use `class_name` for globally accessible scripts.
- **Variables/Properties:** `snake_case` (e.g., `current_level_path`, `total_games_played`)
- **Functions:** `snake_case` (e.g., `get_level_state`, `set_checkpoint_level_path`)
- **Constants:** `SCREAMING_SNAKE_CASE` (e.g., `STATE_NAME`, `FILE_PATH`)
- **Private Members:** Prefix with `_` (e.g., `_load_current_state`)
- **Signals:** `snake_case` (standard Godot signal naming)

### Typing
- **Strong Typing:** STRONGLY RECOMMENDED. Use static typing for variables and return types.
  - Use `:=` for inferred typing where possible (e.g., `var game_state := get_or_create_state()`).
  - Explicitly state return types for functions (e.g., `-> void`, `-> String`).

### Project Structure
- `addons/` - Third-party plugins (Maaack's Game Template, Phantom Camera).
- `assets/` - Art, Audio, and other binary assets.
- `scenes/` - `.tscn` files organized by feature (e.g., `menus/`, `game_scene/`).
- `scripts/` - Core logic scripts, typically extending `Node` or `Resource`.
- `resources/` - Custom `.tres` resources.

### State Management
- Use `GameState` (singleton/static) for cross-session persistence.
- Patterns:
  - `get_or_create_state()` pattern for lazy initialization.
  - `GlobalState.save()` to persist changes immediately.

### Best Practices
- **Exports:** Use `@export` for inspector variables. Type them explicitly (e.g., `@export var level_states : Dictionary = {}`).
- **File Paths:** Use absolute `res://` paths for stability.
- **Safety:** Use `is_instance_valid()` or null checks before accessing node references, though strong typing helps avoid this.
- **Comments:** minimal, explanatory comments for complex logic. Avoid stating the obvious.

## AI Agent Instructions
- **Documentation & Standards:**
  - **Source of Truth:** [Godot 4 Documentation](https://docs.godotengine.org/en/stable/)
  - **Style Guide:** [GDScript Style Guide](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_styleguide.html)
  - **External References:** If stuck, consult [Godot Demo Projects](https://github.com/godotengine/godot-demo-projects) or [Awesome Godot](https://github.com/godotengine/awesome-godot) for implementation patterns.
  - **Instruction:** Agents should consult these resources if project conventions are ambiguous. Prefer patterns found in the codebase first, but fallback to the official style guide for new implementations.
- **Modifying Code:** Always read the file first to match existing style (tabs vs spaces, typing strictness).
- **New Scripts:** If creating a generic system, consider if it should be a `class_name`.
- **Scene Manipulation:** Prefer editing `.tscn` files through the Godot Editor if possible, or be extremely careful editing raw text format.
- **Path Handling:** Always use absolute paths (`res://...`) within Godot logic.

### Asset Sourcing (Game Jam)
- **Goal:** Prioritize finding existing high-quality free assets (CC0/Public Domain) over generation.
- **Strategy:** Use `webfetch` or `search` tools to locate assets on the following trusted sites.
- **Resources:**
  - **Textures/Materials:**
    - [Poly Haven](https://polyhaven.com/) (High quality HDRIs/Textures)
    - [AmbientCG](https://ambientcg.com/) (PBR Materials)
  - **3D Models:**
    - [Kenney Assets](https://kenney.nl/assets) (Low poly, consistent style)
    - [Quaternius](https://quaternius.com/) (Free animated 3D models)
    - [Sketchfab](https://sketchfab.com/) (Filter by 'Downloadable' & 'CC0')
  - **2D Art/Sprites:**
    - [OpenGameArt](https://opengameart.org/) (Community driven)
    - [Kenney Assets 2D](https://kenney.nl/assets/category:2d)
  - **Audio/SFX:**
    - [Freesound](https://freesound.org/) (SFX)
    - [Sonniss GDC Bundles](https://sonniss.com/gameaudiogdc) (Pro quality SFX)
    - [Incompetech](https://incompetech.com/) (Music)
  - **Animations:**
    - [Mixamo](https://www.mixamo.com/) (Character animations)

## Global Game Jam 2026

### Theme
**"Mask"**

### Game Concepts
*Currently evaluating the following concepts. Agents should be prepared to pivot or prototype features relevant to these genres.*

1.  **Impostor Syndrome / If they find out** (Horror / Social Stealth)
    *   **Genre:** 3D Social Stealth / Psychological Horror
    *   **Core Loop:** Survive in hostile environments (e.g., cultist camp) by blending in.
    *   **Mechanic:** Wear a specific "Mask" (literal or behavioral) to mimic the behaviors of the group. Failure to adapt leads to detection.
    *   **Scope:** 3D environment, NPC AI behavior matching, narrative-driven.

2.  **One more day / Still Breathing, Still Acting** (Horror / Survival / Roguelite)
    *   **Genre:** 3D Survival Horror / Roguelite
    *   **Core Loop:** The player is teleported to a new, hostile location/universe every 24 hours.
    *   **Mechanic:** Rapid adaptation to local threats using masks/disguises to survive until the next jump.
    *   **Scope:** Procedural or distinct level design, diverse enemy types, time-limit mechanics.

3.  **Mimic / Skinwalker** (Horror / Reverse Horror)
    *   **Genre:** Monster Simulator / Stealth Action (2D or 3D TBD)
    *   **Core Loop:** You are the monster. Infiltrate a group of humans to consume them one by one.
    *   **Mechanic:** Kill targets to take their appearance (Mask). Use their face to gain trust of others before striking.
    *   **Scope:** AI trust systems, stealth takedowns, shapeshifting mechanics.

4.  **Wonderer** (Atmospheric / Puzzle Platformer)
    *   **Genre:** 2D Metroidvania / Puzzle Platformer (Potential 2.5D)
    *   **Core Loop:** A faceless entity searches for its identity.
    *   **Mechanic:** Find and wear different masks/faces to gain specific abilities (e.g., a bird mask to glide, a rock mask to break walls).
    *   **Goal:** Collect fragments of your "True Face".
    *   **Scope:** Ability-gating, exploration, atmospheric visual storytelling (Slenderman-esque neutral protagonist).
