# MPIN Validator

## Overview
MPIN Validator is a Python-based utility that evaluates the strength of a 4-digit or 6-digit Mobile PIN (MPIN). It checks if the MPIN is commonly used and whether it is derived from a user's demographic details such as Date of Birth, Wedding Anniversary, or Spouse's Birthday.

## Features
- **Commonly Used MPIN Check**: Detects if an MPIN is from a predefined list of commonly used PINs.
- **Demographic-Based Weakness Check**: Evaluates if an MPIN is derived from user-provided DOB, Spouse's DOB, or Anniversary.
- **Strength Evaluation**: Categorizes MPINs as `STRONG` or `WEAK`.
- **Multiple Weakness Reasoning**: If weak, provides an array of reasons such as:
  - `COMMONLY_USED`
  - `DEMOGRAPHIC_DOB_SELF`
  - `DEMOGRAPHIC_DOB_SPOUSE`
  - `DEMOGRAPHIC_ANNIVERSARY`
- **Support for Both 4-Digit and 6-Digit MPINs**

## Installation

Ensure you have Python installed (version 3.6 or later). Clone the repository and navigate to the project directory:
```sh
$ git clone https://github.com/your-repo/mpin_check.git
```

## Usage
Run the main script and provide input as needed:
```sh
$ python src/mpin_validator.py
```
Alternatively, the function `evaluate_mpin(mpin, dob=None, spouse_dob=None, anniversary=None)` can be used in Python scripts.

### Example Usage
```python
from src.mpin_validator import evaluate_mpin

mpin = "1234"
result = evaluate_mpin(mpin)
print(result)  # Output: ('WEAK', ['COMMONLY_USED'])

mpin = "0201"
dob = "02011998"
result = evaluate_mpin(mpin, dob)
print(result)  # Output: ('WEAK', ['DEMOGRAPHIC_DOB_SELF'])
```

## Project Structure
```
mpin-validator/
│── src/
│   ├── mpin_validator.py  # Main logic for evaluating MPIN
│   ├── test_mpin_validator.py  # Unit tests
│── requirements.txt  # Dependencies (if any)
│── README.md  # Documentation
```

## Running Tests
To validate the implementation, run the test cases:
```sh
$ python -m unittest discover tests
```
The test suite covers:
- Commonly used MPINs
- MPINs based on demographics
- Multiple reasons for weakness
- Strong MPIN cases
- Edge cases (empty or random MPINs)

## Example Test Cases
| MPIN  | DOB       | Spouse DOB | Anniversary | Expected Output |
|-------|----------|------------|------------|----------------|
| 1234  | -        | -          | -          | ('WEAK', ['COMMONLY_USED']) |
| 0201  | 02011998 | -          | -          | ('WEAK', ['DEMOGRAPHIC_DOB_SELF']) |
| 9802  | 02011998 | -          | -          | ('WEAK', ['DEMOGRAPHIC_DOB_SELF']) |
| 0403  | -        | -          | 04032020   | ('WEAK', ['DEMOGRAPHIC_ANNIVERSARY']) |
| 6271  | 01011990 | 02021991   | 03031992   | ('STRONG', []) |
| 777777| -        | -          | -          | ('WEAK', ['COMMONLY_USED']) |


## License
This project is licensed under the MIT License.

