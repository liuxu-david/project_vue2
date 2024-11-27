<template>
    <div>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column label="客户名称">
          <template slot-scope="{ row }">
            <span>{{ row.customerName }} - {{ row.customerName }}</span>
        </template>
        </el-table-column>
        <el-table-column
          v-for="(currency, index) in currencyList"
          :key="index"
          :label="currency"
        >
        <!-- 自定义表头 -->
        <template #header>
            <span>{{ currency }}</span>
            <el-popover
              v-model="visible[currency]"
              placement="top"
              width="160">
              <el-input type="text" v-model="batchValue"/>
              <div style="text-align: right; margin: 0">
                <el-button size="mini" type="text" @click="visible[currency] = false">取消</el-button>
                <el-button type="primary" size="mini" @click="handleBath(currency,`${currency}Used`)">确定</el-button>
              </div>
              <el-button slot="reference" size="mini">批量修改</el-button>
            </el-popover>
          </template>
        <template slot-scope="{ row }">
            <el-input v-model="row[currency + 'Used']" placeholder="请输入" size="small"></el-input>
        </template>
        </el-table-column>
      </el-table>
      <el-button @click="handleSubmit">提交</el-button>
      <el-button @click="handleChild">控制子元素</el-button>
      <children ref="children"></children>
    </div>
</template>

<script>
import children from './children.vue'
export default {
  name: 'Home',
  components: {children},
  data () {
    return {
      currencyList: ['aud', 'cad', 'cny', 'eur', 'gbp', 'hkd', 'mxn', 'usd'],
      visible: {}, // 控制每个弹窗显示隐藏
      batchValue: '0', // 批量修改的值
      tableData: [{
        aud: '',
        audUsed: '2',
        cad: '',
        cadUsed: '0',
        cny: '',
        cnyUsed: '0',
        customerCode: '1071379',
        customerName: '技术支持测试客户',
        eur: '',
        eurUsed: '0',
        gbp: '',
        gbpUsed: '0',
        hkd: '',
        hkdUsed: '0',
        mxn: '',
        mxnUsed: '0',
        usd: '',
        usdUsed: '0'
      },
      {
        aud: '',
        audUsed: '0',
        cad: '',
        cadUsed: '0',
        cny: '',
        cnyUsed: '0',
        customerCode: '99999',
        customerName: '客户2',
        eur: '',
        eurUsed: '0',
        gbp: '',
        gbpUsed: '0',
        hkd: '',
        hkdUsed: '0',
        mxn: '',
        mxnUsed: '0',
        usd: '',
        usdUsed: '0'
      }]
    }
  },
  methods: {
    handleEdit (index, row) {
      console.log(index, row)
    },
    handleDelete (index, row) {
      console.log(index, row)
    },
    handleBath (flag, val) {
      this.tableData.forEach(item => {
        item[val] = this.batchValue
      })
      this.batchValue = ''
      this.visible[flag] = false
    },
    handleSubmit () {
      console.log(this.tableData)
    },
    handleChild () {
      this.$refs.children.handleData()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
