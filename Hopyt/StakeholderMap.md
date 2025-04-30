# Hopyt - Entity Level Diagram / Stakeholder Map

This diagram shows the main stakeholders, user roles, system entities, and external dependencies interacting with or supporting the Hopyt ride-hailing application, using a Left-to-Right layout and a dark theme.

```mermaid
%%{init: {'theme': 'dark'}}%%
%% Graph direction LR (Left to Right) for horizontal flow
graph LR
    %% Define groups (subgraphs) for clarity.
    subgraph "Users & Roles"
        direction TB
        R["Rider"]
        D["Driver"]
        A["Admin / Operator"]
        O["Hopyt Platform Owner/Business"]
        S["Support Staff"]
    end

    subgraph "Core System"
        H(("Hopyt Application\n(Flutter Apps + Cloud Functions)"))
    end

    subgraph "Key Dependencies & Services"
        direction TB
        FB["Firebase Platform\n(Auth, Firestore, RTDB, Functions, Hosting, etc.)"]
        GM["Google Maps Platform\n(Maps, Directions, Places, etc.)"]
        TG["TollGuru\n(Toll API)"]
        ST["Stripe\n(Payments)"]
        CF["Cloudflare\n(DNS/CDN)"]
    end

    %% Define Interactions and Relationships (User's Flow - Cleaned)

    %% User -> System Interactions
    R -- Requests/Manages Rides --> H
    D -- Accepts Rides/Navigates --> H
    O -- Defines Business Rules/Monitors --> H
    A -- Manages System/Users --> H
    S -- Uses Admin Interface for Support --> H

    %% System -> User Interactions
    H -- Ride Status/Invoice --> R
    H -- Ride Details/Earnings --> D
    H -- Business Reports/Alerts --> O
    H -- System/User Info --> A
    H -- Support Case Updates --> S

    %% System <-> Dependency Interactions
    H -- Request Backend Services --> FB
    FB -- Provide Backend Services --> H
    H -- Get Geo/Navigation Services --> GM
    GM -- Provide Geo/Navigation Services --> H
    H -- Request Tolls Calculation --> TG
    TG -- Provide Tolls Data --> H
    H -- Request Payments --> ST
    ST -- Provide Payment Status/Webhooks --> H
    H -- DNS/Caching Request --> CF
    CF -- Provide DNS/Caching --> H

    %% Style nodes
    style H fill:#28a745,stroke:#ccc,stroke-width:2px,color:#ffffff
    classDef user fill:#334,stroke:#aaa,stroke-width:1px,color:#eee;
    classDef service fill:#443,stroke:#aaa,stroke-width:1px,color:#eee;
    class R,D,A,O,S user;
    class FB,GM,TG,ST,CF service;
```

I have updated the interactions in the Canvas to reflect your preferred flow and removed the inline comments from that section. The direct links between Support Staff and Rider/Driver have also been removed, ensuring interactions primarily go through the Core System, except for the necessary App Store downloads. Please check the preview on GitH
