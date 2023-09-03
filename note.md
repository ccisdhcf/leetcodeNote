# 9. Palindrome Number
## sol 1 python bad alg
```python
    def palindrome(x):
        
        result = True
        for i in range(int(len(str(x)) / 2)):
            if str(x)[i] != str(x)[len(str(x)) - 1 - i]:
                result = False
                break
            # result = result and (str(x)[i] == str(x)[len(str(x)) - 1 - i])
        return result
        
        if x < 0:
            return False
```


## sol 2 python
```python
    def palindrome(x):
    
        half_len = len(str(x)) / 2
        # print(half_len, end="\n")
        reverse_num = 0
        oddEvenBool = half_len.is_integer()
        for i in range(int(half_len)):
            # print(i)
            b = x % 10
            x //= 10
            reverse_num = b + reverse_num * 10
        
        if not oddEvenBool:
            x //= 10
        # print(reverse_num, end="\n")
        # print(x, end="\n")
        if x == reverse_num:
            return True
        else:
            return False
```


## sol 3 python
```python

    def palindrome(x):
        if x < 0:
            return False
        return str(x) == str(x)[::-1]
```

## sol 4 c++
```c++ 
// similar to sol 2
// C# also work
bool isPalindrome(int x) {
    if(x<0|| (x!=0 &&x%10==0)) return false;
    int sum=0;
    while(x>sum)
    {
        sum = sum*10+x%10;
        x = x/10;
    }
    return (x==sum)||(x==sum/10);
}
```

# 13. Roman to Integer
## keyword: C++ STL unordered_map
### sol1:很醜 可是不慢
```C++
int romanToInt(string s) {
         int result = 0;
    int sLen = s.length();
    for (int i = 0; i < sLen; i++)
    {
        if (s[i] == 'C' && i + 1 < sLen && (s[i + 1] == 'D'||s[i + 1] =='M'))
        {

            switch (s[i + 1])
            {

            case 'D' /* constant-expression */:
                result += 400;
                break;
            case 'M' /* constant-expression */:
                result += 900;
                break;

            default:
                break;
            }
            i++;
        }
         else if (s[i] == 'X' && i + 1 < sLen && (s[i + 1] == 'L'||s[i + 1] == 'C'))
        {

            switch (s[i + 1])
            {
            case 'L' /* constant-expression */:
                result += 40;
                break;
            case 'C' /* constant-expression */:
                result += 90;
                break;
            default:
                break;
            }
            i++;
        }
        else if (s[i] == 'I' && i + 1 < sLen && (s[i + 1] == 'V'||s[i + 1] == 'X'))
        {

            switch (s[i + 1])
            {
            case 'V' /* constant-expression */:
                result += 4;
                break;
            case 'X' /* constant-expression */:
                result += 9;
                break;
            default:
                break;
            }
            i++;
        }
       
        
        else
        {
            switch (s[i])
            {
            case 'I' /* constant-expression */:
                result += 1;
                break;
            case 'V' /* constant-expression */:
                result += 5;
                break;
            case 'X' /* constant-expression */:
                result += 10;
                break;
            case 'L' /* constant-expression */:
                result += 50;
                break;
            case 'C' /* constant-expression */:
                result += 100;
                break;
            case 'D' /* constant-expression */:
                result += 500;
                break;
            case 'M' /* constant-expression */:
                result += 1000;
                break;

            default:
                break;
            }
        }

        // cout << s[i] << " ? " << result << endl;
    }
    return result;
    }
```
### sol2 時間跟sol1一樣，記憶體多了一點，但好看多了
``` C++
int romanToInt(string s) 
{
    unordered_map<char, int> T = { { 'I' , 1 },
                                   { 'V' , 5 },
                                   { 'X' , 10 },
                                   { 'L' , 50 },
                                   { 'C' , 100 },
                                   { 'D' , 500 },
                                   { 'M' , 1000 } };
                                   
   int sum = T[s.back()];
   for (int i = s.length() - 2; i >= 0; --i) 
   {
       if (T[s[i]] < T[s[i + 1]])
       {
           sum -= T[s[i]];
       }
       else
       {
           sum += T[s[i]];
       }
   }
   
   return sum;
}
```

