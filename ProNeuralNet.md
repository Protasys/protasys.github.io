# ProNeuralNet

ProNeuralNet is a plugin of Unreal Engine. User can use this plugin to setup a "neural network brain" for actors. The "brain" can load and query at runtime.

# libpnn

>The Protasys Neural Network Library (libpnn) is a neural network library developed by Protasys LLC <sup>[1]</sup>, providing basic functions and interfaces needed for neural network training.
>
>Users can train test data through the qpnn project.

---

## Select Manual Language

[English](./readme.md)

[Chinese](./readme_ch.md)

---
## Mission

* Core library for neural network training programs
* Provide relevant functions for game AI components or applications
* Convenient docking, as little dependency as possible or static library compilation for dependencies

---

## Concepts

### IPNNSys

IPNNSys is the interface of the neural network management system, pointing to PNNSystem
PNNSystem is responsible for organizing INN and managing INNCore

### INN
INN is the interface of the neural network object NN
NN provides users with basic training and recognition interfaces of neural networks, INN is not thread-safe by default during development

### INNCore
INNCore is the pointer to the neural network core interface, pointing to a neural network core (NNCore)
NNCore wraps a neural network object (NN object), and has some properties, including the unique identifier uuid (a type of hash code) of each NN in the system, uid (a name that users can identify and modify)

### INNFactory

The interface of NNFactory, responsible for creating various objects in libpnn in factory mode

---

## Interfaces

| Interface Name | Detailed Information | Thread Safety | Return Value |
| -- |--| --|--|
| PNNSystem() | Get the singleton pointer of nn system | yes | IPNNCore* |
| CreateNN | Create a new neural network | yes | INN* |
| LoadNN | Load a neural network from a file | yes | bool |
| SaveNN | Save the neural network to a file | yes | bool |

---
## Sample Code

```
PNNSystem()
```




# References

[1] [Home Page of Protasys LLC ](https://protasys.github.io/)


