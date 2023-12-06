# Mermaid简易教程
# 语法
- 图表标题
    ```markdown
    ---
    title: 标题
    ---
    ```
- 箭头：
    ```markdown
    -->
    ```
- 圆角方框：
    ```markdown
    id("圆角方框")
    ```
- 半圆方框：
    ```markdown
    id(["半圆方框"])
    ```
- 子程序方框：
    ```markdown
    id[["子程序方框"]]
    ```
- 圆柱形：
    ```markdown
    id[("圆柱形")]
    ```
- 圆形：
    ```markdown
    id(("圆形"))
    ```
- 不对称方框：
    ```markdown
    id>"不对称方框"]
    ```
- 菱形：
    ```markdown
    id[/"菱形"/]
    ```
- 六边形：
    ```markdown
    id{{"六边形"}}
    ```
- 平行四边形：
    ```markdown
    id[/"平行四边形"/]
    id[\"平行四边形"\]
    ```
- 梯形：
    ```markdown
    id[/"梯形"\]
    id[\"梯形"/]
    ```
- 双圆形：
    ```markdown
    id((("双圆形")))
    ```
- 图表连接方向：
    ```markdown
    flowchart LR
    或
    flowchart TD
    或
    flowchart TB
    # TB - Top to bottom，从上到下
    # TD - Top-down same as top to bottom，从上向下
    # BT - Bottom to top，从底向上
    # RL - Right to left，从右向左
    # LR - Left to right，从左向右
    ```
- Unicode文本：使用""双引号包裹起来
    ```markdown
    "Unicode文本"
    ```
- 在文本中使用markdown语法显："``" 反引号引用markdown语法
    ```markdown
    "`**加粗**`"
    ```
- 内容换行：
    ```markdown
    idx["a
    b
    c"]
    ```
- 图标类型：
  - 流程图：flowchart、graph

# 示例

## 方块
```mermaid
---
title: 方块
---
flowchart
    id1["方块1"]
    id2["方块2"]
```

或
```mermaid
---
title: 方块
---
graph
    id1["方块1"]
    id2["方块2"]
```
**示例代码**：
```markdown
---
title: 方块
---
flowchart
    id1["方块1"]
    id2["方块2"]
```
或
```markdown
---
title: 方块
---
graph
    id1["方块1"]
    id2["方块2"]
```



## 箭头

### 从上到下
- 默认
```mermaid
graph
    id1["id1"]
    id2["id2"]
    id1-->id2
```
**示例代码**：
```markdown
    ```mermaid
    graph
        id1["id1"]
        id2["id2"]
        id1-->id2
    ```
```

### 从上到下(TB或TD)
```mermaid
graph TB
    id1["id1"]
    id2["id2"]
    id1-->id2
```
**示例代码**：
```markdown
    ```mermaid
    graph TB
        id1["id1"]
        id2["id2"]
        id1-->id2
    ```
```

```mermaid
graph TD
    id1["id1"]
    id2["id2"]
    id1-->id2
```
**示例代码**：
```markdown
    ```mermaid
    graph TD
        id1["id1"]
        id2["id2"]
        id1-->id2
    ```
```

```mermaid
graph BT
    id1["id1"]
    id2["id2"]
    id1-->id2
```
**示例代码**：
```markdown
    ```mermaid
    graph BT
        id1["id1"]
        id2["id2"]
        id1-->id2
    ```
```

```mermaid
graph BT
    id1["id1"]
    id2["id2"]
    id2-->id1
```
**示例代码**：
```markdown
    ```mermaid
    graph BT
        id1["id1"]
        id2["id2"]
        id2-->id1
    ```
```

### 从左到右
```mermaid
graph LR
    id1["id1"]
    id2["id2"]
    id1-->id2
```
**示例代码**：
```markdown
    ```mermaid
    graph LR
        id1["id1"]
        id2["id2"]
        id1-->id2
    ```
```

### 从右到左
```mermaid
graph RL
    id1["id1"]
    id2["id2"]
    id1-->id2
```
**示例代码**：
```markdown
    ```mermaid
    graph RL
        id1["id1"]
        id2["id2"]
        id1-->id2
    ```
```

## 节点形状（Node shapes）

### 圆角形状
```mermaid
flowchart
    id1("圆角")
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1("圆角")
    ```
```

### 半圆方框
```mermaid
flowchart
    id1(["半圆方框"])
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1(["半圆方框"])
    ```
```

### 子程序形状的节点
```mermaid
flowchart
    id1[["子程序形状的节点"]]
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1[["子程序形状的节点"]]
    ```
```

### 圆柱形的节点
```mermaid
flowchart
    id1[("圆柱形的节点")]
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1[("圆柱形的节点")]
    ```
```

### 圆圈形的节点
```mermaid
flowchart
    id1(("圆圈形的节点"))
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1(("圆圈形的节点"))
    ```
```

### 不对称形状的节点
```mermaid
flowchart
    id1>"不对称形状的节点"]
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1>"不对称形状的节点"]
    ```
```

### 菱形

```mermaid
flowchart
    id1{"菱形"}
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1{"菱形"}
    ```
```

### 六边形节点
```mermaid
flowchart
    id1{{"六边形节点"}}
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1{{"六边形节点"}}
    ```
```

