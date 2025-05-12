
# Overview

**An Affordable data acquisition system with cellular connectivity, providing low-latency personal performance data, in the palm of your hand.**

Our CompSci Capstone team is partnering with an ECE team to develop a complete sensor data acquisition device. With the ECE team's hardware sensors providing us data, we're sending data with an LTE-capable platform to an online backend. This is all accessible from our online, web-based client.

## Project Core

### The Problem

- Current solutions are expensive, at $5,000+.
- There are often many individual parts.
- Too the average layman, interfaces are too complex.
- A steep learning curve is often required to use current solutions effectively.

### Target Users

- OSU Global Formula Racing Team
- Small labs, startups, educators, hobbyists
- Go-Karts, Snowmobiles, Mountain Bikes

### Our Solution

- Bridges the professional-hobbyist gap
- Cost effective, around $500
- Single Purchase Product (Pi w/ sensors)
- User friendly interface for non-experts

### The Communications Module

- The Raspberry Pi 5 provides a high-performance Linux environment to run Rust programs similar to a full PC while also allowing an LTE module to be mounted via a HAT.
- A power delivery circuit allows most off-the-shelf USB-C power sources to provide enough current for the Pi.
- The data is gathered from a collection of sensors containing GPS, force, string, linear, and 9 degrees of freedom sensor.
- The sensors record and transmit at 100 hz for high precision which produces 5.8 KB/second with future compression possibilities.
- With constant 24 hour use the sensors produce about 348 KB/min, 20.9 MB/hour, 501 MB/day, 3.5 GB/week, or 15 GB/month.


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
