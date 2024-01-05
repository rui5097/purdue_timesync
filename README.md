# Purdue Northwest Time Clock Sync Simulator


## Simulator Overview

This simulator encompasses the following functionalities:

1. **Network Visualization**
   - Generates visualizations of networks based on user input.

2. **Clock Synchronization Simulation**
   - Simulates clock synchronization within the network.
   - Outputs data representing the network state at each time point.
   - Provides data for subsequent machine learning applications.


## Installation Instructions

1. Follow the instructions at [https://git.skewed.de/count0/graph-tool/-/wikis/installation-instructions](https://git.skewed.de/count0/graph-tool/-/wikis/installation-instructions) to install `graph-tool` and run it in your local Linux environment.

2. For Google Colab:

    ```python
    from google.colab import drive
    import os
    
    # Mount Google Drive
    drive.mount('/content/drive')
    os.chdir('/content/drive/MyDrive/')
    
    # Clone the repository
    !git clone https://github.com/rui5097/purdue_clock_sync.git
    
    
    # Add graph-tool repository to apt sources
    !sudo echo "deb http://downloads.skewed.de/apt jammy main" >> /etc/apt/sources.list
    !sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key 612DEFB798507F25
    !sudo apt-get update
    
    # Install required packages
    !sudo apt-get install python3-graph-tool python3-matplotlib python3-cairo
    
    # Purge existing python3-cairo installation
    !sudo apt purge python3-cairo
    
    # Install dependencies
    !sudo apt install libcairo2-dev pkg-config python3-dev
    
    # Force-reinstall pycairo
    !sudo pip install --force-reinstall pycairo
    
    # Install zstandard
    !sudo pip install zstandard
    
    # Change directory to the cloned repository
    os.chdir('/content/drive/MyDrive/purdue_clock_sync')
    
    ```

After completing the above steps, execute the following command:

```python
%run show.ipynb
```

## config

### Mode
- **mode**: Choose the operation mode.
  - Options:
    - `manual`: Configure the routers manually.
    - `auto`: Generate the routers automatically.

### Resource Paths
- **resource_path**: The path where photos are stored.

### Package Size
- **package_size**: The size of the package in megabytes (MB).

### Output Paths
- **output_clocks_delay**: Path for storing clocks delay output.
- **output_link_info**: Path for storing link information output.
- **output_visualization**: Path for storing visualization output.

### Simulation Settings
- **simulate_stride**: Time interval for simulation in seconds.
- **simulate_max_steps**: Maximum simulation steps.
- **simulate_normal_wait_time**: Normal wait time in seconds during simulation.
- **simulate_berkeley_wait_time**: Berkeley wait time in seconds during simulation.

### Clock Settings
- **clock_delay_function**: Clock delay function definition.
  - Example: `delta = t*1.e-6 + (t**2)*1.e-12 + jitter(1.e-10)`

### Auto Mode
- **scene_path**: Path storing the CSV of scenes for auto mode.

### Manual Mode
- **scene_path**: Path storing the CSV of scenes for manual mode.



## Manual Mode Configuration

- In manual mode, the network is completely generated based on user input. Users need to provide information for nodes and edges in the specified CSV files. Modify Files in `/scenes/sim_manual` (or custom path determined by `config/Manual Mode/scene_path`)

#### node.csv
- The first line should have the following headers: "id, name, show_name, type, surface, x, y"
  - Columns represent: Index, Name, Display Name, Node Type, Node Surface Image Address, Coordinates
  - Starting from the second line, each row represents a set of node data.

#### edge.csv
- Headers: "start_node_name, end_node_name, trans_bandwidth, prop_distance, propagation_speed, loss_up, loss_down"
  - Columns represent: Start Node Name, End Node Name, Link Bandwidth, Link Distance, Data Propagation Speed, Upstream Packet Loss, Downstream Packet Loss
  - Starting from the second line, each row represents a set of link data.

#### route.csv
- Headers: "start_node_name, end_node_name"
  - Columns represent: Start Node Name, End Node Name
  - Starting from the second line, each row represents a set of data indicating the start and end nodes for a transmission.

## Auto Mode Configuration

- In auto mode, the network is automatically generated based on user-inputted nodes. Users need to provide information for nodes in the specified CSV file. Modify Files in `/scenes/sim_auto` (or custom path determined by `config/Auto/scene_path`)

#### node.csv
- The first line should have the following headers: "id, name, show_name, type, surface"
  - Columns represent: Index, Name, Display Name, Node Type, Node Surface Image Address
  - Starting from the second line, each row represents a set of node data.

## Output Results

1. **clocks_delay**: Displays the delay between every two nodes after each simulation step.
   - Results are located at the path specified by: `output_clocks_delay = output/clocks_delay/`.

2. **link_info**: Generates detailed information for each link, including attributes such as start node, end node, transmission bandwidth, propagation distance, propagation speed, upstream packet loss, and downstream packet loss.
   - Results are located at the path specified by: `output_link_info = output/link_info/`.

3. **visualization**: Generates the optimal path between nodes within the graph after each simulation step.
   - Results are located at the path specified by: `output_visualization = output/visualization/`.

## How to Cite 
BibTeX entry:
```
@misc{dai2024ptimesync,
    title={P-TimeSync: A Precise Time Synchronization Simulation with Network Propagation Delays},
    author={Wei Dai and Rui Zhang and Jinwei Liu},
    year={2024},
    eprint={2401.01412},
    archivePrefix={arXiv},
    primaryClass={cs.DC}
}
```