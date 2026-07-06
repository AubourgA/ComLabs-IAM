# Identity Overview

```mermaid
classDiagram

class Identity

class LoginIdentifier

class Credential

class Profile

class Session

Identity "1" --> "*" LoginIdentifier

Identity "1" --> "*" Credential

Identity "1" --> "1" Profile

Identity "1" --> "*" Session
```