# A color-picker app
## Requirements clarifications
- Is it a **full-stack web-app** or just a service only app?
- ~~What essential features should we focus on this color-picker?~~ **DON'T ASK THIS, BE SPECIFIC**
- *Features discussion*:
    - So I am thinking to have the primary feature is **color selection**, where users can see a bunch of colors by **palletes** and get their hex values.
    - We can also let users to save their **favorite colors**.
    - Also, I think a **popular color leaderboard** can be a nice to have.
    - Also, users can **log into their account** and **track their favorite colors**.
        - I think it should be enough for now, Do you think there is any other feature that I could add?
## Back-of-the-envelope estimation
- **Daily Active Users (DAUs):** What is the estimated number of daily active users? 
- **Peak Concurrency:** How many users do we expect to be on the site simultaneously, especially during peak hours? What percentage of DAUs are typically active at the peak?
## System Architecture - High level architecture
### 1. Presentation Layer (UI Layer)
- Purpose: This is the front-facing part of the application where users interact with the color picker.
- Components:
    - HTML/CSS for layout and styling.
    - JavaScript or TypeScript to handle dynamic behaviors.
    - Frameworks like React, Angular, or Vue for state management and interactive UI components.
- Responsibilities:
    - Display the color picker tool, color palettes, and other UI elements.
    - Capture user inputs such as selecting colors or making adjustments.
    - Trigger actions to save or retrieve color data by sending requests to the backend.
### 2. Business Logic Layer (Data Validation Layer & Business Logic)
- Purpose: Central layer that handles all the business rules, validation, and processing.
- Components:
    - Core services or controllers that implement the application's logic.
    - Validation modules to check user inputs (e.g., ensuring colors are within valid ranges).
- Responsibilities:
    - Validate inputs from the Presentation Layer, such as ensuring RGB values are within 0-255.
    - Execute business logic, like color format conversion (HEX to RGB).
    - Determine which API services to call based on user actions or business rules.
    - Handle complex operations such as generating complementary color schemes.
### 3. API Service Layer (External/Internal API calls)
- Purpose: This layer abstracts the communication with external or internal APIs, providing services required by the Business Logic Layer.
- Components:
    - RESTful APIs, GraphQL endpoints, or other web service connections.
    - Services that encapsulate API communication logic.
- Responsibilities:
    - Provide a clean interface for the Business Logic Layer to call external/internal APIs without directly handling the HTTP requests.
    - Fetch data such as saved colors, user preferences, or external color palettes.
    - Perform actions like saving user-selected colors to an external service.
    - Handle response data and errors, returning structured results to the Business Logic Layer.
### 4. Data Access Layer
- Purpose: Manages data operations such as saving, retrieving, or modifying information in the database.
- Components:
    - Repositories, DAOs, or similar structures that handle direct database access.
    - Database management systems like SQL Server, MongoDB, or MySQL.
- Responsibilities:
    - Translate requests from the Business Logic Layer into database queries.
    - Perform CRUD operations on color data, user settings, and other application data.
    - Ensure data consistency and integrity, managing transactions where needed.
## High-level design
### 1. Data modeling (Database design)
- color:
    - color_id INT
    - color_name varchar(max)
    - hex_value varchar(7) UNIQUE
    - rbg_value int FOREIGN_KEY (id, rbg_table)
- rbg_table:
    - id INT
    - red INT
    - blue INT
    - green INT
- palletes:
    - pallette_id INT
    - pallette_name varchar(max)
    - description varchar(max)
    - engagment_score INT
- color_palette: join table to handle many-to-many relationship between colors and palletes
    - color_id INT FOREIGN_KEY
    - pallete_id INT FOREIGN_KEY
    - (color_id, pallete_id) PRIMARY_KEY
- users:
    - user_id INT
    - username varchar(max)
    - user_email varchar(max)
    - password_hash varchar(max)
    - created_at TIMESTAMP
### 2. APIs
- GET colors/trending: Get trending colors 
- 
