# 5G Network Project - Task & Status

## 1. Defined Use Cases
The project is designed to support and demonstrate the following 5G scenarios:

### Use Case A: Connected Vehicles (V2X)
*   **Goal**: Low-latency communication for moving vehicles.
*   **Requirements**: High reliability, edge computing integration.
*   **Implementation Status**: **Done** (Simulated via `apps/veh-scripts` and `apps/edge`).

### Use Case B: Industrial IoT / Smart City (mMTC)
*   **Goal**: Massive connectivity for simpler sensors (Temperature, Humidity).
*   **Requirements**: Support for many concurrent connections, network slicing for isolation.
*   **Implementation Status**: **Done** (Simulated via `apps/iot-scripts` and MQTT).

### Use Case C: Enhanced Mobile Broadband (eMBB)
*   **Goal**: Standard high-speed internet access for smartphones.
*   **Requirements**: High throughput, S-NSSAI differentiation.
*   **Implementation Status**: **Done** (Via `basic` and `network-slicing` deployments).

---

## 2. Infrastructure & Logic (Completed Tasks)
These components are fully implemented in the repository.

### 2.1 Core Network Infrastructure
- [x] **5G Core Deployment**: Containerized Open5GS (AMF, SMF, UPF, NRF) via Docker Compose.
- [x] **Subscriber Management**: MongoDB integration and `open5gs-dbctl` automation script.
- [x] **Radio Simulation**: UERANSIM and PacketRusher integration for emulating RAN and UEs.

### 2.2 Network Scenarios & configurations
- [x] **Basic Connectivity**: Simple internet access deployment (`basic/ueransim`).
- [x] **Network Slicing**: Configuration for isolating traffic (SST 1/SD 000001 vs SD 000002).
- [x] **Roaming**: LBO Roaming architecture with Home/Visited networks (`roaming`).
- [x] **Throughput Testing**: Specialized `speed-test` deployment with iPerf3.

### 2.3 Application Layer
- [x] **Edge Computing Service**: Flask application (`apps/edge`) processing vehicle telemetry.
- [x] **IoT Simulator**: Python scripts (`apps/iot-scripts`) generating sensor data to MQTT.
- [x] **Vehicle Simulator**: Python scripts (`apps/veh-scripts`) simulating GPS/Speed data.

### 2.4 Simulation Engine Strategy
- [x] **UERANSIM**: Used for **functional verification**.
    - Configuration: `configs/basic/ueransim/ue.yaml` & `gnb.yaml`.
    - Purpose: Validating correct 3GPP PDU session establishment and signaling flows.
- [x] **PacketRusher**: Used for **load and performance testing**.
    - **Multi-Container capability**: Supports running multiple PacketRusher containers to simulate distinct eNB/gNB clusters.
    - **High Throughput**: Generates massive traffic for data plane stress testing.
    - Configuration: configured in `docker-compose.yaml` (scaling services) and `configs/*/packetrusher/packetrusher.yaml`.

---

## 3. Web Framework & Automation (Pending/To-Do)
These tasks are required to build the unified "Web Framework" for orchestrating the above components.

### 3.1 Backend API (Orchestration Layer)
- [ ] Create Central API (Flask/Node) to wrap `docker compose` commands.
- [ ] Implement Endpoints:
    - [ ] `POST /start-scenario`: Trigger `docker compose up` for specific folders (e.g., slicing, roaming).
    - [ ] `GET /status`: Check container health/status.
    - [ ] `POST /provision`: Interface for `open5gs-dbctl` to add subscribers via API.

### 3.2 Frontend Dashboard (Visualization)
- [ ] Develop Web UI (React/Vue).
- [ ] Features:
    - [ ] **Scenario Selector**: Buttons to switch between "Smart City" and "Connected Car" modes.
    - [ ] **Topology View**: Visualize active Network Functions.
    - [ ] **Live Telemetry**: WebSocket connection to display data from the MQTT broker.

### 3.3 Automated Verification
- [ ] Integrate test suites (pytest) into the API.
- [ ] Automate `iperf` triggers after scenario phases start.
