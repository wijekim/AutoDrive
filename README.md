sequenceDiagram
    participant CALRAServer as CALRA Server
    participant DataReceiver as Data Receiver
    participant E2EPlannerModel as E2E Planner Model
    participant ControlOutput as Control Output
    participant EgoVehicle as Ego Vehicle

    CALRAServer->>DataReceiver: Send PointCloud + RGB-Image
    DataReceiver->>DataReceiver: Receive & Process Data
    DataReceiver->>E2EPlannerModel: Forward Processed Data
    E2EPlannerModel->>E2EPlannerModel: Inference
    E2EPlannerModel->>ControlOutput: Output Waypoints + Control Values
    ControlOutput->>CALRAServer: Send Control Commands
    CALRAServer->>EgoVehicle: Execute Vehicle Control
    EgoVehicle->>EgoVehicle: Move & Update State
