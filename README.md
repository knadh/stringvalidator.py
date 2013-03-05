# stringvalidator.py
Aa simple string validator class in Python for basic data validation such as checking
if a string is alpha, alphanumeric, e-mail etc.

Kailash Nadh, March 2013

License:	MIT License

Documentation: http://nadh.in/code/stringvalidator.py

## Validation checks
<table border="1">
	<thead>
		<tr>
			<td>Check</td>
			<td>Description</td>
			<td>Arguments</td>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>is_numeric</td>
			<td>Check if a string is numeric (123, 12.3, -12.3 etc.)</td>
			<td></td>
		</tr>
		<tr>
			<td>is_alpha</td>
			<td>Check if a string is alphabetical (a-z only)</td>
			<td></td>
		</tr>
		<tr>
			<td>is_alphanumeric</td>
			<td>Check if a string is alphanumeric (a-z and 0-9)</td>
			<td></td>
		</tr>
		<tr>
			<td>is_integer</td>
			<td>Check if a string is an integer (1, -1, 0, but not 1.1)</td>
			<td></td>
		</tr>
		<tr>
			<td>is_float</td>
			<td>Check if a string is a float (1.0, -2.0, but not 1)</td>
			<td></td>
		</tr>
		<tr>
			<td>longer_than</td>
			<td>Check if a string is longer than a given length</td>
			<td>(length)</td>
		</tr>
		<tr>
			<td>shorter_than</td>
			<td>Check if a string is shorter than a given length</td>
			<td>(length)</td>
		</tr>
		<tr>
			<td>is_email</td>
			<td>Check if a given string is a valid e-mail</td>
			<td></td>
		</tr>
		<tr>
			<td>is_tld</td>
			<td>Check if a given string is a top level domain (www.site.com, site.com, but not a.b.site.com)</td>
			<td></td>
		</tr>
		<tr>
			<td>is_handle</td>
			<td>Check if a given string is a valid username handle containing only alphanumeric and _ (username, username9, user_name, 1user ...)</td>
			<td></td>
		</tr>
	</tbody>
</table>

## Usage
Any number of conditions can be chained and passed to the ```StringValidator.validate()``` method.

```StringValidator.validate(input, [checks], log)```

- ```input``` is the input string to be validated. It is always stripped of preceding and trailing spaces

- ```checks``` is the chained list of checks. Checks with arguments are passed as tuples

- ```log``` is an optional boolean flag. If set to ```False```(default), ```StringValidator.validate()``` simply
returns ```True, False``` if all checks pass, or one of the checks fail, respectively.
If set to ```False```, ```True``` is returned if all checks pass, or a ```dict``` containing
what failed and passed is returned. Example:

```
{
	'not_empty': True,
	'is_email': False
}
```

### Examples
```
from StringValidator import StringValidator

validator = StringValidator()

input = "user@email.com"
validator.validate(input, ['is_email'])
# => True

input = "user@email.com"
validator.validate(input, ['is_email', ('longer_than', 20)])
# => False

input = "123.4"
validator.validate(input, ['not_empty', ('shorter_than', 5), 'is_float'])
# => True

input = "123.4"
validator.validate(input, ['is_float', ('longer_than', 5), ('shorter_than', 10)])
# => True


input = "123"
validator.validate(input, ['not_empty', 'is_alpha'], True)
# => {
	'not_empty': True,
	'is_alpha': False
}
```