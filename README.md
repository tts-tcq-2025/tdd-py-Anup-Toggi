# TDD Driven StringCalculator

Build a StringCalculator functionality that can take up to two numbers, separated by commas, and will return their sum. 
for example “” or “1” or “1,2” as inputs.

> DO NOT jump into implementation! Read the example and the starting task below.

- For an empty string it will return 0
- Allow the Add method to handle an unknown amount of numbers
- Allow the Add method to handle new lines between numbers (instead of commas).
  - the following input is ok: “1\n2,3” (will equal 6)
  - the following input is NOT ok: “1,\n” (not need to prove it - just clarifying)
- Support different delimiters : to change a delimiter, the beginning of the string will contain a separate line that looks like this: “//[delimiter]\n[numbers…]” for example “//;\n1;2” should return three where the default delimiter is ‘;’ .
the first line is optional. all existing scenarios should still be supported
- Calling Method with a negative number will throw an exception “negatives not allowed” - and the negative that was passed. if there are multiple negatives, show all of them in the exception message.
- Numbers bigger than 1000 should be ignored, so adding 2 + 1001 = 2
- Delimiters can be of any length with the following format: “//[delimiter]\n” for example: “//[***]\n1***2***3” should return 6

## Tasks



Establish quality parameters:

- Ensure  maximum complexity (CCN) per function == 3

- Ensure 100% line and branch coverage at every step

  

Start Test-driven approach

1. Write the smallest possible failing test: give input `"" assert output to be 0 ` .
2. Write the minimum amount of code that'll make it pass.
3. Refactor any assumptions, continue to pass this test. Do not add any code without a corresponding test.

**Gherkin Language:**

Feature: StringCalculator Add method

  Scenario: Empty string returns 0
    Given the input is ""
    When I call Add method
    Then the result should be 0

  Scenario: Single number returns the number itself
    Given the input is "1"
    When I call Add method
    Then the result should be 1

  Scenario: Two numbers separated by comma return their sum
    Given the input is "1,2"
    When I call Add method
    Then the result should be 3

  Scenario: Unknown amount of numbers separated by commas returns their sum
    Given the input is "1,2,3,4"
    When I call Add method
    Then the result should be 10

  Scenario: Numbers separated by commas and new lines return their sum
    Given the input is "1\n2,3"
    When I call Add method
    Then the result should be 6

  Scenario: Input with invalid delimiter placement is not supported
    Given the input is "1,\n"
    When I call Add method
    Then an error is thrown

  Scenario: Custom single-character delimiter returns sum
    Given the input is "//;\n1;2"
    When I call Add method
    Then the result should be 3

  Scenario: Negative numbers throw an exception listing all negatives
    Given the input is "1,-2,-3"
    When I call Add method
    Then an exception is thrown with message "negatives not allowed: -2, -3"

  Scenario: Numbers greater than 1000 are ignored in sum
    Given the input is "2,1001"
    When I call Add method
    Then the result should be 2

  Scenario: Custom delimiter of any length returns sum
    Given the input is "//[***]\n1***2***3"
    When I call Add method
    Then the result should be 6


**Tabular Form**

## StringCalculator - Test Specification

| Test Case ID | Description                                   | Input                  | Expected Output / Behavior                        | Notes                                  |
|--------------|-----------------------------------------------|------------------------|--------------------------------------------------|----------------------------------------|
| TC01         | Empty string returns 0                         | `""`                   | `0`                                              | Base case                             |
| TC02         | Single number returns the number itself       | `"1"`                  | `1`                                              |                                        |
| TC03         | Two numbers separated by comma return sum     | `"1,2"`                | `3`                                              |                                        |
| TC04         | Unknown amount of numbers separated by commas | `"1,2,3,4"`            | `10`                                             |                                        |
| TC05         | Numbers separated by commas and new lines     | `"1\n2,3"`             | `6`                                              | Newlines as valid delimiters          |
| TC06         | Invalid delimiter placement (unsupported)     | `"1,\n"`                | Error / Exception                                | No need to support or test explicitly |
| TC07         | Custom single-character delimiter returns sum | `"//;\n1;2"`           | `3`                                              | Custom delimiter format                |
| TC08         | Negative numbers throw exception listing all  | `"1,-2,-3"`            | Exception: "negatives not allowed: -2, -3"       | Must list all negatives in message    |
| TC09         | Numbers greater than 1000 are ignored          | `"2,1001"`             | `2`                                              | Numbers > 1000 excluded from sum      |
| TC10         | Custom delimiter of any length returns sum     | `"//[***]\n1***2***3"` | `6`                                              | Delimiters can be longer than 1 char  |

