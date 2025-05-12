
# Overview

## Project Core

### The Problem

- Current solutions are expensive at $5,000+
- Many individual parts
- Complex interfaces
- Steep learning curve

### Target Users

- OSU Global Formula Racing Team
- Small labs, startups, educators, hobbyists
- Go-Karts, Snowmobiles, Mountain Bikes

### Our Solution

- Bridges the professional-hobbyist gap
- Cost effective, around $500
- Single Purchase Product (Pi w/ sensors)
- User friendly interface for non-experts

### Technical Highlights

- Pi receives ECE Team’s data via USB or WIFI
- Pi transmits data batches to AWS via 4G LTE
- Pi transmits low-latency data via WebSockets
- Flexible SQLite DB can allow new sensor types
- Scaliable TCP server utilizing pattern matching
- Cross-platform web-based data visualizations
- All software is written entirely in Rust

## Diagrams

### Data Acquisition System Overview

<!-- <center> -->
<!-- <p>Data Acquisition System Overview</p> -->

<!-- ![System Block Diagram](/img/blkDiag.png) -->
<img src="/img/blkDiag.png" width="75%" />
<!-- </center> -->

### Database Entity Relationship Diagram

<!-- <center> -->
<img src="/img/db-ERD.png" width="75%" />
<!-- </center> -->

### Architecture Design Diagram

<!-- <center> -->
<img src="/img/archDiagram.png" width="75%" />
<!-- </center> -->
