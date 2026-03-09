graph TD
    %% 1. Environment Section
    subgraph Environment [CARLA Simulator Server]
        A[World Simulation] -->|Raw Data| B[Sensors Data]
    end

    %% 2. Processing Section
    subgraph Perception_Planning [E2E Autonomous System]
        B -->|RGB Image| C1[Camera-based Feature Extractor]
        B -->|Point Cloud| C2[LiDAR-based Feature Extractor]
        
        C1 --> D{End-to-End Planner}
        C2 --> D
        
        D -->|Trajectory| E[Waypoints Prediction]
        D -->|Action| F[Direct Control Value]
    end

    %% 3. Control Section
    subgraph Control_Actuation [Control & Feedback]
        E --> G[PID / MPC Controller]
        F --> G
        G -->|Steer, Throttle, Brake| H[Ego Vehicle Actuation]
    end

    %% 4. Closed-loop Feedback
    H -->|State Update| A

    %% Styling
    style Environment fill:#f9f,stroke:#333,stroke-width:2px
    style Perception_Planning fill:#bbf,stroke:#333,stroke-width:2px
    style Control_Actuation fill:#dfd,stroke:#333,stroke-width:2px
