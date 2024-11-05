# 算法笔记

## 滑动窗口
一、代码块模板：
```
function minWindow(s ,t) {
    const need = {};
    const window = {};
    for (const c of t) {
        need[c] = (need[c] || 0) + 1;
    }

    // 记录滑动窗口[left, right)
    let left = 0;
    let right = 0;
    let valid = 0; // 记录窗口中满足need条件的字符个数
    let start = 0;
    let len = Infinity;
    while (right < s.length) {
        const c = s[right];
        right++;
        if (need[c]) {
            window[c] = (window[c] || 0) + 1;
            if (window[c] === need[c]) {
                valid++;
            }
        }

        // 判断左侧窗口是否要收敛
        while (valid === Object.keys(need).length) {
            // 更新最小覆盖子串
            if (right - left < len) {
                start = left;
                len = right - left;
            }
            const d = s[left];
            if (need[d]) {
                if (window[d] === need[d]) {
                    valid--;
                }
                window[d]--;
            }
        }
    }
    return len === Infinity ? '' : s.substring(start, start + len);
}
```

## 回溯算法
一、站在回溯树的一个节点上，只需要考虑3个问题：
* 路径：也就是已经做出的选择
* 选择列表：也就是你当前可以做的选择
* 结束条件：也就是到达决策树底层，无法再做选择的条件