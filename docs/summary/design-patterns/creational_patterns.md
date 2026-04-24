# Creational Patterns

## Singleton

```mermaid
classDiagram

class Singleton {
  +static SingletonUPtr& GetInstance();

  -Singleton(const Singleton&) = delete;
  -Singleton& operator&(const Singleton&) = delete;
}
```

## Builder

```mermaid
graph BT

h1[Product]

h21[Part1] --> h1
h22[Part2] --> h1
h23[Part3] --> h1

h1 --> h3(Builder)
```

### Case1: Meal Package

```mermaid
graph BT

Meal --> MealPackage

Item(Items) --> Meal

Hambuger --> Item
Soda --> Item
```

## Factory

```mermaid
flowchart

1[Single Product]
```

### Case1: Shape Factory

```mermaid
flowchart RL

2.1[Circle] --> 1[Shape Factory]
2.2[Square] --> 1[Shape Factory]
```

### Case2: Color Factory

```mermaid
flowchart RL

2.1[Red] --> 1[Color Factory]
2.2[Green] --> 1[Color Factory]
```

## Abstract Factory

```mermaid
graph LR

1[Multiple Product Families]
```

### Case1: Color Shape Factory

```mermaid
flowchart BT

ColorShape2DFactory --> IColorShapeFactory
ColorShape3DFactory --> IColorShapeFactory

ColorFactory --> ColorShapeFactory
ShapeFactory --> ColorShapeFactory
```

## Prototype
