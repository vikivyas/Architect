# Hopyt - Entity Level Diagram / Stakeholder Map

This diagram shows the main stakeholders, user roles, system entities, and external dependencies interacting with or supporting the Hopyt ride-hailing application, using a Left-to-Right layout and a dark theme.

```mermaid
%%{init: {'theme': 'dark'}}%%
%% Changed graph direction to LR (Left to Right) for better horizontal flow
graph LR
    %% Define groups (subgraphs) for clarity
    subgraph "Users & Roles"
        direction TB %% Arrange users Top-to-Bottom within their box
        R["Rider"]
        D["Driver"]
        A["Admin / Operator"]
        O["Hopyt Platform Owner/Business"]
        S["Support Staff"]
    end

    subgraph "Core System"
        %% Using quotes for multi-line text. Ensure quotes are used for \n to work.
        H(("Hopyt Application\n(Flutter Apps + Cloud Functions)"))
    end

    subgraph "Key Dependencies & Services"
        direction TB %% Arrange dependencies Top-to-Bottom within their box
        %% Using quotes for multi-line text. Ensure quotes are used for \n to work.
        FB["Firebase Platform\n(Auth, Firestore, RTDB, Functions, Hosting, etc.)"]
        GM["Google Maps Platform\n(Maps, Directions, Places, etc.)"]
        TG["TollGuru\n(Toll API)"]
        ST["Stripe\n(Payments)"]
        CF["Cloudflare\n(DNS/CDN)"]
        AS["App Stores\n(Google Play, Apple App Store)"]
    end

    %% Define Interactions and Relationships

    %% User Interactions with Hopyt Core System
    R -- Requests/Manages Rides --> H
    D -- Accepts Rides/Navigates --> H
    A -- Manages System/Users --> H
    O -- Defines Business Rules/Monitors --> H
    S -- Uses Admin Interface for Support --> H

    %% Support Staff Interactions with Users (Keep these direct links for clarity)
    S -- Provides Support --> R
    S -- Provides Support --> D

    %% Hopyt System Dependencies
    H -- Utilizes Backend Services --> FB
    H -- Uses Geo/Navigation Services --> GM
    H -- Calculates Tolls via --> TG
    H -- Processes Payments via --> ST
    %% Moved comment to its own line for compatibility
    %% Firebase Hosting is part of Firebase Platform
    H -- Hosted/Served via --> FB
    H -- DNS/Caching via --> CF
    H -- Distributed via --> AS

    %% User Interactions with Distribution/External (Directly linking users to App Stores)
    R -- Downloads/Updates App via --> AS
    D -- Downloads/Updates App via --> AS

    %% Style nodes (optional, but can enhance readability)
    %% Specific styling overrides the theme. Using green background and white text for Core System.
    style H fill:#28a745,stroke:#ccc,stroke-width:2px,color:#ffffff
    %% General styling for user and service nodes for dark theme contrast
    classDef user fill:#334,stroke:#aaa,stroke-width:1px,color:#eee;
    classDef service fill:#443,stroke:#aaa,stroke-width:1px,color:#eee;
    class R,D,A,O,S user;
    class FB,GM,TG,ST,CF,AS service;
```
