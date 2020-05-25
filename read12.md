[ HOME ](README.md)
# Read 12 - matplotlib  Tutorial
> Most used Python package for 2D-graphics

- It provides a very quick way to visualize data from Python.
- Publication-quality figures in many formats.
- Matplotlib comes with a set of default settings that allow customizing all kinds of properties. You can control the defaults of almost every property in matplotlib: 
  - Figure size and dpi, 
  - Line width, 
  - Color and style, 
  - Axes, axis and grid properties, 
  - Text and font properties and so on. 

- While matplotlib defaults are rather good in most cases, you may want to modify some properties for specific cases.

## Examples for usage

- [Customizing Matplotlib with style sheets and rcParams](https://matplotlib.org/tutorials/introductory/customizing.html)
- [Changing colors and line widths](https://matplotlib.org/tutorials/introductory/pyplot.html)
- [Setting limits](https://github.com/rougier/matplotlib-tutorial#setting-limits)
- [Setting ticks](https://github.com/rougier/matplotlib-tutorial#setting-ticks)
- [Setting tick labels](https://github.com/rougier/matplotlib-tutorial#setting-tick-labels)
- [Moving spines](https://github.com/rougier/matplotlib-tutorial#moving-spines)
- [Adding a legend](https://github.com/rougier/matplotlib-tutorial#adding-a-legend)

### Figures, Subplots, Axes and Ticks

- A figure in matplotlib means the whole window in the user interface.
- Within this figure there can be subplots.
  - You need to specify the number of rows and columns and the number of the plot.
- Axes are very similar to subplots but allow placement of plots at any location in the figure. So if we want to put a smaller plot inside a bigger one we do so with axes.
- There are tick locators to specify where ticks should appear and tick formatters to give ticks the appearance you want. 
  - Major and minor ticks can be located and formatted independently from each other.