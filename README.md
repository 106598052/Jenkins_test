# Jenkins_test
## NTUT ISLab 2018

# Using Python on Jenkins for Continuous Integration

## Install Python

1.Install Python3.6
```shell
$ sudo add-apt-repository ppa:jonathonf/python-3.6
$ sudo apt-get update
$ sudo apt-get install python3.6
```

2.Change the verison of system default
```shell
$ python --version
$ sudo rm /usr/bin/python
$ sudo ln -s /usr/bin/python3.6 /usr/bin/python
$ python --version
```

3.Execute python
```shell
$ mkdir test
$ cd test
$ sudo nano calculator.py

def plus(a, b):
    return a + b

def minus(a, b):
    return a - b
$ sudo nano calculator_test.py

import unittest
import calculator
class CalculatorTestCase(unittest.TestCase):
    def setUp(self):
        self.args = (3, 2)
        
    def tearDown(self):
        self.args = None

    def test_plus(self):
        expected = 5;
        result = calculator.plus(*self.args);
        self.assertEqual(expected, result);

    def test_minus(self):
        expected = 1;
        result = calculator.minus(*self.args);
        self.assertEqual(expected, result);

unittest.main(verbosity=2)

$ sudo python calculator_test.py
```

4.Install coverage
```shell
$ sudo apt install python3-pip
$ sudo pip3 install coverage
$ coverage --version
```


*Install nose
```shell
$ sudo apt install python3-pip
$ pip install nose
$ pip install --upgrade pip
```
