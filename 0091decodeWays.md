The idea is to use dynamic programming, you should have an array of size of the input s in mind, i.e. int[n] where n = s.length();  


**Notations**  
We use s(0,i) to denote the substring of s from index i to index i-1. We define the i'th entry in this array, denoted $r_i$,  as follows:

$r_i :=$ # of ways of decoding the substring s(0,i).

After reading the recursive relation, you should notice that we only need to keep track of $r_{i-1}, r_{i-2}$

**Special Cases**  
Some special cases we should have in mind includes:

invalid:  

1. s= "230"  there are no >26 character and 0x character  
2. s= "0123" starting with 0 is meaningless (i.e. can't decode)  
3. s= "1003"  two consecutive 0's is meaningless

valid:  

1. s= "120" 

**dp recursive relation**    
Now the recursive relation is as follows:

1. if the value of s(i-1, i+1) is valid (i.e. <= 26) and is not unique (i.e. not 10, 20) : $r_i = r_{i-1} + r_{i-2}$.  
2. if the value of s(i-1, i+1) is valid and is unique : $r_i = r_{i-2}$. Since there is no compromise for 0 digit, $r_{i-1}$ is set to 0: $r_{i-1} = 0$.  
3. if the value of s(i-1, i+1) is NOT valid, then you can only decompose it into two single codewords: $r_i=r_{i-1}$.  


Along the way, three things must be checked:  

1. the input doesn't start with 0  
2. the input doesn't contain two consecutive 0's  
3. the input doesn't contains invalid codes x0: 30, 40 ...


```
class Solution {
    public int numDecodings(String s) {
        if (s.length() == 0) return 0;
        
        //check invalid condition 1
        if (s.charAt(0) == '0') return 0;
        
        int res0 = 1; int res1 = 1; int i = 1;
        while (i<s.length()) {
            //check invalid conditions 2,3
            if (s.charAt(i) == '0' && (s.charAt(i-1) == '0'|| s.charAt(i-1)-'0' >= 3 )) {
                return 0;
            } else if (Integer.valueOf(s.substring(i-1, i+1)) <= 26 && s.charAt(i) != '0') {
                int mid = res1;
                res1 = res0 + res1;
                res0 = mid;
                i++;
            } else if (Integer.valueOf(s.substring(i-1, i+1)) <= 26 && s.charAt(i) == '0') {
                res1 = res0;
                res0 = 0;
                i++;
            }else {
                res0 = res1;
                i++;
            }
        }
        return res1;
    }
}
```