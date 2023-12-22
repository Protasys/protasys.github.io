# ProNeuralNet

ProNeuralNet is a plugin of Unreal Engine. User can use this plugin to setup a "neural network brain" for actors. The "brain" can load and query at runtime.

## Enable Plugin

After copy the plugin source to the Plugins/ dir, you can enable the plugin as shown below:

![ProNeuralNet_UE5_Plugin](../images/ProNeuralNet_UE5_Plugin.JPG "Enable Plugin")

# [libpnn](./libpnn.md)

>The Protasys Neural Network Library (libpnn) <sup>[1]</sup> is a neural network library developed by Protasys LLC <sup>[2]</sup>, providing basic functions and interfaces needed for neural network training.
>
>Users can train test data through the qpnn project.

---

## Select Manual Language

[English](./readme.md)

~[Chinese](./readme_ch.md) not support now~

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

[1] [libpnn, The simple way to use NN in C/C++ with Protasys Neural Network Library](./libpnn.md)

[2] [Home Page of Protasys LLC ](https://protasys.github.io/)


