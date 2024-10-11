---
layout: post
title: "Regression Testing with Python"
categories: testing
author: Brandon Barker
---

> "That is one big pile of shit." - Ian Malcolm, Jurassic Park

* * *

Software testing: a common, and essential, practice for validation and verification
of software, and a ~~pain in the ass~~ chore to many developers.
In the hit 1997 thriller _Jurassic Park_, a lack of caution, 
a bit of arrogance, and a fast-paced, 
just-ship-it attitude led to disaster -- exactly what we, as 
responsible software developers, would like to avoid.
While proper code testing would not have saved Ian Malcolm and friends from 
this particularly bad theme park visit (only properly compensating and appreciating their 
staff could have prevented that), it could have prevented other tragedies. 

As software developers it can be easy to forget that our products can have real -- 
and fatal -- impacts. In an infamous example, the European Space Agency's rocket 
[Ariane flight V88][ariane] self-destructed on its maiden flight due to what ultimately 
amounted to 16-bit variable overflow. Another bug -- this time a race condition -- 
impacting the [Therac-25][therac] radiation therapy machine caused massive radiation over dose and the 
deaths of at least three patients. There are certainly examples of this in the sciences as well, 
where our work is often ruled by a fast-paced, result-driven philosophy (did someone say "publish or perish?").

Software rules all parts of our lives, from our phones, 
to our cars, trains, and planes, to life saving medical equipment, to weaponry.
Testing is a necessary part of our careers.
Proper testing practices will save time, money, and potentially lives.
As scientists, it is a necessary step to ensure the fidelity -- and reproducibility -- of our work.
Indeed, an automated test suite is a key review criteria for 
submissions to the [Journal of Open Source Software][joss].
This is my attempt to assemble my thoughts, and produce something of a guide, to 
one type of software testing from the lens of a computational physicist.

## Regression testing

Regression testing: a type of software testing that ensures that recent code 
changes have not broken your code. It's a type of testing designed to 
stress your *entire code*, in contrast to __unit tests__ which test indivisible units 
of your code -- a numerical quadrature, an interpolation, a serialization function, 
or a matrix factorization.
Whereas unit tests are intended to test individual functionalities, regression tests
stress the entire application to ensure that its __behavior does not change in time 
as new changes are added__. In scientific computing, this usually means running your code
(say, for example, a fluid simulation) and saving its output for later.
This output is the **gold standard** and represents the correct behavior of your code.
Then, later, after changes have been push to your code, the same simulation as before
is re-run and its output compared against the gold data. If there are differences
between the new output and the gold standard, it could be indicative of a bug.
We might test for:

* physical correctness (does the code give the expected answer on test problems?)
* numerical correctness (does the code converge at the expected order?)
* performance (did recent changes slow the code down?)
* portability (can the code compile on all supported architectures? 
    Personal example: making changes that run fine on CPU but not on GPU.)
* testing different compilers and optimization levels
* and more!

Ideally this process is automated, such that on pushes to the code, or pull requests 
to the repository, these tests are initiated automatically. With these ideas in mind:
how can we create a tool flexible enough to accomplish this?

## Python for regression testing
I've chosen Python as my language of choice for implementing regression testing.
It is a great scripting language (which is what we need) and has a mature ecosystem 
to accommodate many workflows. I am also going to assume that the code we're testing is 
_compiled code_ such as C, Fortran, or Rust. If that isn't your case, ignore those parts.

Given that we are testing compiled code, we need a tool that can:

* build the code
* run the code
* validate its output
* cleanup any temporary build and test files

A Python skeleton class might look something like:

