# button组件学习

### 1. 基础用法

在 Vue 中，你可以使用原生的 HTML 按钮元素，也可以使用 UI 框架（如 Element Plus、Vuetify 等）提供的按钮组件。例如：

**原生按钮**：

```markdown
<template>
  <button @click="handleClick">点击我</button>
</template>

<script>
export default {
  methods: {
    handleClick() {
      alert('按钮被点击了！');
    }
  }
}
</script>
```

效果图：

![image-20241010082956790](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/button1.png)

**使用 Element Plus**：

```markdown
<template>
  <el-button @click="handleClick">点击我</el-button>
</template>

<script>
import { ElButton } from 'element-plus';

export default {
  components: {
    ElButton
  },
  methods: {
    handleClick() {
      alert('按钮被点击了！');
    }
  }
}
</script>
```

效果如上



### 2. 样式

你可以通过 CSS 为按钮添加样式，例如：

```
<template>
  <button class="my-button" @click="handleClick">点击我</button>
</template>

<style>
.my-button {
  background-color: blue;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
}
</style>
```

### 3. 事件处理

按钮的事件处理主要通过 `@click` 指令来实现：

```markdown
<template>
  <button @click="handleClick">点击我</button>
</template>

<script>
export default {
  methods: {
    handleClick() {
      console.log('按钮被点击了！');
    }
  }
}
</script>
```

效果图：

![image-20241010083457567](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/button2.png)

### 4. 状态管理

你可以通过绑定 `disabled` 属性来控制按钮的可用状态：

```markdown
<template>
  <button :disabled="isDisabled" @click="handleClick">点击我</button>
</template>

<script>
export default {
  data() {
    return {
      isDisabled: true
    };
  },
  methods: {
    handleClick() {
      console.log('按钮被点击了！');
    }
  }
}
</script>
```

### 5. 插槽

如果使用 UI 框架，通常可以通过插槽来插入自定义内容：

```markdown
<template>
  <el-button @click="handleClick">
    <i class="el-icon-search"></i> 搜索
  </el-button>
</template>

<script>
import { ElButton } from 'element-plus';

export default {
  components: {
    ElButton
  },
  methods: {
    handleClick() {
      console.log('搜索按钮被点击了！');
    }
  }
}
</script>
```

效果图：

![image-20241010083705357](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/button3.png)