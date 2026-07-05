````mermaid
flowchart LR

    User[Utilisateur]

    IAM["ComLabs IAM"]

    Platform["ComLabs Platform"]

    Mobile["ComLabs Mobile"]

    Portal["Portail Client"]

    API["API"]

    User --> IAM

    IAM --> Platform
    IAM --> Mobile
    IAM --> Portal
    IAM --> API
    ````
    