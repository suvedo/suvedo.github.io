### [LeetCode 678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/description/)

**题目描述：**输入一个仅包含```'(',')'```和```'*'```的字符串，判断字符串左右括号是否匹配，其中```'*'```可表示左括号，右括号或者为空。

**题目分析：**</br></br>
_方法一：动态规划_</br>
要计算```[i, j]```区间内的左右括号是否匹配，可以计算```[i, k]``` 和```[k + 1, j]```区间的字符串是否同时匹配，
（其中```i <= k < j```）,如果有一个k值能匹配，说明```[i, j]```匹配，否则，还需要看整个```[i, j]```区间是否匹配:
如果```s[j] == '('```或者```s[i] == ')'```，则不能匹配；否则，如果```s[j] == ')'```且```s[i] == '('``` 
或者 ```s[i] == '*'``` 或者 ```s[j] == '*'```，```dp[i][j] == dp[i + 1][j - 1]```.

```
class Solution {
public:
    bool checkValidString(string s) {
        int n = s.size();
        if(n == 0) return true;
        vector<vector<bool>> dp(n + 1, vector<bool>(n + 1, false));
        for(int i = 0; i < n; i ++) {
            if(s[i] == '*') dp[i][i] = true;
            dp[i + 1][i] = true;
        }
        for(int k = 1; k < n; k ++) {
            for(int i = 0; i + k < n; i ++) {
                if(s[i] == ')' || s[i + k] == '(') continue;
                if(s[i + k] == ')' && s[i] == '(' || s[i] == '*' || s[i + k] == '*') {
                    dp[i][i + k] = dp[i + 1][i + k - 1];
                }
                if(dp[i][i + k]) continue;
                for(int j = i; j < i + k; j ++) {
                    if(dp[i][j] && dp[j + 1][i + k]) {
                        dp[i][i + k] = true;
                        break;
                    }
                }
            }
        }
        return dp[0][n - 1];
    }
};
```
时间复杂度:O(n^3),空间复杂度:O(n^2)

_方法二：greedy + stack_</br>
