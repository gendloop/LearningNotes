# Behavioral Patterns

## Strategy

![](res/b587a26ab4064938934f8144060268c1.svg)

### Case 1: TripMode

![](res/62f58113c6abf756fcf4b8813c125e83.svg)

```mermaid
graph LR
p[enum TYPE]
ch1[BY_BUS]
ch2[BY_TRAIN]
ch3[BY_PLANE]

p --> ch1
p --> ch2
p --> ch3
```

![](res/4c751f61496388bdfd7349dff706fdd8.svg)

```mermaid
graph LR
p[static unordered_map s_trip_modes_]
ch1[BY_BUS, ByBus*]
ch2[BY_TRAIN, ByTrain*]
ch3[BY_PLANE, ByPlane*]

p --> ch1
p --> ch2
p --> ch3
```

### Case 2: MathOperation

![](res/2afb8463f2f1e4bedaab5dd72599fedd.svg)

### Case 3: ParseFile

![](res/f65fbc15813abddbebbe5da69abdc0d9.svg)

## Chain of Responsibility

![](res/cebbde950af9894936110affc66ca9a5.svg)

![](res/ea6c90febc97e649ed41136a4eff0fc9.svg)

![](res/5934c74bfc38658378cb523f2616bd18.svg)

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

![](res/3b0869ee3bc3119060b948d2ac5adaa6.svg)

### Case 1: Logger

![](res/b8a578b159c7f71be2376d153653b4d9.svg)

### Case 2: PassNotes

```mermaid
flowchart
subgraph PassNotesChain
Girl1 --passToTheNext-->
Girl2 --passToTheNext-->
Girl3

Girl1 --Be my girlfriend ?--> Girl1
Girl2 --Be my girlfriend ?--> Girl2
Girl3 --Be my girlfriend ?--> Girl3

end

Req[A Note] --> PassingNotesChain
PassingNotesChain .-> Res[Response]
```

## Template

![](res/2e880734dd078471c4331352fb53b1cb.svg)

### Case 1: Charge Device

![](res/e08b375be6ca7c249e5d9160314b5f87.svg)

```mermaid
flowchart LR

ChargeDevice --- ChargePhone & ChargeComputer & ChargeEV --- charge

charge ---> chargePhone & chargeComputer & chargeEV
```

### Case 2: Play Game

![](res/e18e1add33e827df2e74b75f3903bb96.svg)

## State

![](res/a4f2df43a9dd16ed0b9b06544db3474d.svg)

### LightSwitch

![](res/fba62554416bf816512b20ba5911cc33.svg)
