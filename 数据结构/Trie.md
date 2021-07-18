

- 使用数组模拟

```
int son[N][26];
son[N][26]这个数组表示的是，一个字符串通过26个字母组成，且长度不会超过N，所以开son数组开成[N][26]。

int cnt[N];
cnt[N]这个数组是用来记录在一个位置上被打上了多少次标记，该位置上打上的标记次数等于这个字符串出现的字数。
或者是bool cnt[N]  表示这个字符串是否出现

int idx;
idx 用来记录每一个字符的所在位置，方便后面询问（Query）时查找，表示现在最新的可用的下标是多少（和单、双链表中idx的作用类似）。

```

```c++
void Insert(char str[]){
    int p = 0;  /* 0表示根节点，0同时也表示节点为空（但在p = 0这里不是代表为空的意思），每次从根节点开始寻找 */
    for(int i = 0; str[i]; i++){
        int u = str[i] - 'a';   /* 将字母转换成数字，方便之后存入Trie树中 */
        if(!son[p][u]) son[p][u] = ++ idx;  /* 如果字符串中的某一个字符在Trie树中不存在，则创建该字符的节点 */
        p = son[p][u];  /* 此时的p就是str中最后一个字符对应的trie树的位置idx。 */
    }
    cnt[p]++;   /* 在p这个位置上打上标记，每加一次说明这一个字符串出现了一次 */
}

int Query(char str[]){
    int p = 0;
    for (int i = 0; str[i]; i++){
        int u = str[i] - 'a';
        if (!son[p][u]) return 0;
        p = son[p][u];
    }
    return cnt[p];
}

```

[835. Trie字符串统计 - AcWing题库](https://www.acwing.com/problem/content/837/)



[208. 实现 Trie (前缀树) - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

