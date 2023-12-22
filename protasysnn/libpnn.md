# Protasys Neural Network (PNN) Library

## 1. Introduction

Protasys Neural Network (PNN) is a powerful library designed for advanced neural network computations. It provides a high-level interface for neural network operations, making it easy to develop machine learning applications.

## 2. Class Descriptions

### 2.1 IPNNSys

The `IPNNSys` class is an interface for the Protasys Neural Network (PNN) system. It provides methods for creating a factory, generating random numbers, and other operations.

#### Creating an IPNNSys

You can create an `IPNNSys` object using the `PNNSystem` function:

```cpp
IPNNSys* pPNNSys = pnn::PNNSystem();
```

#### Generating Random Numbers

You can use the `RandomDouble_0_1` method to generate a random number in the range [0, 1]:

```cpp
double value = pPNNSys->RandomDouble_0_1();
```

### 2.2 IPNNFactory

The `IPNNFactory` class is an interface for a factory that can create and destroy neural networks and neural network cores.

You can get factory with IPNNSys Object

```cpp
auto pFactory = pPNNSys->Factory();
```

### 2.3 INN

The `INN` class is an interface for a neural network. It provides methods for querying the network, training the network, saving and loading the network, and other operations.

#### Creating an INN

You can create an `INN` object using the `Factory` method of `IPNNSys`:

```cpp
auto pFactory = pPNNSys->Factory();
auto pNN = pFactory->CreateNN();
```


## 2.4 FPMatrixData

The `FPMatrixData` struct represents a matrix of floating-point numbers. It contains the following fields:

- `rows`: The number of rows in the matrix.
- `cols`: The number of columns in the matrix.
- `data`: A pointer to the elements of the matrix. The elements are stored in row-major order, i.e., `data[i][j] = data[i * cols + j]`.
- `isAllocated`: A boolean flag indicating whether the data for the matrix has been allocated.

## 2.5 PNNMatrix

The `PNNMatrix` class represents a matrix of floating-point numbers. It provides methods for creating and manipulating matrices. The class contains the following public methods:

- Constructors: `PNNMatrix` provides several constructors for creating a matrix. You can create a matrix with a specific number of rows and columns, copy a matrix from another matrix, or create a matrix from a `FPMatrixData` struct.
- Destructor: The `~PNNMatrix` destructor is used to free the resources used by the matrix.
- Operator overloads: `PNNMatrix` overloads several operators for performing operations on matrices. These include addition (`+`), subtraction (`-`), multiplication (`*`), and division (`/`).
- `Dot`: This method performs the dot product of two matrices.
- `RowSize` and `ColSize`: These methods return the number of rows and columns in the matrix, respectively.
- `resize`: This method changes the size of the matrix, optionally preserving the existing data.
- `T`: This method returns the transpose of the matrix.
- `MaxValueIndex`: This method returns the coordinates of the largest value in the matrix.
- `Print`: This method prints the matrix to the standard output.
- `GetMatrixData`: This method returns a `FPMatrixData` struct representing the matrix.

The `PNNMatrix` class also contains several protected fields:

- `m_rows` and `m_cols`: These fields store the number of rows and columns in the matrix, respectively.
- `m_data`: This field is a pointer to the elements of the matrix.
- `m_row_ptr`: This field is a pointer to the row indices of the matrix.


## 3. Usage

### 3.1 Initialization

Before using the PNN library, you need to initialize the PNN system. This can be done using the `PNNSystem` function:

```cpp
IPNNSys* sys = PNNSystem("config_file.ini");
```

The `PNNSystem` function takes a configuration file as an argument. This file should contain the settings for the PNN system. If no file is provided, the function will use a default configuration file named "pnn.ini".

### 3.2 Releasing the PNN System

When you are done using the PNN system, you should release it using the `PNNSystem_Free` function:

```cpp
PNNSystem_Free();
```

Please note that this function is not thread-safe. You should ensure that no other threads are using the PNN system when you call this function.

### 3.3 Creating a Matrix

You can create a matrix using the `PNNMatrix` constructor:

```cpp
PNNMatrix matrix(rows, cols);
```

This will create a matrix with the specified number of rows and columns.

### 3.4 Performing Operations on Matrices

You can perform operations on matrices using the overloaded operators. For example, you can add two matrices together like this:

```cpp
PNNMatrix matrix1(rows, cols);
PNNMatrix matrix2(rows, cols);
PNNMatrix result = matrix1 + matrix2;
```

This will add `matrix1` and `matrix2` together and store the result in `result`.

### 3.5 Getting and Setting Matrix Elements

You can get and set the elements of a matrix using the `()` operator. For example, you can set the element at row `i` and column `j` like this:

```cpp
matrix(i, j) = value;
```

And you can get the element at row `i` and column `j` like this:

```cpp
double value = matrix(i, j);
```

### 3.6 Transposing a Matrix

You can transpose a matrix using the `T` method:

```cpp
PNNMatrix transposed = matrix.T();
```

This will return a new matrix that is the transpose of `matrix`.

### 3.7 Printing a Matrix

You can print a matrix to the standard output using the `Print` method:

```cpp
matrix.Print();
```

This will print the elements of the matrix to the standard output.

### 3.8 Perceiving

You can use the `Perceive` method to perform a perception operation. This method requires an `FPMatrixData` object (C-style use `FPMatrixData` and C++ style use `PNNMatrix` )as input:

```cpp
size_t _target = pNN->Perceive(p_input);
```

Below is a sample code using `IPNNSys` and `INN` for perceiving:

```cpp
// Create IPNNSys
IPNNSys* pPNNSys = pnn::PNNSystem();

// Create INN
auto pFactory = pPNNSys->Factory();
auto pNN = pFactory->CreateNN();

// Get input size
size_t inputSize = pNN->GetInputSize();

// Create input matrix
FPMatrixData* p_input = create_protasys_matrix_data(1, inputSize);

// Fill input matrix
for(size_t x=0;x<inputSize;++x)
{
    double value = pPNNSys->RandomDouble_0_1();
    set_protasys_matrix_data(p_input, 0, x, value);
}

// Perceive
size_t _target = pNN->Perceive(p_input);

// Print perception result
std::cout<<"perception result:"<<_target<<std::endl;

// Free input matrix
pnn::free_protasys_matrix_data(p_input);
```

Or use `PNNMatrix`  instead of `FPMatrixData` 

```cpp

// Create IPNNSys
IPNNSys* pPNNSys = pnn::PNNSystem();

// Create INN
auto pFactory = pPNNSys->Factory();
auto pNN = pFactory->CreateNN();

// Get input size
size_t inputSize = pNN->GetInputSize();

// Create input matrix
PNNMatrix _senseMatrix(1, inputSize);

// Fill input matrix
for(size_t x=0;x<inputSize;++x)
{
    _senseMatrix(0,x) = pPNNSys->RandomDouble_0_1();
}

// Perceive
size_t _target = pNN->Perceive(_senseMatrix);

// Print perception result
std::cout<<"perception result:"<<_target<<std::endl;

```


## 4. Conclusion

The PNN library provides a powerful and easy-to-use interface for neural network computations. By using the PNN library, you can quickly develop machine learning applications without having to worry about the low-level details of neural network computations.

## 5. Contact Information

If you have any questions or need further assistance, please contact Protasys, LLC at protasysllc@gmail.com.