# 14. Longest Common Prefix
### sol1:很醜、又慢
``` C++
string longestCommonPrefix(vector<string> &strs)
{
    int len = 0;
    int shortestStrLen = 200;
    if (strs.size() == 1)
    {
        return strs[0];
    }

    for (string _str : strs)
    {
        if (_str.length() < shortestStrLen)
        {
            shortestStrLen = _str.length();
            
        }
    }
    // cout << shortestStrLen << endl;
    bool NeedBreak = false;
    int resultLen=0;
    for (int i = 0; i < shortestStrLen; i++)
    {
        cout<<"shortestStrLen: "<<shortestStrLen<<endl;
        char _char = strs[0][i];
        for (string  _str:strs)
        {
            if (!NeedBreak)
            {
                
                NeedBreak = NeedBreak || (_str[i] != _char);
                cout << _str[i] << " ?VS? " << _char << endl;

            }
            else{
                // cout <<"out1 ,resultLen:"<<resultLen<<endl;
                // return strs[0].substr(0, resultLen);
                break;
            }
            
        }
        resultLen=i;
        if (NeedBreak)
        {
            cout <<"out2"<<endl;
            return strs[0].substr(0, resultLen);
        }
       }
    cout <<"out3"<<endl;
    return strs[0].substr(0, shortestStrLen);
  
}
```
### sol2 漂亮
``` c++
string longestCommonPrefix(vector<string>& s) {
    int ans = s[0].length(), n = s.size();
    for(int i=1; i<n; i++){
        int j = 0;
        while(j<s[i].length() && s[i][j]==s[0][j])j++;
            ans = min(ans, j);
        }
    return s[0].substr(0, ans);
}
```

# 20. Valid Parentheses
### sol1: by me ,100% 81%
``` c++
class Solution {
public:
    bool isValid(string s) {
        stack<char> subString;
    for (int i = 0; i < s.length(); i++)
    {
        switch (s[i])
        {
        case '(':
            subString.push('(');
            break;
        case '[':
            subString.push('[');
            break;
        case '{':
            subString.push('{');
            break;
        case ')':
            //cout << subString.top() << endl;
            if (subString.empty()|| subString.top() != '(')
            {
                return false;
            }
            else {
                subString.pop();
            }
            break;
        case ']':
            
            if (subString.empty() || subString.top() != '[') {
                return false;
            }
            else {
                subString.pop();

            }
            break;
        case '}':
            if (subString.empty() || subString.top() != '{') {
                return false;

            }
            else {
                subString.pop();

            }
            break;

        default:
            break;
        }
    }
    if (subString.empty()) {
        return true;
    }
    else {
        return false;
    }
};
};
```
### sol2 by 哥
``` python
class Solution:
    def isValid(self, s:str) ->bool:
        if len(s)%2!=0:
            return False
        d={'(':')','[':']','{':'}'}
        l=[]
        for bracket in s:
            if bracket in d:
                l.append(bracket)
            elif len(l)==0 or d[l.pop()]!=bracket:
                return False
        return len(l)== 0
```
### sol 3 from leetcode  這個厲害XD
``` c++
bool isValid(string s)
    {
        stack<char> st;
        for(char &ch:s)
        {
            if(ch=='(')
               st.push(')');
            else if(ch=='{')
               st.push('}');
            else if(ch=='[')
               st.push(']');
            else
            {
                if(st.empty() || ch!=st.top())
                   return false;
                else
                   st.pop();
            }
        }
        return st.empty();
    }
```
# 21. Merge Two Sorted Lists
### sol1:recursive by leetcode

``` c++
class Solution {
public:
	ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) 
  {
		// if list1 happen to be NULL
		// we will simply return list2.
		if(l1 == NULL)
        {
			return l2;
		}
		
		// if list2 happen to be NULL
		// we will simply return list1.
		if(l2 == NULL)
        {
			return l1;
		} 
		
		// if value pointend by l1 pointer is less than equal to value pointed by l2 pointer
		// we wall call recursively l1 -> next and whole l2 list.
		if(l1 -> val <= l2 -> val)
        {
			l1 -> next = mergeTwoLists(l1 -> next, l2);
			return l1;
		}
		// we will call recursive l1 whole list and l2 -> next
		else
        {
			l2 -> next = mergeTwoLists(l1, l2 -> next);
			return l2;            
		}
	}
};	
```

