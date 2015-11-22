# Mopidy Software Verification and Validation

## Table of contents
@@TOC@@


## Introduction
Verifying a piece of software is to ensure that both the intermediate as well as the final product conform to their specification and requirements.
On the other hand, to validate software is to make sure that the final product will fulfull its intended environment, mainly through the use of tests.

The main techniques used for verifying and validating (V&V) are **static techniques** and **dynamic techniques**:

- **Static techniques**: analyze the static system representations to both find problems/bugs and evaluate quality. This includes reviews, inspections, formal verification, etc.
- **Dynamic techniques**: execute the system and observe its behavior (software testing and simulation).


In Mopidy the software is constantly and consistently validated through the use of tools such as [Travis CI](https://travis-ci.org/mopidy/mopidy) which runs the test suite automatically when code is pushed to the repository as well as [coveralls.io](https://coveralls.io/github/mopidy/mopidy) which checks code coverage for every successful build.

The test suit uses [Tox](https://tox.readthedocs.org/en/latest/) with [pytest](http://pytest.org/latest/) as a backend for testing the python code, [Sphinx](http://sphinx-doc.org/) for documentation and finally [flake8](https://pypi.python.org/pypi/flake8) for code style.

Contributions to the project are also very strict as it is required to include tests for said code/features in order to be accepted upstream.

On the other hand verification is not as important, seeing as there isn't really a formal specification or requirements document.
Most of the functionality available came from user or developer requests.

## Degree of Testability

### Controllability
(The degree to which it is possible to control the state of the component under test (CUT) as required for testing.)

### Observability
(The degree to which it is possible to observe (intermediate and final) test results.)

### Isolateability
Mopidy has unit tests for most modules, mostly because each contribution must include tests in order to be accepted, which means that the isolateability is achieved because everything is confined in its module.
Also, since the project is based in Python, developers can make use of the Python package [mock](https://pypi.python.org/pypi/mock) to reduce or eliminate the dependency on other objects by using Mock objects instead, keeping each test considerably isolated.

Pytest also makes it possible to do single unit tests. For example, testing a single directory:
`py.test tests/http/`

### Separation of concerns
(The degree to which the component under test has a single, well defined responsibility.)

### Understandability
(The degree to which the component under test is documented or self-explaining.)

### Heterogeneity
(The degree to which the use of diverse technologies requires to use diverse test methods and tools in parallel.)


## Test Statistics
Running `tox -e py27` we get the results:

![](./images/v&v/pytest_results.png "pytest results")

A total of **2065** tests passed with a code coverage of **78%**.

After analyzing the source code we concluded that most, if not all of the tests in the project are unit tests.
Also, some of the packages still have no tests associated with them (like the "file" package).

Regarding code coverage, besides being a pretty high percentage, we also think the tests themselves are valid and provide good insight on whether the software is working as intended or not.
