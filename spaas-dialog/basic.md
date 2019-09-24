基本用法, 内容区域默认是 100%, 如果想要居中效果，必须指定 contentWidth 的宽度

```vue
<template>
  <div class="test-page">
    <spaas-dialog
      :visible.sync="visible"
      title="测试dialog"
      @comfirm="handleComfirm"
      contentWidth="600px"
      :confirm="confirm"
      :before-close="handleBeforeClose"
    >
      ddd
    </spaas-dialog>
    <el-button @click="visible = !visible">改变窗口状态</el-button>
  </div>
</template>

<script>

export default {
  data() {
    return {
      visible: false,
      content: [
        {
          $type: 'input', // 类型，element-ui 提供的所有表单类型，即 el-xxx
          $id: 'name', // 每一个原子都存在id，用于存储该原子的值，注意不能重复
          label: '活动名称',
          attrs: {'data-name': 'form1'}, // 可选, 写法与 Vue 的 Render 函数规范保持一致
          el: {
            size: 'mini',
            placeholder: 'test placeholder'
          },
          rules: [
            {required: true, message: '请输入活动名称', trigger: 'blur'},
            {min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur'}
          ]
        },
        {
          $type: 'select',
          $id: 'region',
          label: '活动区域',
          // options 具有选择功能的原子表单可用此定义可选项，例如: select, radio-group, radio-button, checkbox-group, checkbox-button
          options: [
            {
              label: '区域一',
              value: 'shanghai'
            },
            {
              label: '区域二',
              value: 'beijing'
            }
          ],
          rules: [
            {required: true, message: '请选择活动区域', trigger: 'change'}
          ]
        },
        {
          $type: 'date-picker',
          $id: 'date',
          label: '活动时间',
          el: {
            type: 'datetime',
            placeholder: '请选择'
          },
          rules: [
            {
              type: 'date',
              required: true,
              message: '请选择日期时间',
              trigger: 'change'
            }
          ]
        },
        {
          $type: 'switch',
          $id: 'delivery',
          label: '即时配送'
        },
        {
          // 增加的 enableWhen 示例, 与 element-ui 无关
          $type: 'input',
          $id: 'enableWhenDelivery',
          el: {
            placeholder: '如果你选择即时配送就看到我啦'
          },
          label: '隐藏项demo',
          enableWhen: {delivery: true} // 可选属性，表示当 delivery 的值为 true 时显示
        },
        {
          $type: 'checkbox-group',
          $id: 'type',
          label: '活动性质',
          default: [],
          options: [
            {
              label: '美食/餐厅线上活动'
            },
            {
              label: '地推活动'
            },
            {
              label: '线下主题活动'
            },
            {
              label: '单纯品牌曝光'
            }
          ],
          rules: [
            {
              type: 'array',
              required: true,
              message: '请至少选择一个活动性质',
              trigger: 'change'
            }
          ]
        },
        {
          $type: 'radio-group',
          $id: 'resource',
          label: '特殊资源',
          options: [
            {
              label: '线上品牌商赞助'
            },
            {
              label: '线下场地免费'
            }
          ],
          rules: [
            {required: true, message: '请选择活动资源', trigger: 'change'}
          ]
        },
        {
          $type: 'input',
          $id: 'desc',
          label: '活动形式',
          el: {
            type: 'textarea'
          },
          rules: [{required: true, message: '请填写活动形式', trigger: 'blur'}]
        }
      ],
    }
  },
  methods: {
    handleComfirm() {
      this.visible = false
    },
    confirm() {
      return new Promise((resolve) => {
        // this.visible = false
        setTimeout(() => resolve(), 2000)
      })
    },
    handleBeforeClose() {
      /** return new Promise((resolve) => {
        setTimeout(() => {
          resolve(false)
          console.log('返回 false 不关闭窗口')
        }, 2000)
      }) */
      return true
    }
  }
  
}
</script>
```