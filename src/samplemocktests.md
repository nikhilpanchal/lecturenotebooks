```python
from unittest import TestCase
from unittest.mock import Mock, MagicMock, patch


class Calculation:
    def run(self):
        return 10 * 10

    def debug_run(self):
        pass


class Calculator:
    def multiply(self, val, exponent):
        result = val

        for i in range(1, exponent):
            result *= val

        return result

    def square_and_increment(self, val):
        return self.multiply(val, 2) + 1

    def invoke(self, calculation):
        return calculation.run()

    def debug_invoke(self, calculation):
        return calculation.debug_run()


if False:
    calculator = Calculator()

    # Stub out a dependent method since the focus of this test is not multiply.
    calculator.multiply = Mock()
    calculator.multiply.return_value = 100

    result = calculator.square_and_increment(10)
    calculator.multiply.assert_called_once_with(10, 2)
    assert result == 101, "Square and increment of 10 should be 101"

if False:
    # Mocking out an object to ensure its member methods are called as expected
    calculation = MagicMock()
    calculator = Calculator()
    calculator.invoke(calculation)

    calculation.run.assert_called_with()

if False:
    # test_
    pass

if False:
    mock = Mock()
    mock.sample_field = 30
    mock.return_value = 10

    mock.sample_method.return_value = 20

    assert mock() == 10
    assert mock.sample_field == 30
    assert mock.sample_method() == 20

# Side effects.
if False:
    # Setup a stub to throw an exection
    mock = Mock()
    mock.debug_run.side_effect = Exception("Erroneous call")

    calculator = Calculator()
    calculator.debug_invoke(mock)

if False:
    # Or have the mock call another dummy function
    def dummy():
        print("Call to the dummy stub function, do stub stuff here")
        return 500


    mock = Mock()
    mock.debug_run.side_effect = dummy
    mock.crap.return_value = 100

    calculator = Calculator()
    assert calculator.debug_invoke(mock) == 500, "FAiled"

# Creating a mock based on a class definition
if False:
    mock = MagicMock(spec=Calculation)
    mock.debug_run.return_value = 10
    mock.crap.return_value = 100

    calculator = Calculator()
    calculator.debug_invoke(mock)


if True:
    class MyTestCase(TestCase):
        def test_something(self):
            pass

    MyTestCase().test_something()
```