### sol2:iterative by leetcode
##### 我也這麼寫@@
``` c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
       
	    // if list1 happen to be NULL
		// we will simply return list2.
        if(list1 == NULL)
            return list2;
		
		// if list2 happen to be NULL
		// we will simply return list1.
        if(list2 == NULL)
            return list1;
        
        ListNode * ptr = list1;
        if(list1 -> val > list2 -> val)
        {
            ptr = list2;
            list2 = list2 -> next;
        }
        else
        {
            list1 = list1 -> next;
        }
        ListNode *curr = ptr;
        
		// till one of the list doesn't reaches NULL
        while(list1 &&  list2)
        {
            if(list1 -> val < list2 -> val){
                curr->next = list1;
                list1 = list1 -> next;
            }
            else{
                curr->next = list2;
                list2 = list2 -> next;
            }
            curr = curr -> next;
                
        }
		
		// adding remaining elements of bigger list.
        if(!list1)
            curr -> next = list2;
        else
            curr -> next = list1;
            
        return ptr;
       
    }
};
```

### sol3 python 
``` python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        newHead = dummyHead = ListNode()
        while list1 and list2:
            if list1.val < list2.val:
                dummyHead.next = list1
                list1 = list1.next
            else:
                dummyHead.next = list2
                list2 = list2.next
            dummyHead = dummyHead.next
        
        if list1:
            dummyHead.next = list1
        if list2:
            dummyHead.next = list2
        return newHead.next
```

# 122. Best Time to Buy and Sell Stock II

### sol1 python greedy
``` python
    def maxProfit(self, prices: List[int]) -> int:
        result=0
        for i in range(len(prices)-1):
            if prices[i+1]>prices[i]:
                result+=prices[i+1]-prices[i]
        return result
```

### sol2 dp buttom-up
``` python
    def maxProfit(self, prices: List[int]) -> int:
        
		# It is impossible to sell stock on first day, set -infinity as initial value for cur_hold
        cur_hold, cur_not_hold = -float('inf'), 0
        
        for stock_price in prices:
            
            prev_hold, prev_not_hold = cur_hold, cur_not_hold
            
			# either keep hold, or buy in stock today at stock price
            cur_hold = max( prev_hold, prev_not_hold - stock_price )
			
			# either keep not-hold, or sell out stock today at stock price
            cur_not_hold = max( prev_not_hold, prev_hold + stock_price )
            
        # maximum profit must be in not-hold state
        return cur_not_hold
```

### sol 3 dp top-down
``` python
    def maxProfit(self, prices: List[int]) -> int:
        
        @cache
        def trade(day_d):
            
            if day_d == 0:
                
                # Hold on day_#0 = buy stock at the price of day_#0
                # Not-hold on day_#0 = doing nothing on day_#0
                return -prices[day_d], 0
            
            prev_hold, prev_not_hold = trade(day_d-1)
            
            hold = max(prev_hold, prev_not_hold - prices[day_d] )
            not_hold = max(prev_not_hold, prev_hold + prices[day_d] )
            
            return hold, not_hold
        
        # --------------------------------------------------
        last_day= len(prices)-1
        
        # Max profit must come from not_hold state (i.e., no stock position) on last day
        return trade(last_day)[1]
```

# 112. Path Sum
### sol1: dfs
``` python
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        def dfs(targetSum,Node,currectSum):
            if Node!=None:
                currectSum+=Node.val
                if Node.left==Node.right==None:
                    print(currectSum)

                    if currectSum==targetSum:
                        print(currectSum)
                        return True
                        
                if Node.left!=None:
                    if dfs(targetSum,Node.left,currectSum):
                        return True
                    
                if Node.right!=None:
                    if dfs(targetSum,Node.right,currectSum):
                        return True
                  
            return False
        return dfs(targetSum,root,0)
```

### sol2:dfs? bfs 
``` python
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root: return False
        stack = [[root, root.val]]
        while stack:
            node, total = stack.pop()
            if total == targetSum and node.left is None and node.right is None: return True
            if node.right: stack.append([node.right, total + node.right.val])
            if node.left: stack.append([node.left, total + node.left.val])
        return False
```

