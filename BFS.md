## 广度优先搜索

### 核心
BFS的核心思想，就是把一些问题抽象成图，从一个点开始，向四周开始扩散。BFC相对DFS的最主要的区别是：BFS找到的路径一定是最短的，但代价就是空间复杂度可能比DFS大很多。

### 框架
```
function BFC(start, target) {
    // 核心数据结构
    const q = [];

    // 避免走回头路
    const visited = new Set();
    let setp = 0;

    // 将起点加入队列
    q.push(start);
    visited.add(start);

    while (q.length > 0) {
        const sz = q.length;
        
        // 将当前队列中的所有节点向四周扩散
        for (let i = 0; i < sz; i++) {
            const cur = q.shift();
            // 划重点：这里判断是否达到终点
            if (cur === target) {
                return step;
            }

            // 将cur的相邻节点加入队列
            const adj = cur.adj();
            for (let j = 0; j < adj.length; j++) {
                const x = adj[j];
                if (!visited.has(x)) {
                    q.push(x);
                    visited.add(x);
                }
            }
        }
    }
    、、
}
```