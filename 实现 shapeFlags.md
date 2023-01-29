在 patch 过程中，会遇到元素、组件、文本 children、数组 children 等各种判断，使用枚举标记方便一点，但使用某个值不够高效，而且判断之间互相组合，所以使用位运算代替

[[ShapFlags#实现 ShapFlags]]
[[createVnode#实现 shapFlags]]
[[getShapFlag#实现 shapFlags]]
[[patch#实现 shapFlags]]
[[mountElement#实现 shapFlags]]