# Intuition
This problem requires us to design a program (codes) that converts integer to roman.
## Algorithm
- First of all, we need a 'dictionary' telling us how 
to map different digits to roman. This can be done by dictionary in Python (hashmap in Java). 
- Then according to the description, we know the convertion take place from the left of the integer, i.e., we first convert larger digits.
So we sort the dictionary by its key from large to small and obtain a key list with different integers.
- We loop over the key list. For each key (integer), we need to know how many corresponding roman strings are needed 
so we do division(floor). Then we convert digits from the input number larger than this integer to roman successfully, 
and go to smaller digits.
- Each time we complete a conversion, we need to substract the converted part from the input number and look at the remaining value 
in the following step.

## Example
For example, we have input number 2984. We first look for how many '1000' we need and find we need two. So we get 'M'*2 which is 'MM'.
Then we look for how many '900' we need and get 'CM'. There is no '500', '400', '100' or '90' needed, so we go to '50' and get 'L'.
After that we need three '10' to reach 80 and one '4' to get 4. That is, 'X'*3 and 'IV'*1. Finally, we add all these stuffs and get 
"MMCMLXXXIV".

# Code
```python
class Solution:
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        # create a dictionary
        roman_dict = {1:'I',4:'IV',5:'V',9:'IX',10:'X',40:'XL',50:'L',90:'XC',100:'C',400:'CD',500:'D',900:'CM',1000:'M'}
        key_list = sorted(list(roman_dict.keys()))[::-1]  # sort the keys(integers) from large to small
        
        # output roman string
        roman = ''
        for k in key_list:
            k_num = num//k
            k_string = roman_dict[k]*k_num
            roman = roman+k_string
            num = num-k_num*k
            
        return roman
```
# Runtime and space complexity
We use constant time and space to construct the dictionary and so is the sort.
In the conversion step, the most time-consuming part is that the input number divided by 1000, which may be related to large integer
division. Denote the number of digits in the input number by n, then this step has runtime O(nlogn). After that the runtime is constant
since the loop length is constant. And we don't use extra space in this step.\
So the runtime is O(nlogn) and space is O(1).



