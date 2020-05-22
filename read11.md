# Read 11 - Data Analysis

>Data Science is basically trying to make sense of data by identifying patterns, applying algorithms to extract information and predict future actions that are suitable for a specific situation.

**_Unstructured Data:_** 

It does not have a predefined data model. It can be available in audio, video and text format.

**_Structured Data:_** 

It is mostly available in a text format which originates from databases or specific file formats like CSV (Comma Separated Values)

**_Data Analytics:_** 

Identifying patterns of the data and understanding the data by processing it in such a way that you convert the data into information.

**_Data Visualization:_** 

Having analyzed this data, you’d want to present it visually so that decisions can be made. 

**_Machine Learning:_** You feed data into the machine, and the machine tries to identify patterns in data after rigorous training and testing and there upon gives us desired results. 
 
**_Artificial Intelligence:_**

Whenever there is situation when the machine needs to make decisions on its own where judgment is involved.

**_Natural Language Processing (NLP):_**

Machine Learning and Artificial Intelligence can take multiple forms in the field of Natural Language Processing.

**_Data Science:_**

 Machine Learning, Natural Language Processing (NLP), Artificial Intelligence as are referred inside Data Science.

 ---
 # Jupyter

 * JupyterLab enables you to work with documents and activities such as Jupyter notebooks, text editors, terminals, and custom components in a flexible, integrated, and extensible manner.
 * Code Consoles provide transient scratchpads for running code interactively, with full support for rich output. A code console can be linked to a notebook kernel as a computation log from the notebook, for example.
* Kernel-backed documents enable code in any text file (Markdown, Python, R, LaTeX, etc.) to be run interactively in any Jupyter kernel.
Notebook cell outputs can be mirrored into their own tab, side by side with the notebook, enabling simple dashboards with interactive controls backed by a kernel.
* Multiple views of documents with different editors or viewers enable live editing of documents reflected in other viewers.

---
# NumPy Tutorial

[Source](https://www.tutorialspoint.com/numpy/index.htm)

* NumPy, which stands for Numerical Python, is a library consisting of multidimensional array objects and a collection of routines for processing those arrays. 
* Using NumPy, mathematical and logical operations on arrays can be performed. 
  - Mathematical and logical operations on arrays.
  - Fourier transforms and routines for shape manipulation.
  - Operations related to linear algebra. NumPy has in-built functions for linear algebra and random number generation.
- Standard Python distribution doesn't come bundled with NumPy module. A lightweight alternative is to install NumPy using popular Python package installer, pip.

```
pip install numpy
```

**_ndarray_**
The most important object defined in NumPy is an N-dimensional array type. It describes the collection of items of the same type. Items in the collection can be accessed using a zero-based index.

- It describes the collection of items of the same type. 
- Items in the collection can be accessed using a **zero-based index**.
- Each element in ndarray is an object of data-type object (**called dtype**).
- NumPy supports a much greater variety of numerical types than Python does. 
- A 2-dimensional array is also known as a matrix.
- numpy has a variety of diffent methods to perfom over them, for exampleÑ shape, size, subsetting etc.  

The basic ndarray is created using an array function in NumPy:
```
numpy.array 
<!-- or -->
numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
```

### Data Type Objects (dtype)
A data type object describes interpretation of fixed block of memory corresponding to an array, depending on the following aspects:

- Type of data (integer, float or Python object)
- Size of data
- Byte order (little-endian or big-endian). The byte order is decided by prefixing '<' or '>'.



