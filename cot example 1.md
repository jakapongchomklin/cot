# cot example 1

## 1. Prepare

- Generate user stories if need. (from a source requirements)
- Use them in step 2.

## 2. Template

```
You are an analyst who derives UML class diagrams from user stories.
Think step-by-step using the Chain-of-Thought pattern shown in the example.

[Example of Chain-of-Thought Prompting]

User Story:
As an archivist, I want to link electronic versions of researchers' publications to citations, so that I can share them with other researchers.

Reasoning:
[Class Identification]
- The actor "archivist" does not perform system operations → not a class.
- Primary domain entities are "Publication" and "Citation".
→ Classes = Publication, Citation.

[Attribute Identification]
- The story mentions electronic versions of publications.
→ Attribute "isElectronic" belongs to Publication.

[Relationship Identification]
- The story mentions linking publication to citation.
→ Relationship = Publication —(association)— Citation.

Output:
Classes:
- Publication
- Citation

Attributes:
- Publication(isElectronic)
- Citation(none)

Relationships:
- Publication —(association)— Citation


[Now analyze the following user story using the SAME reasoning steps]

User Story:
As a moderator, I want to select whether to have the estimators estimate with {0, 1/2, 1, 2, 3, 5, 8, etc.} or {0, 1, 2, 4, 8, 16, 32, etc.} policies.

Reasoning:
(Write Class Identification → Attribute Identification → Relationship Identification)

Output Format:
Classes:
- ...
- ...
Attributes:
- ClassName(attributeName)
Relationships:
- ClassA —(relationship)— ClassB

[draw a class diagram]

Generate PUML for me
```

## 3. A sample PUML

```
@startuml
' ========================
' Classes
' ========================

class Member {
  +nationalID: String
  +name: String
  +dateOfBirth: Date
  +address: String
  +email: String
  +emergencyContact: String
}

class Membership {
  +membershipID: String
  +registrationDate: Date
  +status: String
}

class PersonalTrainer {
  +trainerID: String
  +name: String
  +IDCard: String
  +expertise: String
}

class TrainingProgram {
  +programID: String
  +sessionCount: Integer
  +exerciseType: String
  +price: Double
}

class Payment {
  +paymentID: String
  +amount: Double
  +paymentDate: Date
  +paymentStatus: String
  +paymentMethod: String
}

class Receipt {
  +receiptID: String
  +sendDate: Date
  +recipientEmail: String
}

class TrainingSession {
  +sessionID: String
  +date: Date
  +time: Time
  +sessionsUsed: Integer
  +remainingSessions: Integer
}

class Report {
  +reportID: String
  +month: String
  +totalSessionsUsed: Integer
  +totalSessionsLeft: Integer
  +totalPaymentAmount: Double
}

' ========================
' Relationships
' ========================

Member "1" -- "1" Membership : has >
Member "1" -- "0..*" TrainingProgram : purchases >
TrainingProgram "1" -- "1" PersonalTrainer : assigned to >
TrainingProgram "1" -- "1" Payment : has >
Payment "1" -- "1" Receipt : generates >
TrainingProgram "1" -- "0..*" TrainingSession : includes >
PersonalTrainer "1" -- "0..*" TrainingSession : conducts >
Report ..> Member : summarizes >
Report ..> PersonalTrainer : summarizes >
Report ..> TrainingProgram : summarizes >

@enduml
```


