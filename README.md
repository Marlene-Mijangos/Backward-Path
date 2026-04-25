# Backward Path Studio

Web application for visually editing graphs and computing the number of independent sets using an engine inspired by the backward path approach. It includes an interactive canvas, node and edge editing, case export functionality, and a performance section with stress testing.

## Description

This project is a single-page mini application that combines a user interface, graph-processing logic, and performance visualization.
Users can paste a graph in text form, modify it visually, and obtain metrics such as i(G), estimated width, detected case type, and execution time.

The interface supports both light and dark themes through CSS variables, and the performance chart is generated using Chart.js.

## Features

- Visual graph editor with canvas
- Node movement mode
- Node creation mode
- Edge creation mode
- Node deletion mode
- Edge deletion mode
- Text input compatible with edge format U V
- Automatic result computation when editing the graph
- Stress test panel to measure runtime versus graph size
- Export of cases in TXT format
- Export of metrics in CSV format
- Cases stored in memory during the session
- Light/dark theme toggle

## Interface

The app is organized into two main sections:

- Left sidebar: data input, editing tools, stress test controls, and saved cases
- Main area: summary, graph canvas, and performance panel

## Project Structure
/project-root
│
├── index.html          # Main entry point (single-page structure)
├── /css
│   └── styles.css     # Global styles, themes (light/dark via CSS variables)
│
├── /js
│   ├── app.js         # Application initialization and global state
│   ├── ui.js          # UI interactions (panels, buttons, modes)
│   ├── graph.js       # Graph data structure and operations
│   ├── editor.js      # Canvas rendering and visual editing logic
│   ├── algorithm.js   # Independent set computation (backward path approach)
│   ├── metrics.js     # Width estimation, case detection, timing
│   ├── stress.js      # Stress testing and benchmarking logic
│   └── export.js      # TXT/CSV export utilities
│
├── /data
│   └── samples.json   # Optional predefined graph cases
│
└── /lib
    └── chart.min.js  # External library: :contentReference[oaicite:0]{index=0}

If you prefer to separate files, the recommended structure would be:

/project-root
│
├── index.html              # Main entry point (SPA layout)
│
├── /assets
│   ├── /css
│   │   └── styles.css      # Global styles and theme variables
│   └── /icons              # UI icons (optional)
│
├── /src
│   ├── /core
│   │   ├── graph.js        # Graph structure and basic operations
│   │   ├── algorithm.js    # Independent set computation (backward path)
│   │   └── metrics.js      # Width estimation, classification, timing
│   │
│   ├── /ui
│   │   ├── canvas.js       # Graph rendering and interaction
│   │   ├── controls.js     # Toolbar and editing modes
│   │   └── panels.js       # Sidebar, summary, and outputs
│   │
│   ├── /features
│   │   ├── stress.js       # Stress test and benchmarking
│   │   ├── export.js       # TXT/CSV export utilities
│   │   └── storage.js      # Session memory (saved cases)
│   │
│   └── app.js              # App bootstrap and state coordination
│
├── /data
│   └── samples.json        # Example graphs (optional)
│
└── /lib
    └── chart.min.js        # External dependency: :contentReference[oaicite:0]{index=0}

## Requirements

- Modern browser with support for Canvas, Pointer Events, and ES6+
- Internet connection to load fonts from Fontshare and Chart.js via CDN

## Usage

1. Open the application in a modern web browser.
2. Input a graph using the text panel (edge format `U V`) or build it visually on the canvas.
3. Select an editing mode (move nodes, add/remove nodes, add/remove edges) to modify the graph.
4. Observe how the system automatically updates metrics such as `i(G)`, estimated width, detected case type, and execution time.
5. Use the stress test panel to evaluate performance across different graph sizes.
6. Export graph cases (TXT) or computed metrics (CSV) for further analysis.
7. Switch between light and dark themes according to your preference.


Input Format

The input text supports an optional first line indicating the number of nodes N.
After that, edges are listed in the format U V, one per line.

Example:

8
6 3
2 1
5 7
6 7
3 5

Displayed Results

The output panel displays information in the following format:

Number of i(G): 55
Time: 0.2000 ms
Detected case: simple path
Width: 1
Components: 1

Algorithm

The GraphEngine implements several special-case optimizations before applying the general strategy:

Empty graph
Simple cycle
Simple path
Disconnected graph
General case using an approximate Hamiltonian path search and counting with a backward path window

It also includes auxiliary functions to detect connectivity, extract connected components, generate a candidate traversal, and compute the total number of independent sets according to the graph structure.

## Stress test

The performance section generates square grids of size N×N, computes the result, and plots execution time as a linear curve using Chart.js.
This makes it possible to compare the algorithm’s behavior as graph size increases.

## Export
Export CSV: saves metrics of the current graph
Download case: exports the current graph text
Stress CSV: downloads stress test results

## External Dependencies

- Chart.js para la gráfica de rendimiento.
- Fontshare Satoshi para la tipografía.

## Implementation Notes

- The visual theme is controlled via data-theme="light" or data-theme="dark"
- The canvas uses touch-action: none to improve interaction with Pointer Events
- The Chart.js instance is destroyed before being recreated to avoid conflicts between instances

## Possible Improvements

- Split JavaScript into modules
- Store cases in localStorage
- Add stricter input validation
- Display additional labels or identifiers on the canvas
- Export graph results in JSON format in addition to CSV

## Licencia

Academic and personal use. Adjust this section according to your preferred license.
