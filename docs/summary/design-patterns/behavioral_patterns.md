# Behavioral Patterns

## Strategy

```mermaid
flowchart LR
Context --> Strategy

subgraph Dynamic Choose
Strategy --> Strategy1 & Strategy2 & ...
end
```

### Case 1: TripMode

```mermaid
flowchart BT
ByBus & ByTrain & ByPlane --> TripMode
```

```mermaid
flowchart LR
p[enum TYPE]
ch1[BY_BUS]
ch2[BY_TRAIN]
ch3[BY_PLANE]

p --> ch1 & ch2 & ch3
```

```mermaid
classDiagram
TripMode <|-- ByBus
TripMode <|-- ByTrain
TripMode <|-- ByPlane

class TripMode {
 + virtual TYPE getType();
 + virtual void travel();
}

class ByBus {
 + virtual TYPE getType();
 + virtual void travel();
}

class ByTrain {
 + virtual TYPE getType();
 + virtual void travel();
}

class ByPlane {
 + virtual TYPE getType();
 + virtual void travel();
}
```

```mermaid
flowchart LR
p[static unordered_map s_trip_modes_]
ch1[BY_BUS, ByBus*]
ch2[BY_TRAIN, ByTrain*]
ch3[BY_PLANE, ByPlane*]

p --> ch1 & ch2 & ch3
```

### Case 2: MathOperation

```mermaid
flowchart BT
Add & Subtract & Multiply & Devide --> MathOperation
```

### Case 3: ParseFile

```mermaid
flowchart BT
ParseDxf & ParseJson & ParseStep --> ParseFile
```

## Chain of Responsibility

```mermaid
flowchart LR

Root[A Request]
h1[Handle1]
h2[Handle2]
h3[...]
h4[Handle4]

Root --> h1 --> h2 --> h3 --> h4
```

```mermaid
flowchart BT

h1[Handle1::deal]
h2[Handle2::deal]
h3[...::deal]
h4[Handle4::deal]
h[Handle::deal]

h1 & h2 & h3 & h4 --> h
```

```mermaid
classDiagram
class Handle {
 -Handle* next_handle_;

 +void filter(const Request&, Response&);
 +void setNextHandle(Handle*);
 +Handle* getNextHandle();
 +virtual deal(const Request&, Response&);
}
```

```cpp
void filter(const Request& req, Response& res) {
 deal(req, res);
#ifdef Stop passing down
    if(res == FINISHED)
        return;
#endif
 auto next_handle = getNextHandle();
    if(next_handle)
        next_handle->filter(req, res);
#endif
}
```

```mermaid
flowchart
subgraph HandleChain
Handle1 --setNextHandle--> Handle2 --setNextHandle--> ... --setNextHandle--> Handle4
end

Req[A Request] --> HandleChain
HandleChain .-> Res[Response]
```

### Case 1: Logger

```mermaid
flowchart
subgraph LoggerChain
ErrorLogger --gotoNext-->
WarnLogger --gotoNext-->
InfoLogger

ErrorLogger --Log ?--> ErrorLogger
WarnLogger --Log ?--> WarnLogger
InfoLogger --Log ?--> InfoLogger

end

Req[A Log] --> LoggerChain
LoggerChain .-> Res[Response]
```

### Case 2: PassNotes

```mermaid
flowchart
subgraph PassNotesChain
Girl1 --passToTheNext--> Girl2 --passToTheNext--> Girl3

Girl1 --Be my girlfriend ?--> Girl1
Girl2 --Be my girlfriend ?--> Girl2
Girl3 --Be my girlfriend ?--> Girl3
end

Req[A Note] --> PassingNotesChain
PassingNotesChain .-> Res[Response]
```

## Template

```mermaid
classDiagram

Template <|-- A
Template <|-- B
Template <|-- C

class Template {
 +void commonMethod();
 +virtual void uniqueMethod();
}

class A {
 +virtual void uniqueMethod();
}
class B {
 +virtual void uniqueMethod();
}
class C {
 +virtual void uniqueMethod();
}
```

### Case 1: Charge Device

```mermaid
flowchart LR

P[class ChargeDevice]
M1[-void powerOn]
M2[-void powerOff]
M3[-virtual void charge]

M4[+run]
M4_Ex(powerOn, charge, powerOff)

M1 & M2 & M3 --- P --- M4 --- M4_Ex
```

```mermaid
flowchart LR
ChargeDevice --- ChargePhone & ChargeComputer & ChargeEV --- charge
charge ---> chargePhone & chargeComputer & chargeEV
```

### Case 2: Play Game

```mermaid
classDiagram
PlayGame <|-- PlayGameA
PlayGame <|-- PlayGameB

class PlayGame {
 +void play();

 -virtual void initGame();
 -virtual void startGame();
 -virtual void endGame();
}

class PlayGameA{

 -void initGame();
 -void startGame();
 -void endGame();
}

class PlayGameB{

 -void initGame();
 -void startGame();
 -void endGame();
}
```

## State

```mermaid
flowchart BT

2[External Factors] --> Context

Context  --reply--> 1[Inner State Changed]

State1 --> 3[Inner State]
State2 --> 3[Inner State]
State3 --> 3[Inner State]
```

### LightSwitch

```mermaid
flowchart LR
Light --switch--> LightState
LightState --- LightOn & LightOff
```