### 平行四边形
```mermaid
flowchart
    id1[/"平行四边形"/]
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1[/"平行四边形"/]
    ```
```

```mermaid
flowchart
    id1[\"平行四边形"\]
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1[\"平行四边形"\]
    ```
```

### 梯形
```mermaid
flowchart
    id1[/"梯形"\]
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1[/"梯形"\]
    ```
```

```mermaid
flowchart
    id1[\"梯形"/]
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1[\"梯形"/]
    ```
```

### 双圆型
```mermaid
flowchart
    id1((("双圆型")))
```
**示例代码**：
```markdown
    ```mermaid
    flowchart
        id1((("双圆型")))
    ```
```

## 线

### 箭头
```mermaid
graph LR
    A-->B
```
```markdown
    ```mermaid
    graph LR
        A-->B
    ```
```

### 连实线
```mermaid
graph LR
    A---B
```
```markdown
    ```mermaid
    graph LR
        A---B
    ```
```

### 文本连线
```mermaid
graph LR
    A-- "是" --- B

    C--- |"是"| D

    E-->|是| F
    E--是 --->F
```
```markdown
    ```mermaid
    graph LR
        A-- "是" --- B

        C--- |"是"| D

        E-->|是| F
        E--是 --->F
    ```
```
### 虚线
```mermaid
graph LR
    A-.-B
    A-.->B
    A-. "是".->B
```

```markdown
    ```mermaid
    graph LR
        A-.-B
        A-.->B
        A-. "是".->B
    ```
```
### 粗箭头
```mermaid
graph LR
    A==>B
    A== 是 ==>B
```

```markdown
    ```mermaid
    graph LR
        A==>B
        A== 是 ==>B
    ```
```
## 子图
```mermaid
graph TB
    subgraph one
    A1-->A2
    end
    subgraph two
    B1-->B2
    end
    subgraph three
    C1-->C2
    end
    A1-->B2
    C2-->B2
```

```markdown
    ```mermaid
    graph TB
        subgraph one
        A1-->A2
        end
        subgraph two
        B1-->B2
        end
        subgraph three
        C1-->C2
        end
        A1-->B2
        C2-->B2
    ```
```




# 流程图
> 关键字 flowchart，可以使用graph替换
## 示例1
```mermaid
    flowchart TD
        A-->B["过程"]
        A-->C{"条件"}
        B-->D[["子过程"]]
        D-->E[/"结果"/]--"是"-->F("结束")
        C--"是"-->D
        C--"否"-->E
```
```markdown
    ```mermaid
        flowchart TD
            A-->B["过程"]
            A-->C{"条件"}
            B-->D[["子过程"]]
            D-->E[/"结果"/]--"是"-->F("结束")
            C--"是"-->D
    ```
```

## 示例2
```mermaid
graph TD;
A-->B;
A-->C;
B-->D;
B-->E;
E--xF;
```
```markdown
    ```mermaid
    graph TD;
    A-->B;
    A-->C;
    B-->D;
    B-->E
    E-->>F
    ```
```
# 表格
| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |

```markdown
| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |
```

# 时序图
- 关键字： sequenceDiagram
- 格式：主体1 关系线 主体2: 消息 
- 关系线类型：

|类型|描述|
|:---|:---|
|->| 无箭头实线：Solid line without arrow |
|-->|无箭头虚线：Dotted line without arrow |
|->>|有箭头实线：Solid line with arrowhead |
|-->>|有箭头虚线： Dotted line with arrowhead |
|-x|以x结尾的实线：Solid line with a cross at the end|
|--x| 以x结尾的虚线：Dotted line with a cross at the end |
|-)| 末尾是开箭头异步实线：Solid line with an open arrow at the end(async)|
|--)|末尾是开箭头异步虚线：Dotted line with a open arrow at the end(async)|

## 示例1
```mermaid
    sequenceDiagram
    C--x D: ddd
    Alice->>John: Hello John, how are you?
    John-->>Alice: Great!
    Alice-)John: See you later!
```
```markdown
    ```mermaid
        sequenceDiagram
        Alice->>John: Hello John, how are you?
        John-->>Alice: Great!
    ```
```

## 示例2
```mermaid
    sequenceDiagram
        客户端->>缓存: 查缓存
        缓存-->>数据库: 查数据库
        数据库->>客户端: 返回结果
        Note right of 数据库: 你好
        
```

```markdown
    ```mermaid
        sequenceDiagram
            客户端->>缓存: 查缓存
            缓存-->>数据库: 查数据库
            数据库->>客户端: 返回结果
            Note right of 数据库: 你好
            
    ```

```


## 示例3
```mermaid
    sequenceDiagram
        A->B: 无箭头实线
        B->>C: 有箭头实线
        C-->D: 无箭头虚线
        B-->>D: 有箭头虚线
        D-xB: x结尾实线
        C--xB: x结尾虚线
        B-)A: 末尾是异步开箭头实现
        D--)A: 末尾是异步开箭头虚线
```

```markdown
    ```mermaid
        sequenceDiagram
            A->B: 无箭头实线
            B->>C: 有箭头实线
            C-->D: 无箭头虚线
            B-->>D: 有箭头虚线
            D-xB: x结尾实线
            C--xB: x结尾虚线
            B-)A: 末尾是异步开箭头实现
            D--)A: 末尾是异步开箭头虚线
            
    ```
```