# 334. Increasing Triplet Subsequence
special test case!!
[1,5,0,4,1,3]
[0,4,1,-1,2]
### sol1
```python
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        # 只在意前一個<下一個 第二個上升結束的數字要大於第一個!
        a,b,c=-1,-1,-1
        for i in range(0,len(nums)-1):
            # print(nums[i],nums[i+1])
            if nums[i]<nums[i+1]:
                if b==-1:
                    a=nums[i]
                    b=nums[i+1]
                else:
                    if a<nums[i]<b:
                        b=nums[i]
                        print("!!",a,b)
                    if nums[i+1]>b:
                        return True
                    
                    if nums[i+1]<b:
                        a=nums[i] if a>nums[i] else a
                        b=nums[i+1]
            elif b!=-1 and b>nums[i+1] and a<nums[i+1]:
                b=nums[i+1]
                # print("??",a,b)

            # print("result",a,b,c)
                    

```

# 468. Validate IP Address
### sol1 bug!!!
``` python
def validIPAddress(self, queryIP: str) -> str:
        # v4:
        def checkV4(_queryIP):
            IPList=_queryIP.split(".")
            if len(IPList)!=4:
                return False
            else :
                #bug example  0.1.2.3
                for i in IPList:
                    if not i.isdigit():
                        return False
                    if str(i)!=str(int(i)):   #leading zeros
                        return False
                    if int(i)>255 or int(i)<0:
                        return False
                return True
        #v6
        def checkV6(_queryIP):
            HexList=['a','b','c','d','e','f','A','B','C','D','E','F']
            IPList=_queryIP.split(":")
            if len(IPList)!=8:
                return False
            else:
                for i in IPList:
                    # print("???",i,type(i))
                    if len(str(i))>4 or len(str(i))<1:
                        return False
                    for j in i:
                        if not j.isdigit() and not j in HexList:
                            # print(j)
                            return False

                return True
        if checkV4(queryIP):
            return "IPv4"
        elif checkV6(queryIP):
            return "IPv6"
        else:
            return "Neither"
```
### sol2
``` python
class Solution:
    def validate_IPv4(self, IP: str) -> str:
        nums = IP.split('.')
        for x in nums:
            # Validate integer in range (0, 255):
            # 1. length of chunk is between 1 and 3
            if len(x) == 0 :
                return "Neither"
            elif len(x) > 3:
                return "Neither"
            if not x.isdigit() or int(x) > 255:
                return "Neither"
            if x[0] == '0' and len(x) != 1:
                return "Neither"
        return "IPv4"
    
    def validate_IPv6(self, IP: str) -> str:
        nums = IP.split(':')
        hexdigits = '0123456789abcdefABCDEF'
        for x in nums:
            # Validate hexadecimal in range (0, 2**16):
            # 1. at least one and not more than 4 hexdigits in one chunk
            # 2. only hexdigits are allowed: 0-9, a-f, A-F
            if len(x) == 0 or len(x) > 4 or not all(c in hexdigits for c in x):
                return "Neither"
        return "IPv6"
        
    def validIPAddress(self, IP: str) -> str:
        if IP.count('.') == 3:
            return self.validate_IPv4(IP)
        elif IP.count(':') == 7:
            return self.validate_IPv6(IP)
        else:
            return "Neither"
```



# 566. Reshape the Matrix
### sol1
``` python
    def matrixReshape(self, mat: List[List[int]], r: int, c: int) -> List[List[int]]:
        Orow=len(mat)
        Ocol=len(mat[0])
        if Orow*Ocol !=r*c:
            return mat
        else:
            counter=1
            result=[]
            temp=[]
            for i in range(len(mat)):
                for j in range(len(mat[0])):
                    if (counter)%c !=0:
                        temp.append(mat[i][j])
                        counter+=1
                    else:
                        temp.append(mat[i][j])
                        result.append(temp)
                        temp=[]
                        counter+=1
            return result
```
### sol2
``` python
    def matrixReshape(self, mat: List[List[int]], r: int, c: int) -> List[List[int]]:
        if len(mat[0])*len(mat) != r* c:
            return mat
        elements = [element for row in mat for element in row]   #flatten
        ret = [elements[i:i+c] for i in range(0, r*c, c)]
        return ret
```

