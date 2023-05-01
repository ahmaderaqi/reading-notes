# Q1-




Dunder (double underscore) methods in Python are special methods that have a specific naming convention of starting and ending with two underscores. These methods provide a way to define how objects of a class behave in various contexts, such as mathematical operations, comparisons, and string representation. 

For example, the `__init__` method is a commonly used dunder method in Python. It is called when an object is created from a class and is used to initialize the object's attributes. Here's an example:

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person1 = Person("John", 30)
print(person1.name) # Output: John
print(person1.age) # Output: 30



In this example, the `__init__` method initializes the `name` and `age` attributes of the `Person` class when a new `Person` object is created. The `self` parameter refers to the object being created, and is used to set its attributes.




 # Q3-

The Python `statistics` module provides a set of functions for statistical operations such as calculating measures of central tendency, measures of spread, and probability distributions. The `statistics` module is a part of the Python Standard Library, so it doesn't require any additional installation.

Here's an example of a function within the `statistics` module that can be used to calculate the mean:

import statistics

lists= [2, 3, 5, 7, 11, 13]

mean_value= statistics.mean(data)

print(mean_value)

# Output: 6.833333333333333



In this example, we import the `statistics` module and create a list of data. We then use the `mean()` function to calculate the mean of the data. The `mean()` function takes an iterable as an argument and returns the mean (average) of the values. In this case, the mean of the `data` list is 6.83. 

Other functions in the `statistics` module include `median()` for calculating the median value, `stdev()` for calculating the standard deviation, and `variance()` for calculating the variance. The `statistics` module provides a convenient and efficient way to perform common statistical calculations in Python.
