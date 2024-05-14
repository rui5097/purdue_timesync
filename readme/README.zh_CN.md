# Purdue Northwest时钟同步模拟器

## 视频指导

- [Guide for how to use P-TimeSync - YouTube](https://www.youtube.com/watch?v=hPGJymCEeGw)

## 模拟器概述

该模拟器包括以下功能：

1. **网络可视化**
   - 根据用户输入生成网络可视化。
2. **时钟同步模拟**
   - 模拟网络内的时钟同步。
   - 输出代表每个时间点的网络状态的数据。
   - 为后续机器学习应用提供数据。

## 安装说明

1. 按照https://git.skewed.de/count0/graph-tool/-/wikis/installation-instructions上的说明安装`graph-tool`并在本地Linux环境中运行show.ipynb。

2. 对于Google Colab：

   ```pythonCopy code
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

完成上述步骤后，执行以下命令：

```python
%run show.ipynb
```

## 配置

### 模式

- **mode**：选择操作模式。
- 选项：
    - `manual`：手动配置路由器。
  - `auto`：自动生成路由器。

### 资源路径

- **resource_path**：存储照片的路径。

### 包大小

- **package_size**：包的大小，以兆字节（MB）为单位。

### 输出路径

- **output_clocks_delay**：存储时钟延迟输出的路径。
- **output_link_info**：存储链接信息输出的路径。
- **output_visualization**：存储可视化输出的路径。

### 模拟设置

- **simulate_stride**：模拟的时间间隔，以秒为单位。
- **simulate_max_steps**：最大模拟步数。
- **simulate_normal_wait_time**：模拟期间的正常等待时间，以秒为单位。
- **simulate_berkeley_wait_time**：模拟期间的伯克利等待时间，以秒为单位。

### 时钟设置

- **clock_delay_function**：时钟延迟函数定义。用于模拟真实的时钟延迟数据。
- 示例：`delta = t*1.e-6 + (t**2)*1.e-12 + jitter(1.e-10)`

### 自动模式

- **scene_path**：存储自动模式场景的CSV文件的路径。

### 手动模式

- **scene_path**：存储手动模式场景的CSV文件的路径。

## 手动模式配置

- 在手动模式下，网络完全根据用户输入生成。用户需要在指定的CSV文件中提供节点和边的信息。修改`/scenes/sim_manual/`（或者由`config/Manual Mode/scene_path`确定的自定义配置路径）中的文件。

#### node.csv

- 第一行应包含以下标题："id, name, show_name, type, surface, x, y"
  - 列代表：索引，名称，显示名称，节点类型，节点表面图像地址，坐标
  - 从第二行开始，每行表示一组节点数据。

#### edge.csv

- 标题："start_node_name, end_node_name, trans_bandwidth, prop_distance, propagation_speed, loss_up, loss_down"
  - 列代表：起始节点名称，结束节点名称，链接带宽，链接距离，数据传播速度，上行数据包丢失，下行数据包丢失
  - 从第二行开始，每行表示一组链接数据。

#### route.csv

- 标题："start_node_name, end_node_name"
  - 列代表：起始节点名称，结束节点名称
  - 从第二行开始，每行表示一组数据，表示传输的起始和结束节点。

## 自动模式配置

- 在自动模式下，网络根据用户输入的节点自动生成。用户需要在指定的CSV文件中提供节点的信息。修改`/scenes/sim_auto`（或由`config/Auto/scene_path`确定的自定义配置路径）中的文件。

#### node.csv

- 第一行应包含以下标题："id, name, show_name, type, surface"
  - 列代表：索引，名称，显示名称，节点类型，节点表面图像地址
  - 从第二行开始，每行表示一组节点数据。

## 输出结果

1. **clocks_delay**：显示每两个节点之间的延迟在每个模拟步骤之后。
   - 结果位于指定路径：`output_clocks_delay = output/clocks_delay/`。
2. **link_info**：生成每个链接的详细信息，包括起始节点、结束节点、传输带宽、传播距离、传播速度、上行数据包丢失和下行数据包丢失等属性。
   - 结果位于指定路径：`output_link_info = output/link_info/`。
3. **visualization**：生成每个模拟步骤后图形内节点之间的最佳路径的可视化结果。
   - 结果位于指定路径：`output_visualization = output/visualization/`。

## 如何引用

BibTeX条目：

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