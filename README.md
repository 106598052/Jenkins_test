# Jenkins_test 
present by NTUT ISLab 2018

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
$ sudo apt install python-pip
$ coverage --version
```

5.Run python with coverage
```shell
$ coverage run calculator_test.py
$ coverage report -m
```

6.Install nose
```shell
$ sudo apt install python3-pip
$ pip install --upgrade pip
$ pip3 install nose
```

7.Install java 8
```shell
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
$ java -version
```

8.Install Jenkins
```shell
$ wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
**remember the key might be change
$ sudo sh -c 'echo deb http://pkg.jenkins.io/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
$ sudo apt-get update
$ sudo apt-get install jenkins
$ sudo service jenkins start
$ sudo add-apt-repository ppa:cwchien/gradle
$ sudo apt-get update
$ sudo apt-get install gradle
$ ifconfig
$ sudo more /var/lib/jenkins/secrets/initialAdminPassword
$ firefox localhost:8080/
```
copy the password and paste on the jenkins
setup the admin user data
setup the url for jenkins

9.Install Jenkins plugin

Cobertura
Violations

10.Add new item

Select FreeStyle project
Choose Source Code Management and select git
Fill your github url 
Choose Build Environment and select Delete workspace before build starts
Choose Build and select Execute shell
write
```
nosetests --with-xunit --all-modules --traverse-namespace --with-coverage --cover-package=project1 --cover-inclusive
python -m coverage xml --include=project1*
pylint -f parseable -d I0011,R0801 project1 | tee pylint.out
```
Choose Add post-build action
Publish Cobertura Coverage Report fill in coverage.xml
Publish JUnit test result report fill in nosetests.xml
Report Violations fill pylint.out in pylint
save

11.Build Jenkins

Build now and see the report

**Change Jenkins language
install plugin Locale
fill zh_tw in Default Language
