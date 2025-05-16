# Codebase

## Github Organization

Our team's codebase is held by a GitHub organization: **CS Personal Data Acquisition Prototype**.

The organization can be found <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype" target="_blank">here</a>.


## Repositories

The following are our most important repositories:

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Rust-Tcp" target="_blank">Rust-TCP</a>

- Remote TCP server facilitating inter-project communication between repositories.
- Holds historical data in an integrated SQLite3 database.
- Serves egui web client to user devices.
- Hosted on AWS for the project.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Mock-Data" target="_blank">Mock_Data</a>

- Generates mock ECE data at 100Hz.
- Transmits the generated data through websockets.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Pi_Transmit" target="_blank">Pi_Transmit</a>

- Connects to a local SQLite3 database to transmit batches of stored data to Rust-TCP.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Pi_Forwarder" target="_blank">Pi_Forwarder</a>

- Reads ECE sensor data through serial ports or network websockets.
- Immediately zero-copy forwards that data to any connected clients in parallel utilizing websockets.
- Immediately stores recieved data in a local SQLite database.
- Batch transmits local SQLite3 database to Rust-TCP.
- Efficiently deletes transmitted data by utilizing database transactions.

---

### <a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/UI-Layer" target="_blank">UI-Layer</a>

- Cross-platform web client frontend.
- Immediate mode rendering utilizing egui.

<!-- These descriptions need expanded -->

