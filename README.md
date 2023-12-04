# Purdue Northwest Time Clock Synchronization Simulator [![Awesome](https://cdn.jsdelivr.net/gh/sindresorhus/awesome@d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome#readme)


## Purpose

- This system is designed to simulate a network and its routes, as well as produce visualizations and data for machine learning.
- The system allows users to either manually input a custom network architecture or have the simulator randomly generate a network topology.

## Install

## Functions

### config

- mode:
  - manual: configure the routers manually
  - auto: generate the routers automatically
  - Purdue_example: show the example of the scene in Purdue
  - Starlink_example: show the example of the scene with Starlink

- resource_path: the path storage the photo

- scene_path: the path storage the csv of scene
- package_size: the size of the package(MB)

- show_best_route: Y/N, if Y ,will show the route with least delay in the map
- output: the address of output, nothing for show in the lab

### Manual

- The system takes the input network and then procedurally generates detailed nodes, links between nodes, and routing paths within the network architecture.
- The required manual inputs are:
  1. Nodes' name
  2. Nodes' 

### Auto

- Based on the quantity of nodes specified in the input, the system algorithmically generates a full routing network topology along with calculations for optimal traversal paths between nodes.