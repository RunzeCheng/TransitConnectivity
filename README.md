# Enhanced OSM Connectivity Scenario Simulator

## Project Structure

The original monolithic `version3.py` file has been refactored into multiple modules based on functionality:

### Core Modules

#### 1. **models.py** - Data Models
- `OSMNode`: Represents geographic nodes from OSM data
- `OSMWay`: Represents roads/paths in OSM data
- `VehiclePath`: Handles vehicle movement along paths with progress tracking

**Key Functions:**
- `get_position_at_progress()`: Calculate vehicle position along path
- `get_direction_at_progress()`: Calculate vehicle heading/direction

---

#### 2. **osm_parser.py** - OSM File Parsing
- `OSMParser`: Static class for parsing OSM XML files

**Key Functions:**
- `parse_osm_file()`: Parse OSM XML and extract nodes/ways
- `get_bounds()`: Calculate geographic bounds
- `convert_coordinates_to_canvas()`: Convert lat/lon to canvas coordinates
- `create_vehicle_paths()`: Generate vehicle paths from road data
- `create_sample_data()`: Generate sample data for testing

---

#### 3. **simulation_logic.py** - Simulation Engine
- `SimulationEngine`: Core simulation logic and calculations

**Key Features:**
- Application type assignment (File Transfer, IoT Sensing, Voice Call, etc.)
- Bandwidth requirement calculations (traditional and SemCom)
- Vehicle/carriage creation with requirements
- Connection assignment algorithm (priority-based)
- System metrics calculation (throughput, goodput, success ratio)

**Key Methods:**
- `calculate_bandwidth_requirement()`: Standard BW calculation
- `calculate_bandwidth_requirement_semcom()`: SemCom-aware BW calculation
- `compute_semantic_comm_delays()`: Model compression/compute trade-offs
- `assign_connections()`: Priority-based user-to-AP assignment
- `calculate_metrics()`: Compute performance metrics

---

#### 4. **visualization.py** - Canvas Rendering
- `CanvasRenderer`: Handles all drawing operations

**Key Features:**
- OSM road network visualization with color-coded road types
- Vehicle rendering with directional arrows
- Train carriage rendering
- Base station and satellite visualization
- Connection line drawing
- Legend creation
- Utilization-based color coding

**Key Methods:**
- `draw_osm_roads()`: Render road network
- `draw_road_vehicle()`: Draw vehicle with direction
- `draw_base_station()`: Draw BS tower with utilization
- `draw_satellite()`: Draw satellite with solar panels
- `draw_legend()`: Create visualization legend

---

#### 5. **metrics_logger.py** - Metrics and CSV Logging
- `MetricsLogger`: Handles metrics tracking and CSV output

**Key Features:**
- CSV file management with configurable test numbers
- Metric formatting for display
- Structured logging with headers

**Key Methods:**
- `log_metrics()`: Append metrics to CSV file
- `clear_csv()`: Reset CSV file with header
- `format_metrics_summary()`: Format metrics for status display

---

#### 6. **ui_components.py** - UI Builder
- `UIBuilder`: Constructs all UI elements

**Key Features:**
- Tabbed control interface (OSM, Simulation, Logging, SemCom, Map)
- Slider controls for parameters
- Requirement display tables
- Canvas setup with scrollbars

**Key Methods:**
- `create_all_widgets()`: Main UI construction
- `_create_control_tabs()`: Tabbed interface
- `_create_requirements_tree()`: User requirement displays
- `_create_canvas_panel()`: Simulation visualization area

---

#### 7. **main.py** - Application Entry Point
- `EnhancedScenarioSimulator`: Main application class (extends `tk.Tk`)

**Key Responsibilities:**
- Application initialization and coordination
- State management (vehicles, base stations, satellites)
- Simulation loop control
- Integration of all modules

**Key Methods:**
- `simulate_scenario()`: Start simulation
- `update_simulation()`: Main simulation loop
- `initialize_simulation_objects()`: Create simulation entities
- `redraw_canvas()`: Update visualization
- `update_requirement_displays()`: Refresh UI tables

---

## File Dependencies

```
main.py
├── models.py
├── osm_parser.py
│   └── models.py
├── simulation_logic.py
│   └── models.py
├── visualization.py
│   └── models.py
├── metrics_logger.py
└── ui_components.py
    └── visualization.py
```

## Configuration Parameters

### Semantic Communication (SemCom)
- `bandwidth_mb_s`: max 12.5 MB/s (≈100 Mbps)
- `base_delay_s`: 0.001 s (1 ms)
- `compute_capacity_mb_s`: 62,500 MB/s
- `alpha`: 0-1.0 (compression exponent)

### Digital Twin (DT)
- Traditional DT: +(0-50ms) cloud delay
- Multilayer DT: No additional delay

### Application Types
1. **File Transfer**: 50 MB, 10s latency, Priority 1
2. **IoT Sensing**: 0.01 MB, 500ms latency, Priority 1
3. **Charging Scheduling**: 0.5 MB, 1s latency, Priority 1
4. **Voice Call**: 0.1 MB, 150ms latency, Priority 2
5. **Traffic Planning**: 0.5 MB, 150ms latency, Priority 2
6. **Autonomous Driving**: 1.0 MB, 50ms latency, Priority 3

## Running the Application

```python
python main.py
```

## Key Features

1. **OSM Integration**: Load real OpenStreetMap data or use sample data
2. **Dynamic Simulation**: Vehicles move along realistic road networks
3. **Semantic Communication**: Model compression vs. compute trade-offs
4. **Priority-Based Scheduling**: Higher priority users get preference
5. **Real-Time Metrics**: Track throughput, goodput, and success ratios
6. **CSV Logging**: Export metrics for analysis
7. **Interactive Visualization**: Pan, zoom, and observe simulation in real-time

## Benefits of Modular Structure

1. **Maintainability**: Each module has a clear, focused purpose
2. **Testability**: Individual components can be tested in isolation
3. **Reusability**: Modules can be reused in other projects
4. **Scalability**: Easy to add new features without affecting existing code
5. **Readability**: Smaller files are easier to understand and navigate
6. **Collaboration**: Multiple developers can work on different modules simultaneously