``` python
import subprocess
import os

class RegresstionTest():
    def __init__( 
      self,
      compiler, # gcc, cargo, clang
      compiler_args, #everything after the compiler, e.g., -o main main.c
      code_args, # args passed to code
      build_dir, # where it is built
      executable,
      goldfile # path to data
    ):
      # set member variables...
      self.executable = os.path.join(build_dir, executable) # etc

    def build_code(self):
      """
        Build the code 
      """
      compile_cmd = compiler + " " + compiler_args
      subprocess.run(
        compile_cmd, 
        shell=True, 
        check=True, 
        stdout=subprocess.PIPE, 
        stderr=subprocess.PIPE
      )

    def run_code(self):
      """
        Run the code 
      """
      run_cmd = executable + " " + code_args
      subprocess.run(
        run_cmd, 
        shell=True, 
        check=True, 
        stdout=subprocess.PIPE, # maybe redirect to file
        stderr=subprocess.PIPE
      )

    def compare(self):
      """
        Compare code output to gold
      """
      # very application dependent

    def test_code(self):
      """
        run the test
      """
      self.build_code()
      self.run_code()
      self.compare()

```

This code snippet contains all of the essential pieces for running a regression test 
(warning: I did not try to run this code on anything). There is definitely room for improvements, 
like wrapping the `subprocess.run` calls in a `try: except:` pattern for error catching, 
handling of the output of the code, details of the comparison, 
and a cleanup function to remove any temporary output from the test, but the idea is there. 

Let's go one step further. I mentioned that part of my motivation for using Python 
was its mature ecosystem. Let's make use of that, turning our regression testing 
class into a child of Python's [unittest][unittest] tool. 
`unittest` provides many useful features for running tests (both regression and 
unit tests), especially for running suites of tests. For our needs, `unittest` 
provides a class `TestCase` from which we may inherit. `TestCase` provides:

* `setUp()` for providing pre-test work
* `tearDown()` for post test cleanup
* a number of assert functions (`assertEqual(a,b)`, `assertTrue(b)`) that we can use for our test

Reconfiguring our test code to use `TestCase` is straightforward. After importing `unittest`, we 
need to: 

1. inherit from the TestCase class and call its initialization
``` python
import unittest
class RegressionTest(unittest.TestCase):
  def __init__(
    self,
    ##... all the same
    testcase = "test_code" # our test function, as a string
  ):
  super().__init__(testcase)
```

2. point `setUp()` to `build_code()`
```python
def setUp(self):
  self.build_code()
```

3. point `tearDown()` to any cleanup code

4. set up a test suite:

```python
if __name__ == "__main__":
    suite = unittest.TestSuite()
  suite.addTest(
    RegressionTest(
      # RegressionTest params...
    )
  )
  
  runner = unittest.TextTestRunner()
  runner.run(suite)
```


## Automation

The last step is to automate the process. In order to catch potential bugs, 
we want these tests run frequently. All major changes to the code base should be tested 
in order to catch potential bugs early. For collaborative development with GitHub and friends, 
this might mean triggering tests on every pull request (PR) / merge request. 
This idea of continuously testing code is often called **continuous integration (CI)**.
CI systems typically consist of a suite of unit tests, regression tests, and more.
On GitHub, this is achievable with GitHub actions (other git servers have similar features).
A simple example, placed in `.github/workflows/`, might look like

``` bash
name: Regression Tests

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
    tests:
      name: Run regression tests
      runs-on: ubuntu-latest

      steps:
        - name: Checkout code
          uses: actions/checkout@v2
          with:
            submodules: recursive
        - name: Set system to non-interactive mode
          run: export DEBIAN_FRONTEND=noninteractive
        - name: Install dependencies
          run: |
            sudo apt-get update -qq
            sudo apt-get install -qq --no-install-recommends tzdata
            sudo apt-get install -qq git
            sudo apt-get install -qq make cmake g++
            sudo apt-get install -qq python3 python3-numpy
        - name: Run test scripts
          run: |
            cd tst/regression
            python3 regression_test.py
```

* * *

There are as many ways to design a regression test suite as there are people to design them, this 
is just my approach. A complete example following this outline can be found 
[here](https://github.com/AstroBarker/sitar/tree/main/tst/regression).


[ariane]: https://en.wikipedia.org/wiki/Ariane_flight_V88
[therac]: https://www.bugsnag.com/blog/bug-day-race-condition-therac-25/
[unittest]: https://realpython.com/python-unittest/#
[joss]: https://joss.readthedocs.io/en/latest/review_criteria.html]]
