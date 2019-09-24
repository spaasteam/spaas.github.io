内嵌 el-data-table 场景
```vue
<template>
  <div class="table-page">
    <spaas-dialog
      :visible.sync="visible"
      title="tableDialog"
      :hasFooter="false"
    >
      <el-data-table v-bind="tableConfig"></el-data-table>
    </spaas-dialog>
    <el-button @click="visible = !visible">改变窗口状态</el-button>
  </div>
</template>

<script>

export default {
  data() {
    return {
      visible: false,
      tableConfig: {
        url:
          'http://39.98.50.163:3000/mock/985/xpaas-commodity-center/api/v1/commodity/backCategorys/1/propertys',
        dataPath: 'payload',
        hasEdit: false,
        hasNew: false,
        hasDelete: false,
        // tableAttrs: {
        //   height: '390px'
        // },
        searchForm: [
          {
            $type: 'input',
            $id: 'text',
            $el: {
              size: 'small'
            }
          }
        ],
        columns: [
          {
            label: '属性名称',
            prop: 'propertyName'
          },
          {
            label: '属性值',
            prop: 'propertyValue'
          }
        ],
        extraButtons: [
          {
            type: 'text',
            text: '属性关联'
          }
        ]
      }
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