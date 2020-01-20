# [30. 串联所有单词的子串](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)
### 题意
给定一个字符串s和一些长度相同的单词words。找出s中恰好可以由words中所有单词串联形成的子串的起始位置。

注意子串要与words中的单词完全匹配，中间不能有其他字符，但不需要考虑words中单词串联的顺序。

示例 1：

输入：
  s = "barfoothefoobarman",  
  words = ["foo","bar"]
### 思路
map记录单词，直接遍历即可。
也可以用题解里的思路，用滑动窗口。
### 代码
```cgo
    vector<int> findSubstring(string s, vector<string>& words) {
        vector<int> ans;
        if(words.size() <=0 )return ans;
        if(words[0].size() <= 0) return ans;
        if(words[0].size()*words.size() > s.size()) return ans;

        map<string,int> wordCount;
        int index =1;
        for(int i=0; i<words.size(); i++) {
            wordCount[words[i]] += 1;
        }

        int oneWordLen=words[0].size(), allLen=oneWordLen*words.size();
        int maxIndex=s.size()-allLen;
        map<string, int> subCount;
        for(int i=0; i<=maxIndex; i++) {
            subCount.clear();
            int count =0;
            int k=0;

            while(i+k<=s.size()-oneWordLen) {
                string subStr=s.substr(i+k, oneWordLen);
                k+=oneWordLen;
                if(wordCount[subStr]>0) {
                    subCount[subStr]+=1;

                    if(subCount[subStr]<= wordCount[subStr]) {
                        count ++;
                        if(count == words.size()) {
                            ans.push_back(i);
                            break;
                        }
                    }else {
                        break;
                    }
                }else{
                    break;
                }
            }
        }
        return ans;
    }
```