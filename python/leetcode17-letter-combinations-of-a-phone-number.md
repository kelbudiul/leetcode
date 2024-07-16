```python
class Solution:

    def letterCombinations(self, digits: str) -> List[str]:
        # If the input is empty, return an empty list
        if not digits:
            return []
            
        # Mapping of digits to letters
        phone_map = {
            '2': 'abc',
            '3': 'def',
            '4': 'ghi',
            '5': 'jkl',
            '6': 'mno',
            '7': 'pqrs',
            '8': 'tuv',
            '9': 'wxyz'
        }
        
        def backtrack(combination: str, next_digits: str) -> None:
            # If there are no more digits to check
            if len(next_digits) == 0:
                # The combination is done
                output.append(combination)

            # If there are still digits to check
            else:
                # Iterate over all letters which map the next available digit
                for letter in phone_map[next_digits[0]]:
                    # Append the current letter to the combination
                    # and proceed to the next digits
                    backtrack(combination + letter, next_digits[1:])

        output: List[str] = []
        backtrack("", digits)
        return output
```