# Create Excel Workflow

```mermaid
graph TD;
    A[Start] --> B[Define Base Directory for CSV Files];
    B --> C[Initialize Excel Workbook and Data Structures];
    C --> D[Read All CSV Files in Base Directory];

    D --> E{Is Entry a Directory?};
    E -- Yes --> F[Read Subdirectory Recursively];
    F --> D;
    E -- No --> G{Is Entry a CSV File?};
    G -- No --> H[Skip File];
    G -- Yes --> I[Extract Metadata from Filename and Path];

    I --> J{Generation Worksheet Exists?};
    J -- No --> K[Create Generation Worksheet];
    J -- Yes --> L[Load Existing Worksheet];
    K --> L;

    L --> M[Initialize Counters for Correct Answers and Questions];
    M --> N[Read and Parse CSV File Rows];

    N --> O[Count Correct Answers and Total Questions];
    O --> P[Add Row to Generation Worksheet];
    P --> Q[Update Exams Summary];
    Q --> R[Update Years Summary];

    R --> S{More Files to Process?};
    S -- Yes --> D;
    S -- No --> T[Create 'Exams' Worksheet];

    T --> U[Populate 'Exams' Worksheet with Summary];
    U --> V[Create 'Years' Worksheet];
    V --> W[Populate 'Years' Worksheet with Summary];

    W --> X[Save Workbook as Excel File];
    X --> Y[Log Success Message];
    Y --> Z[End];
    H --> S;