# FIFO

## Description

This repository contains a Verilog implementation of a First-In-First-Out (FIFO) queue. FIFO is a commonly used data structure in digital design, where the first data written into the queue is the first one read out. This is particularly useful in communication systems, buffers, and other applications where data order needs to be maintained.

Additionally, the repository includes a FIFO control module (`fifo_ctrl`) and a register file (`reg_file`), which further expand the functionality of the FIFO system.

## Features

- **Parameterizable depth**: The FIFO depth (number of entries) can be configured as needed.
- **Synchronous write**: write operation is synchronized to the clock.
- **ASynchronous read**: read operation is asynchronous.
- **Full and Empty flags**: Status flags are provided to indicate when the FIFO is full or empty.
- **Configurable data width**: Data width is configurable through a parameter.
- **Control logic**: FIFO control module for managing the read/write operations and handling overflow/underflow conditions.
- **Register file**: A register file module for storing and accessing data efficiently.

## Files

- `fifo.v`: Main Verilog file containing the FIFO module implementation.
- `fifo_ctrl.v`: A control module that handles the read and write operations of the FIFO.
- `reg_file.v`: A register file module for storing and retrieving data.
- `fifo_tb.v`: Testbench for the FIFO, used for simulation and verification of the FIFO's functionality.

## Usage

### FIFO Module Parameters

- `data_width`: Specifies the width of the data being stored in the FIFO (default: 8 bits).
- `addr_width`: Specifies the depth (number of entries) in the FIFO (default: 16).

### FIFO Ports

| Port         | Direction | Description                                  |
|--------------|-----------|----------------------------------------------|
| `clk`        | Input     | Clock signal (rising edge active).           |
| `reset`      | Input     | Reset signal (active high).                  |
| `wr`         | Input     | Write enable signal (1 = write data).        |
| `rd`         | Input     | Read enable signal (1 = read data).          |
| `w_data`     | Input     | Data input bus (size defined by `DATA_WIDTH`).|
| `r_data`     | Output    | Data output bus (size defined by `DATA_WIDTH`).|
| `full`       | Output    | Full flag (1 = FIFO is full).                |
| `empty`      | Output    | Empty flag (1 = FIFO is empty).              |

### FIFO Control Module (`fifo_ctrl.v`)

The `fifo_ctrl` module is responsible for controlling the read and write operations of the FIFO. It monitors the status flags (full/empty) and ensures that no overflow or underflow occurs during operation.

### FIFO Control Ports

| Port         | Direction | Description                                  |
|--------------|-----------|----------------------------------------------|
| `clk`        | Input     | Clock signal.                                |
| `reset`      | Input     | Reset signal.                                |
| `wr_en`      | Input     | Write enable signal.                         |
| `rd_en`      | Input     | Read enable signal.                          |
| `full`       | Output    | Full flag.                                   |
| `empty`      | Output    | Empty flag.                                  |

### Register File Module (`reg_file.v`)

The `reg_file` module is a simple register file for storing and retrieving data. It acts as the memory backend for the FIFO, providing the storage for the FIFO's data entries.

### Register File Ports

| Port         | Direction | Description                                  |
|--------------|-----------|----------------------------------------------|
| `clk`        | Input     | Clock signal.                                |
| `reset`      | Input     | Reset signal.                                |
| `wr_addr`    | Input     | Write address.                               |
| `rd_addr`    | Input     | Read address.                                |
| `wr_data`    | Input     | Data input for writing.                      |
| `rd_data`    | Output    | Data output after reading.                   |

## Simulation

To run the testbench for the FIFO:

```bash
# Using a Verilog simulator like Icarus Verilog or ModelSim
iverilog -o fifo_tb fifo_tb.v fifo.v fifo_ctrl.v reg_file.v
vvp fifo_tb
