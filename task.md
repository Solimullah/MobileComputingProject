# 5G Network Framework - Project Task Breakdown

## Overview
This project involves building a web-based framework for operating, configuring, and visualizing a 5G network (RAN, Core, Transport) with automatic use-case-based configuration and verification.

---

## Phase 1: Infrastructure & Foundation (Milestone 4)

### 1.1 Environment Setup & Verification
- [ ] Verify Docker and Docker Compose installation
- [ ] Configure `HOST_IP_ADDRESS` in `build-files/open5gs.env`
- [ ] Install MongoDB and mongosh
- [ ] Install gtp5g kernel module for PacketRusher
- [ ] Verify basic deployment works (`basic/ueransim`)
- [ ] Add subscriber to database and verify connectivity

### 1.2 Backend API Development
- [x] Create Flask/Node.js backend project structure
- [x] Implement REST API endpoints:
  - [x] `GET /api/network/status` - Get network component status
  - [x] `POST /api/network/start` - Start network components
  - [x] `POST /api/network/stop` - Stop network components
  - [x] `GET /api/usecases` - List available use cases
  - [x] `POST /api/usecases/activate` - Activate a use case
  - [x] `GET /api/config` - Get current configuration
  - [x] `PUT /api/config` - Update configuration
  - [x] `GET /api/topology` - Get network topology data
- [x] Implement Docker Compose orchestration service
- [x] Create configuration file handler (JSON/YAML)

### 1.3 Frontend Web UI Development
- [x] Initialize React.js project
- [x] Install Cytoscape.js for network visualization
- [x] Create main dashboard layout:
  - [x] Network topology visualization panel
  - [x] Use case selection panel
  - [x] Status monitor panel
  - [x] Configuration editor panel
- [x] Implement component start/stop controls
- [x] Create topology graph rendering with Cytoscape.js

---

## Phase 2: Use Case Framework & Configuration (Milestone 5)

### 2.1 Use Case Implementation
- [ ] Define use case data models:
  - [ ] Industrial IoT (SST: 1, low latency, moderate throughput)
  - [ ] Connected Vehicles V2X (URLLC slice priority)
  - [ ] Smart City (mixed traffic types)
- [ ] Create use case to configuration mapping logic
- [ ] Implement automatic network reconfiguration on use case selection
- [ ] Support multiple simultaneous use case activation

### 2.2 Network Slicing Integration
- [ ] Integrate with `network-slicing` deployment
- [ ] Implement slice management in UI:
  - [ ] View active slices (SST/SD visualization)
  - [ ] Configure slice parameters
  - [ ] Assign UEs to slices
- [ ] Map use cases to specific network slices:
  - [ ] Industrial IoT → SST:1, SD:000001 (SMF1/UPF1)
  - [ ] Connected Vehicles → SST:1, SD:000002 (SMF2/UPF2)

### 2.3 Configuration Management
- [ ] Implement MNC/MCC configuration
- [ ] Implement bit rate configuration
- [ ] Create configuration profile save/load functionality
- [ ] Add configuration validation logic
- [ ] Persist configurations to JSON/YAML files

---

## Phase 3: Verification & Testing (Milestone 6)

### 3.1 Automated Test Framework
- [ ] Create pytest-based test framework
- [ ] Implement verification tests:
  - [ ] Session establishment test (UE registration)
  - [ ] PDU session setup test
  - [ ] Latency test (ping via GTP tunnel)
  - [ ] Throughput test (iPerf via `speed-test` deployment)
  - [ ] Slice isolation test (verify traffic routing)
- [ ] Create test orchestrator service
- [ ] Store test results for UI display

### 3.2 Test Result Visualization
- [ ] Display test pass/fail status in UI
- [ ] Show detailed test results and logs
- [ ] Visualize latency and throughput metrics
- [ ] Add test history/comparison view

### 3.3 Roaming Scenario (Optional/Advanced)
- [ ] Debug and verify `roaming` deployment
- [ ] Fix v-AMF to h-AMF communication via SEPP
- [ ] Verify roaming UE registration
- [ ] Visualize roaming scenario in topology view

---

## Phase 4: Documentation & Demo (Milestone 6)

### 4.1 Documentation
- [ ] Complete API documentation
- [ ] Update README with framework usage
- [ ] Create user guide for the web UI
- [ ] Document use case configurations
- [ ] Create architecture diagrams

### 4.2 Demo Preparation
- [ ] Prepare demo script
- [ ] Test all scenarios end-to-end
- [ ] Create demo video/presentation
- [ ] Prepare edge case handling

---

## Existing Deployment Scenarios

| Scenario | Description | Compose File |
|----------|-------------|--------------|
| `basic/ueransim` | Basic 5G core with UERANSIM gNB/UE | `compose-files/basic/ueransim/docker-compose.yaml` |
| `basic/packetrusher` | Basic 5G core with PacketRusher | `compose-files/basic/packetrusher/docker-compose.yaml` |
| `network-slicing` | Two slices (SST:1 SD:000001/000002) with separate SMF/UPF | `compose-files/network-slicing/docker-compose.yaml` |
| `roaming` | LBO Roaming with visited/home networks (SEPP) | `compose-files/roaming/docker-compose.yaml` |
| `scp/model-c` | SCP indirect communication (direct NRF) | `compose-files/scp/model-c/docker-compose.yaml` |
| `scp/model-d` | SCP indirect with delegated discovery | `compose-files/scp/model-d/docker-compose.yaml` |
| `speed-test` | PacketRusher + iPerf server for throughput testing | `compose-files/speed-test/docker-compose.yaml` |

---

## Technology Stack

| Layer | Technology |
|-------|------------|
| Frontend | React.js + Cytoscape.js |
| Backend API | Python/Flask or Node.js/Express + Docker |
| Network Simulation | Open5GS + UERANSIM/PacketRusher (Docker containers) |
| Data Storage | JSON/YAML files + MongoDB |
| Testing | pytest (Python) |

---

## Notes
- Focus on state/config simulation rather than real network traffic
- Prioritize core features within 10-week academic timeframe
- Use existing deployments as foundation
- Refer to `docs/` for detailed documentation