# 188.  Best Time to Buy and Sell Stock IV
### so1l dp:
``` python 
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        # no transaction, no profit
        if k == 0: return 0
        # dp[k][0] = min cost you need to spend at most k transactions
        # dp[k][1] = max profit you can achieve at most k transactions
        dp = [[1000, 0] for _ in range(k + 1)]
        for price in prices:
            for i in range(1, k + 1):
                # price - dp[i - 1][1] is how much you need to spend
                # i.e use the profit you earned from previous transaction to buy the stock
                # we want to minimize it
                dp[i][0] = min(dp[i][0], price - dp[i - 1][1])
                # price - dp[i][0] is how much you can achieve from previous min cost
                # we want to maximize it
                dp[i][1] = max(dp[i][1], price - dp[i][0])
        # return max profit at most k transactions
		# or you can write `return dp[-1][1]`
        return dp[k][1]
```
### sol2 https://labuladong.github.io/algo/di-ling-zh-bfe1b/yi-ge-fang-3b01b/
``` python
```


# 1286. Iterator for Combination
### sol 1: python itertools.combinations
``` python
class CombinationIterator:

    def __init__(self, characters: str, combinationLength: int):
        self.x = list(itertools.combinations(characters, combinationLength))
        print(self.x)
    def next(self) -> str:
        temp = ""
        for i in (self.x[0]):
            temp+=str(i)
        self.x.pop(0)
        return temp

    def hasNext(self) -> bool:
        if self.x!=[]:
            return True
        else:
            return False

```
### sol 2:
[leetcode Link](https://leetcode.com/problems/iterator-for-combination/solutions/1576856/all-5-solutions-w-detailed-explanations-bitmask-backtrack-on-the-fly-gosper-s-hack/)

#### 2-1 Optmized Bit-manipulation
``` c++
class CombinationIterator {
    string s;
    int n, L, mask = 0;
    bool has_next = true;
public:                            //  initially set bits corresponding ↓ to 1st n bits of s
    CombinationIterator(string s, int n) : s(s), L(size(s)), n(n), mask((1<<n)-1 << L-n) { }
    string next() {
        string combination = "";
        for(int j = L-1; j >= 0; j--)             // iterate over mask from MSB to LSB
                if(mask & 1 << j)                 // if a bit is set,
                    combination += s[L-1-j];      // then add character corresponding to that bit
        updateMask();                             // move to next mask
        return combination;
    }
    void updateMask() {
        int rightMostBit = mask & -mask;            // get right-most set bit
        if(rightMostBit != 1) {                     // if last bit(LSB) is not set, just right-shift
            mask ^= rightMostBit;                   // unset right-most bit
            mask |= rightMostBit>>1;                // and set its right-adjacent bit
        } 
        else {
            // all 1s occur adjacently at right-end means we explored all
            if((mask & (mask + 1)) == 0) { has_next = false; return; } 
            
            int rightOnesCnt = 0, pos = 0;           // get group of continous 1s at right
            while(mask & 1 << pos) {
                mask ^= 1 << pos;                    // unset these group of 1s
                rightOnesCnt++, pos++;
            }
            int rightMostBit = mask & -mask;         // now get rightmost set bit position & right-shift it
            mask ^= rightMostBit;                    // First: unset it
            mask |= rightMostBit >>= 1;              // Then : set its right-adjacent
            while(rightOnesCnt--)                    // paste rightmost group of 1s that we had unset above /
                mask |= rightMostBit >>= 1;          // right-adjacent to rightMostBit that was right-shifted above
        }
    }
    bool hasNext() { return has_next; }
};
```
#### 2-2 Optimized Bit-manipulation - Gosper's Hack
``` c++
class CombinationIterator {
    string s;
    int n, L, mask = 0;
    bool has_next = true;
public:
    CombinationIterator(string s, int n) : s(s), L(size(s)), n(n), mask((1<<n)-1 << L-n) { }
    string next() {
        string combination = "";
        for(int j = L-1; j >= 0; j--)             // iterate over mask from MSB to LSB
                if(mask & 1 << j)                 // if a bit is set,
                    combination += s[L-1-j];      // then add character corresponding to that bit
        updateMask();                             // move to next mask
        return combination;
    }
    // using Gospel's hack
    void updateMask() {
        int t = mask + 1, u = t ^ mask, v = t & mask;
        mask = v - (v & -v) / (u + 1);
        has_next = mask;
    }
    bool hasNext() { return has_next; }
```
# 1306. Jump Game III
### sol1 bfs
``` python
def canReach(self, arr: List[int], start: int) -> bool:
        # bfs? set record visited?
        arrLen=len(arr)
        visited=set()
        visited.add(start)
        currVisit=[]
        currVisit.append(start)
        if arr[start]==0:
            return True
        step=1
        while step<arrLen: #bfs
            nextVisit=[]
            while len(currVisit):
                curr=currVisit.pop(0)
                # print("--------------------")
                # print(arr)
                # print(curr)               
                if (curr +arr[curr])<arrLen and (curr +arr[curr]) not in visited:
                    # print(curr +arr[curr])
                    if arr[curr +arr[curr]]==0:
                        return True
                    visited.add(curr +arr[curr])
                    nextVisit.append(curr +arr[curr])
                if (curr -arr[curr])>=0 and (curr -arr[curr]) not in visited:
                    # print(curr -arr[curr])
                    if arr[curr -arr[curr]]==0:
                        return True
                    visited.add(curr -arr[curr])
                    nextVisit.append(curr -arr[curr])
            currVisit=nextVisit.copy()
            step+=1
        return False

```
### sol2 one line
[ref](https://leetcode.com/problems/jump-game-iii/solutions/465602/java-c-python-1-line-recursion/)
``` c++

    bool canReach(vector<int>& A, int i) {
        return 0 <= i && i < A.size() && A[i] >= 0 && (!(A[i] = -A[i]) || canReach(A, i + A[i]) || canReach(A, i - A[i]));
    }
```
### sol3 bfs dfs
[ref](https://leetcode.com/problems/jump-game-iii/solutions/1619031/c-python-simple-solution-w-explanation-dfs-bfs-traversals/)
##### dfs
``` python 
class Solution:
    def canReach(self, A, cur):
        if cur < 0 or cur >= len(A) or A[cur] < 0: return False
        A[cur] *= -1
        return A[cur] == 0 or self.canReach(A, cur + A[cur]) or self.canReach(A, cur - A[cur])
```
##### bfs
``` python
class Solution:
    def canReach(self, A, cur):
        q = deque([cur])
        while q:
            cur = q.popleft()
            if A[cur] == 0: return True
            if A[cur] < 0 : continue
            if cur + A[cur] < len(A): q.append(cur + A[cur])
            if cur - A[cur] >= 0:     q.append(cur - A[cur])
            A[cur] *= -1
        return False
```
# 1346. Check If N and Its Double Exist
check 1 zero or multiple zero in list
### sol 1:  
``` python
    def checkIfExist(self, arr: List[int]) -> bool:
        arrDict={}
        count = arr.count(0)
        if count>1:
            return True
        elif count==1:
            arr.remove(0)

        for i in arr:
            arrDict[i]=i
        for i in arr:
            if i*2 in arrDict.values():
                # print(i/2)
                print(i*2)
                return True
        return False
```
### sol 2 : set
``` python 
    def checkIfExist(self, arr: List[int]) -> bool:
        seen = set()
        for i in range(len(arr)):
            if arr[i] * 2 in seen:
                return True
            elif arr[i] % 2 == 0 and arr[i] / 2 in seen:
                return True
            else:
                seen.add(arr[i])
        return False
```


# 1422. Maximum Score After Splitting a String
### sol1 
``` python
    def maxScore(self, s: str) -> int:
        li=[]
        for i in range(1,len(s)):
            left=s[:i]
            right=s[i:]
            li.append(left.count('0')+right.count('1'))
        return max(li)
```


# 2798. Number of Employees Who Met the Target
### sol 1
``` python
class Solution:
    def numberOfEmployeesWhoMetTarget(self, hours: List[int], target: int) -> int:
        result=0
        for i in hours:
            if i>=target:
                result+=1
        return result
```

### sol2 one line
``` python
 def numberOfEmployeesWhoMetTarget(self, hours: List[int], target: int) -> int:
    return len([it for it in hours if it >= target])
```