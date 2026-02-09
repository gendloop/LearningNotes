## STL

### Containers

### Algorithms

```cpp
#include <algorithm>
#include <numeric>
```

#### std::accumulate

```cpp
// 计算容器元素和, 初始值为 0
int sum = std::accumulate(nums.begin(), nums.end(), 0);
// 自定义二元操作(字符串拼接)
std::string sentence = std::accumulate(words.begin(), words.end(),
    std::string(""),
    [](std::string acc, const std::string& wokd) {
        return acc + " " + word;
    }
);
```

#### std::transform

#### std::partition

#### std::unique

#### std::advance

### Iterators

### Functors

### Adapters

### References
