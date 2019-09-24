confirmDisabled 场景

```vue
<template>
  <div class="table-page">
    <spaas-dialog
      :visible.sync="visible"
      title="tableDialog"
      :confirmDisabled="disableFn"
    >
      <el-button @click="btnDisabled = !btnDisabled">改变 confirm 的启用状态</el-button>
      <span>现在 disabled 状态为 {{btnDisabled}}</span>
    </spaas-dialog>
    <el-button @click="visible = !visible">改变窗口状态</el-button>
  </div>
</template>

<script>

export default {
  data() {
    return {
      visible: false,
      btnDisabled: false,
      disableFn: () => this.btnDisabled
    }
  },
  methods: {
    comfirmFn() {
      return new Promise((resolve) => {
        // this.visible = false
        setTimeout(() => resolve(true), 2000)
      })
    }
  }
  
}
</script>
```