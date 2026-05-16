# Structural Patterns

## Flyweight

```mermaid
classDiagram

class Flyweight {
 std::unordered_map(name, obj) objs_;
}
```

### IconFlyweight

```mermaid
graph BT

Icons --Contain--- IconFlyweight

SaveIcon --> Icon
OpenIcon --> Icon
```

## Composite

```mermaid
flowchart BT

h1[Composite]
h21[Leaf]
h22[Composite]
h31[Leaf]
h32[Composite]

h31 & h32 --> h22
h21 & h22 --> h1
```

### FileComponent

```mermaid
flowchart BT

h1[Directory]
h21[File]
h22[Directory]
h31[File]
h32[Directory]

h31 & h32 --> h22
h21 & h22 --> h1

f1[FileComponent]
f21[File]
f22[Directory]
f21 & f22 --> f1
```
