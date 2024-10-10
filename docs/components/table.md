# Table表格学习

在 Vue 中，表格组件非常常见，用于显示结构化的数据。可以使用原生的 HTML 表格，也可以使用 UI 库（如 Element Plus、Vuetify）提供的表格组件。下面我们详细学习表格的各个方面，包括基础用法、数据绑定、排序、分页、样式自定义等。

### 1. **基础用法**

#### 使用原生 HTML 表格

你可以使用标准的 HTML 标签创建简单的表格：

```markdown
<template>
  <table border="1">
    <thead>
      <tr>
        <th>姓名</th>
        <th>年龄</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(user, index) in users" :key="index">
        <td>{{ user.name }}</td>
        <td>{{ user.age }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  data() {
    return {
      users: [
        { name: 'Alice', age: 25 },
        { name: 'Bob', age: 30 }
      ]
    };
  }
}
</script>
```

#### 使用 Element Plus 表格组件

使用像 Element Plus 这样的 UI 库时，可以使用更加复杂和功能丰富的表格组件：

```markdown
<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="name" label="姓名" width="180"></el-table-column>
    <el-table-column prop="age" label="年龄" width="180"></el-table-column>
  </el-table>
</template>

<script>
import { ElTable, ElTableColumn } from 'element-plus';

export default {
  components: {
    ElTable,
    ElTableColumn
  },
  data() {
    return {
      tableData: [
        { name: 'Alice', age: 25 },
        { name: 'Bob', age: 30 }
      ]
    };
  }
}
</script>
```

效果图：

![image-20241010092520776](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/table1.png)

### 2. **数据绑定**

在 Vue 中，表格的数据通常通过 `data` 绑定到表格组件，动态生成表格行。这里通过 `v-for` 循环或使用 UI 库的 `:data` 属性来实现。

#### 示例：

```markdown
<template>
  <el-table :data="tableData">
    <el-table-column prop="name" label="姓名"></el-table-column>
    <el-table-column prop="age" label="年龄"></el-table-column>
  </el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { name: 'John', age: 28 },
        { name: 'Doe', age: 22 }
      ]
    };
  }
}
</script>
```

### 3. **排序**

Element Plus 中可以非常方便地添加表格排序功能，只需要在 `el-table-column` 中添加 `sortable` 属性：

```markdown
<template>
  <el-table :data="tableData">
    <el-table-column prop="name" label="姓名" sortable></el-table-column>
    <el-table-column prop="age" label="年龄" sortable></el-table-column>
  </el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { name: 'John', age: 28 },
        { name: 'Doe', age: 22 }
      ]
    };
  }
}
</script>
```

效果图：

![image-20241010093656406](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/table2.png)

### 4. **分页**

当数据量较大时，通常需要对表格进行分页显示。在 Element Plus 中，可以使用 `el-pagination` 组件与表格组合使用：

```markdown
<template>
  <div>
    <el-table :data="currentPageData" style="width: 100%">
      <el-table-column prop="name" label="姓名"></el-table-column>
      <el-table-column prop="age" label="年龄"></el-table-column>
    </el-table>

    <el-pagination
      background
      layout="prev, pager, next"
      :total="tableData.length"
      :page-size="pageSize"
      @current-change="handlePageChange">
    </el-pagination>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { name: 'Alice', age: 25 },
        { name: 'Bob', age: 30 },
        { name: 'Charlie', age: 35 },
        { name: 'David', age: 40 },
        // 更多数据
      ],
      pageSize: 2,
      currentPage: 1
    };
  },
  computed: {
    currentPageData() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = this.currentPage * this.pageSize;
      return this.tableData.slice(start, end);
    }
  },
  methods: {
    handlePageChange(page) {
      this.currentPage = page;
    }
  }
}
</script>
```

效果图：

![image-20241010093911937](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/table3.png)

### 5. **选择行**

可以在表格中添加选择框，允许用户选择一行或多行数据：

```markdown
<template>
  <el-table :data="tableData" @selection-change="handleSelectionChange">
    <el-table-column type="selection" width="55"></el-table-column>
    <el-table-column prop="name" label="姓名"></el-table-column>
    <el-table-column prop="age" label="年龄"></el-table-column>
  </el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { name: 'Alice', age: 25 },
        { name: 'Bob', age: 30 }
      ],
      selectedRows: []
    };
  },
  methods: {
    handleSelectionChange(selectedRows) {
      this.selectedRows = selectedRows;
    }
  }
}
</script>
```

效果图：

![image-20241010094033867](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/table4.png)

### 6. **自定义样式**

可以通过内联样式或外部样式表自定义表格的样式。在 Element Plus 中，也可以通过 `class-name` 属性为特定的列或行添加自定义样式。

```markdown
<template>
  <el-table :data="tableData" row-class-name="custom-row">
    <el-table-column prop="name" label="姓名"></el-table-column>
    <el-table-column prop="age" label="年龄"></el-table-column>
  </el-table>
</template>

<style>
.custom-row {
  background-color: #f5f5f5;
}
</style>
```

### 7. **合并单元格**

表格还可以合并单元格，比如在显示报表时：

```markdown
<template>
  <el-table :data="tableData" :span-method="mergeCells">
    <el-table-column prop="name" label="姓名"></el-table-column>
    <el-table-column prop="age" label="年龄"></el-table-column>
  </el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { name: 'Alice', age: 25 },
        { name: 'Alice', age: 30 }
      ]
    };
  },
  methods: {
    mergeCells({ row, column, rowIndex, columnIndex }) {
      if (rowIndex === 0 && columnIndex === 0) {
        return [2, 1]; // 合并两行一列
      }
    }
  }
}
</script>
```

效果图：

![image-20241010094228645](https://my-wxy-bucket.oss-cn-nanjing.aliyuncs.com/images/table5.png)