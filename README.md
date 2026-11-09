# Modernize your legacy code with GitHub Copilot

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey lj3076!

Mona here. I'm done preparing your exercise. Hope you enjoy! 💚

Remember, it's self-paced so feel free to take a break! ☕️

[![](https://img.shields.io/badge/Go%20to%20Exercise-%E2%86%92-1f883d?style=for-the-badge&logo=github&labelColor=197935)](https://github.com/lj3076/skills-modernize-your-legacy-code-with-github-copilot/issues/1)

---

## Data Flow

```mermaid
sequenceDiagram
actor User
participant Main as MainProgram
participant Ops as Operations
participant Data as DataProgram

loop Until the user exits
Main->>User: Display menu
User->>Main: Select an option
alt View balance
Main->>Ops: TOTAL
Ops->>Data: READ, balance
Data-->>Ops: Current balance
Ops-->>User: Display balance
else Credit account
Main->>Ops: CREDIT
Ops->>User: Request credit amount
User-->>Ops: Amount
Ops->>Data: READ, balance
Data-->>Ops: Current balance
Ops->>Ops: Add amount to balance
Ops->>Data: WRITE, updated balance
Data-->>Ops: Balance stored
Ops-->>User: Display updated balance
else Debit account
Main->>Ops: DEBIT
Ops->>User: Request debit amount
User-->>Ops: Amount
Ops->>Data: READ, balance
Data-->>Ops: Current balance
alt Sufficient funds
Ops->>Ops: Subtract amount from balance
Ops->>Data: WRITE, updated balance
Data-->>Ops: Balance stored
Ops-->>User: Display updated balance
else Insufficient funds
Ops-->>User: Display insufficient funds
end
else Exit
Main->>Main: Stop menu loop
Main-->>User: Display goodbye message
end
end
```

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

