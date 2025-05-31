# Codebase

## Github Organization

Our team's codebase is held by a GitHub organization: **CS Personal Data Acquisition Prototype**.

The organization can be found <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype" target="_blank">here</a>.

Detailed descriptions, feature overviews, installation/build guides, troubleshooting steps, and issues/future work can be found on each repository README page.


## Repositories

The following repositories make up our project:

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Rust-Tcp" target="_blank">Rust-TCP</a>

- Remote TCP server facilitating inter-project communication between repositories.
- Holds historical data in an integrated SQLite3 database.
- Serves egui web client to user devices.
- Hosted on AWS for the project.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/UI-Layer" target="_blank">UI-Layer</a>

- Web client frontend.
- Immediate mode rendering utilizing egui.
- Allows for text and graphical visualization of live and historical data.
- User and session system.
- Light and dark modes.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/client-api-lib" target="_blank">client-api-lib</a>

- Rust crate to facilitate communication between UI and TCP server.
- Linked to UI layer as an external crate.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Pi_Transmit" target="_blank">Pi_Transmit</a>

- Connects to a local SQLite3 database to transmit batches of stored data to Rust-TCP.
- Options for batch size and frequency.
- Run on Raspberry Pi or locally on desktop.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Mock-Data" target="_blank">Mock_Data</a>

- Generates mock ECE data at 100Hz.
- Transmits the generated data through websockets.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Infrastructure_Setup" target="_blank">Infrastructure_Setup</a>

- AWS deployment scripts for TCP server

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/ECE_Consolidation" target="_blank">ECE_Consolidation</a>

- Script to read and store sensor data from ECE Team's sensor pack.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Sample_DB" target="_blank">Sample_DB</a>

- Sample raw data db for use with Pi_Transmit.

---

<!-- These descriptions need expanded -->

