# Form表单学习

### 1. 基础用法

在 Vue 中，可以使用原生的 HTML 表单元素，或者使用 UI 框架的表单组件。例如：

**原生表单**：

```markdown
<template>
  <form @submit.prevent="handleSubmit">
    <label for="name">姓名:</label>
    <input type="text" v-model="name" id="name" required />
    <button type="submit">提交</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: ''
    };
  },
  methods: {
    handleSubmit() {
      alert(`提交的姓名是: ${this.name}`);
    }
  }
}
</script>
```

效果图：

![image-20241010090123972](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/form1.png)

**使用 Element Plus 的表单**：

```markdown
<template>
  <el-form @submit.prevent="handleSubmit">
    <el-form-item label="姓名" required>
      <el-input v-model="name"></el-input>
    </el-form-item>
    <el-button type="primary" native-type="submit">提交</el-button>
  </el-form>
</template>

<script>
import { ElForm, ElFormItem, ElInput, ElButton } from 'element-plus';

export default {
  components: {
    ElForm,
    ElFormItem,
    ElInput,
    ElButton
  },
  data() {
    return {
      name: ''
    };
  },
  methods: {
    handleSubmit() {
      alert(`提交的姓名是: ${this.name}`);
    }
  }
}
</script>
```

效果如上

### 2. 验证

表单验证通常使用 `v-model` 和条件语句来确保输入合法。

**原生表单验证**：

```markdown
<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" v-model="name" required />
    <span v-if="!name">姓名是必填项</span>
    <button type="submit">提交</button>
  </form>
</template>
```

**Element Plus 表单验证**：

```markdown
<template>
  <el-form :model="form" :rules="rules" ref="formRef">
    <el-form-item label="姓名" prop="name">
      <el-input v-model="form.name"></el-input>
    </el-form-item>
    <el-button type="primary" @click="submitForm">提交</el-button>
  </el-form>
</template>

<script>
import { ElForm, ElFormItem, ElInput, ElButton } from 'element-plus';

export default {
  components: {
    ElForm,
    ElFormItem,
    ElInput,
    ElButton
  },
  data() {
    return {
      form: {
        name: ''
      },
      rules: {
        name: [
          { required: true, message: '姓名是必填项', trigger: 'blur' }
        ]
      }
    };
  },
  methods: {
    submitForm() {
      this.$refs.formRef.validate((valid) => {
        if (valid) {
          alert(`提交的姓名是: ${this.form.name}`);
        } else {
          console.log('验证失败');
        }
      });
    }
  }
}
</script>
```

效果图：

![image-20241010090422144](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/form2.png)

### 3. 样式

可以通过 CSS 和 UI 框架的样式类自定义表单的外观。

**原生表单样式**：

```markdown
<style>
form {
  display: flex;
  flex-direction: column;
}

input {
  margin-bottom: 10px;
}
</style>
```

**Element Plus 样式**：

```markdown
<template>
  <el-form :model="form" label-width="100px">
    <el-form-item label="姓名">
      <el-input v-model="form.name"></el-input>
    </el-form-item>
  </el-form>
</template>
```

### 4. 事件处理

表单的事件处理主要通过 `@submit` 或 `@input` 来实现：

**原生表单事件处理**：

```markdown
<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" v-model="name" @input="handleInput" />
    <button type="submit">提交</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: ''
    };
  },
  methods: {
    handleInput() {
      console.log('输入的姓名是:', this.name);
    },
    handleSubmit() {
      alert(`提交的姓名是: ${this.name}`);
    }
  }
}
</script>
```

**Element Plus 事件处理**：

```markdown
<template>
  <el-form @submit.native.prevent="handleSubmit">
    <el-form-item>
      <el-input v-model="form.name" @input="handleInput"></el-input>
    </el-form-item>
    <el-button type="primary" native-type="submit">提交</el-button>
  </el-form>
</template>
```

效果图：

![image-20241010090605437](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/form3.png)

### 5. 组合与嵌套

你还可以组合不同的表单组件，创建复杂的表单结构。

**组合示例**：

```markdown
<template>
    <el-form :model="form" ref="formRef" label-width="100px">
      <el-form-item label="姓名" prop="name">
        <el-input v-model="form.name" placeholder="请输入姓名"></el-input>
      </el-form-item>
      <el-form-item label="年龄" prop="age">
        <el-input type="number" v-model="form.age" placeholder="请输入年龄"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm">提交</el-button>
      </el-form-item>
    </el-form>
  </template>
  
  <script>
  import { ElForm, ElFormItem, ElInput, ElButton } from 'element-plus';
  
  export default {
    components: {
      ElForm,
      ElFormItem,
      ElInput,
      ElButton
    },
    data() {
      return {
        form: {
          name: '',
          age: null
        }
      };
    },
    methods: {
      submitForm() {
        console.log(this.form);
      }
    }
  }
  </script>
```

效果如图：

![image-20241010091218485](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/form4.png)