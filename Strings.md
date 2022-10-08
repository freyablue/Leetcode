#### 12. Integer to Roman(medium)
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given an integer, convert it to a roman numeral.

````
class Solution:
    def intToRoman(self, num: int) -> str:
        symbols = [['M',1000],['CM',900],['D',500],['CD',400],['C',100],['XC',90],['L',50],['XL',40],['X',10],['IX',9],['V',5],['IV',4],['I',1]]
        n = len(symbols)
        i = 0
        curr = symbols[i][1]
        s = ""
        while num!=0 and i<n:
            if num//curr>=1:
                s = s+symbols[i][0]
                num = num-curr
            elif num//curr<1:
                i=i+1
            curr = symbols[i][1]
        return s
````

#### 13. Roman to Integer(easy)

````
class Solution:
    def romanToInt(self, s: str) -> int:
        symbols = {'M':1000,'CM':900,'D':500,'CD':400,'C':100,'XC':90,'L':50,'XL':40,'X':10,'IX':9,'V':5,'IV':4,'I':1}
        result = 0
        string = ""
        i = 0
        while i<len(s):
            string = str(s[i])+str(s[i+1]) if i<len(s)-1 else ""
            if string in symbols:
                result = result+symbols[string]
                i+=2
            else:
                result = result+symbols[str(s[i])]
                i+=1
        return result
````