# Format Answers Workflow

```mermaid
graph TD
    A[Start] --> B[Define Base Directories]
    B --> C[Create CSV Results Directory if Missing]
    C --> D[Read Year Directories]

    D --> E{Is Year Directory Valid?}
    E -->|No| F[Skip Year Directory]
    E -->|Yes| G[Iterate Over Subdirectories ht, vt]

    G --> H{Is Subdirectory Valid?}
    H -->|No| I[Log Missing Subdirectory]
    H -->|Yes| J[Check for Facit File]

    J -->|Missing| K[Log Missing Facit File]
    J -->|Found| L[Read and Filter Facit Answers]

    L --> M[Iterate Over Models openai]
    M --> N{Is Model Directory Valid?}
    N -->|No| O[Log Missing Model Directory]
    N -->|Yes| P[Read Generation Directories]

    P --> Q{Is Generation Directory Valid?}
    Q -->|No| R[Skip Generation Directory]
    Q -->|Yes| S[Iterate Over JSON Files]

    S --> T[Read JSON File and Filter Answers]
    T --> U[Divide Facit into Chunks 40 Questions per File]
    U --> V[Compare Answers and Facit Chunk]

    V --> W[Generate CSV Rows]
    W --> X[Write CSV File]
    X --> Y{More JSON Files?}
    Y -->|Yes| S
    Y -->|No| Z{More Generations?}
    Z -->|Yes| P
    Z -->|No| AA{More Models?}
    AA -->|Yes| M
    AA -->|No| AB{More Subdirectories?}
    AB -->|Yes| G
    AB -->|No| AC{More Years?}
    AC -->|Yes| D
    AC -->|No| AD[End]
    
    F --> AC
    I --> G
    O --> M
    R --> P
    ``