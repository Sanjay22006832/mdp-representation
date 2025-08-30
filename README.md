# MDP REPRESENTATION
### NAME : M Sanjay
### REG NO : 212222240090

## AIM:
To represent a Markov Decision Process (MDP) problem in the following ways.

Text representation

Graphical representation

Python - Dictionary representation

## PROBLEM STATEMENT:

### Problem Description
An RL agent controls a single room’s thermostat to keep the room comfortable while minimizing energy usage. At each decision step it chooses one of three actions: Heat, Cool, or Do Nothing. Ambient disturbances (outside temperature, occupancy, windows) cause stochastic changes; outcomes are probabilistic. The agent learns a policy that balances comfort (keep in desired temperature range) and energy cost.

### State Space
S = {
S0: Cold (room temperature below comfort),
S1: Comfortable (within desired temperature range),
S2: Hot (room temperature above comfort)
}

### Sample State
S1 (Comfortable) — room is within 22–25°C (no urgent action needed).

### Action Space
A = {
A0: Heat — run heater to increase temperature,
A1: Cool — run AC to decrease temperature,
A2: Do Nothing — maintain current thermostat (no active heating/cooling)
}

### Sample Action
From S0 (Cold): take Heat (A0) to try to reach Comfortable.

### Reward Function
If resulting state is Comfortable → +10.

If resulting state is Cold → −5.

If resulting state is Hot → −5.

Action energy cost: Heat or Cool = −1, Do Nothing = 0.
(Immediate reward = reward of next state + action cost.)
### Graphical Representation
<img width="2000" height="1400" alt="room_temp_control_colorful (1)" src="https://github.com/user-attachments/assets/8ce1e37c-d7bb-429e-a448-9054aac1adea" />


## PYTHON REPRESENTATION:
```
P = {
    1: {   # S0: Cold
        0: [(0.9, 2, +9, False), (0.1, 3, -6, False)],   # Heat: to Comfortable (0.9) or overshoot Hot (0.1)
        1: [(1.0, 1, -6, False)],                       # Cool: stays Cold (no benefit) but cost
        2: [(0.7, 1, -5, False), (0.3, 2, +10, False)]  # DoNothing: likely stay Cold, small chance become Comfortable
    },
    2: {   # S1: Comfortable
        0: [(0.8, 2, +9, False), (0.2, 3, -6, False)],  # Heat: usually stay Comfortable, sometimes Hot
        1: [(0.8, 2, +9, False), (0.2, 1, -6, False)],  # Cool: usually stay Comfortable, sometimes Cold
        2: [(0.8, 2, +10, False), (0.1, 1, -5, False), (0.1, 3, -5, False)]  # DoNothing: mostly stays Comfortable
    },
    3: {   # S2: Hot
        0: [(1.0, 3, -6, False)],                       # Heat: keeps Hot and wastes energy
        1: [(0.9, 2, +9, False), (0.1, 1, -6, False)],  # Cool: usually to Comfortable, rare overshoot Cold
        2: [(0.7, 3, -5, False), (0.3, 2, +10, False)]  # DoNothing: likely remain Hot, sometimes drift to Comfortable
    }
}
```


## OUTPUT:
```
{1: {0: [(0.9, 2, 9, False), (0.1, 3, -6, False)],
     1: [(1.0, 1, -6, False)],
     2: [(0.7, 1, -5, False), (0.3, 2, 10, False)]},
 2: {0: [(0.8, 2, 9, False), (0.2, 3, -6, False)],
     1: [(0.8, 2, 9, False), (0.2, 1, -6, False)],
     2: [(0.8, 2, 10, False), (0.1, 1, -5, False), (0.1, 3, -5, False)]},
 3: {0: [(1.0, 3, -6, False)],
     1: [(0.9, 2, 9, False), (0.1, 1, -6, False)],
     2: [(0.7, 3, -5, False), (0.3, 2, 10, False)]}}
```

## RESULT:

Thus the given real world problem is successfully represented in a MDP form.

