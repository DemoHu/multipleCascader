<template>
  <div class="multiple_cascader">
    <div class="cascader cascader_1">
      <div slot="header" class="clearfix">
        <span>支付方式(单选)</span>
      </div>
      <div v-for="(item,index) in data" :key="index" @click="selectItemFun1(item)" @mouseover="hoverItemOne(item.value,item.children)" @mouseout="outHoverItemOne1" class="text item">
        <div>{{item.label}}</div>
        <i class="el-icon-check" v-show="selectItem1.value === item.value"></i>
      </div>
    </div>
    <div class="cascader cascader_1" v-show="hoverItem1 && noHover1">
      <div slot="header" class="clearfix">
        <span>充值通道(单选)</span>
      </div>
      <div v-for="(item,index) in hoverItem1Children" :key="index" @click="selectItemFun2(item)" @mouseover="hoverItemOne2(item.value,item.children)" @mouseout="outHoverItemOne2" class="text item">
        <div>{{item.label}}</div>
        <i class="el-icon-check" v-show="selectItem2.value === item.value"></i>
      </div>
    </div>
    <div class="cascader cascader_1" v-show="hoverItem2 && noHover2">
      <div slot="header" class="clearfix">
        <span>充值通道商户</span>
        <el-button style="float: right; padding: 3px 0" type="text" @click="allSelect()">全选</el-button>
      </div>
      <div v-for="(item,index) in hoverItem2Children" :key="index" @click="selectItemFun3(item, item.value)"  class="text item">
        <div>{{item.label}}</div>
        <i class="el-icon-check" v-show="selectItem3Arr.includes(item.value)"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MultipleCascader',
  data() {
    return {
      hoverItem1: '',
      noHover1: false,
      selectItem1: '',
      hoverItem1Children: [],
      hoverItem2: '',
      noHover2: false,
      selectItem2: '',
      hoverItem2Children: [],
      selectItem3: '',
      selectItem3Arr: [],
      data: [
        {
          label: '微信扫码',
          value: '1',
          children: [
            { label: '微信扫码1', value: '1-1',
              children: [
                { label: '微信扫码1-1-1', value: '1-1-1' },
                { label: '微信扫码1-1-2', value: '1-1-2' },
                { label: '微信扫码1-1-3', value: '1-1-3' }
              ]
            },
            { label: '微信扫码2', value: '1-2',
              children: [
                { label: '微信扫码1-2-1', value: '1-2-1' },
                { label: '微信扫码1-2-2', value: '1-2-2' },
                { label: '微信扫码1-2-3', value: '1-2-3' }
              ]
            },
            { label: '微信扫码3', value: '1-3',
              children: [
                { label: '微信扫码1-3-1', value: '1-3-1' },
                { label: '微信扫码1-3-2', value: '1-3-2' },
                { label: '微信扫码1-3-3', value: '1-3-3' }
              ]
            }
          ]
        },
        {
          label: '支付宝扫码',
          value: '2',
          children: [
            { label: '支付宝扫码1', value: '2-1',
              children: [
                { label: '支付宝扫码2-1-1', value: '2-1-1' },
                { label: '支付宝扫码2-1-2', value: '2-1-2' },
                { label: '支付宝扫码2-1-3', value: '2-1-3' }
              ]
            },
            { label: '支付宝扫码2', value: '2-2',
              children: [
                { label: '支付宝扫码2-2-1', value: '2-2-1' },
                { label: '支付宝扫码2-2-2', value: '2-2-2' },
                { label: '支付宝扫码2-2-3', value: '2-2-3' }
              ]
            },
            { label: '支付宝扫码3', value: '2-3',
              children: [
                { label: '支付宝扫码2-3-1', value: '2-3-1' },
                { label: '支付宝扫码2-3-2', value: '2-3-2' },
                { label: '支付宝扫码2-3-3', value: '2-3-3' }
              ]
            }
          ]
        },
        {
          label: '银行扫码',
          value: '3',
          children: [
            { label: '银行扫码1', value: '3-1',
              children: [
                { label: '银行扫码3-1-1', value: '3-1-1' },
                { label: '银行扫码3-1-2', value: '3-1-2' },
                { label: '银行扫码3-1-3', value: '3-1-3' }
              ]
            },
            { label: '银行扫码2', value: '3-2',
              children: [
                { label: '银行扫码3-2-1', value: '3-2-1' },
                { label: '银行扫码3-2-2', value: '3-2-2' },
                { label: '银行扫码3-2-3', value: '3-2-3' }
              ]
            },
            { label: '银行扫码3', value: '3-3',
              children: [
                { label: '银行扫码3-3-1', value: '3-3-1' },
                { label: '银行扫码3-3-2', value: '3-3-2' },
                { label: '银行扫码3-3-3', value: '3-3-3' }
              ]
            }
          ]
        }
      ]
    }
  },
  created() {},
  methods: {
    /**第一级hover */
    hoverItemOne(value, children) {
      this.hoverItem1 = value
      this.hoverItem1Children = children
      this.noHover1 = true
      this.noHover2 = false
    },
    outHoverItemOne1() {
      this.noHover1 = false
    },
    /**选择第一级 */
    selectItemFun1(item) {
      this.selectItem1 = item
      this.selectItem2 = ''
    },
    /**第二级hover */
    hoverItemOne2(value, children) {
      this.hoverItem2 = value
      this.hoverItem2Children = children
      this.noHover1 = true
      this.noHover2 = true
    },
    outHoverItemOne2() {
      // this.noHover1 = true
    },
    /**选择第二级 */
    selectItemFun2(item) {
      this.selectItem2 = item
      this.selectItem3 = ''
      this.selectItem3Arr = []
      this.selectParent1(item)
    },
    /**选择第三级 */
    selectItemFun3(item, value) {
      this.selectItem3 = item
      if (this.selectItem3Arr.includes(value)) {
        this.selectItem3Arr.splice(this.selectItem3Arr.findIndex(item => item === value), 1)
      }else {
        this.selectItem3Arr = [...this.selectItem3Arr,value]
      }
      this.selectParent2(item)
    },
    /**全选第三级 */
    allSelect() {
      this.selectItem3Arr = []
      this.hoverItem2Children.forEach(item => {
        this.selectItemFun3(item, item.value)
      })
    },
    /**反选一级 */
    selectParent1(item) {
      this.data.forEach(v => {
        v.children.forEach( cv => {
          if (item.value == cv.value) {
            this.selectItem1 = v
          }
        })
      })
    },
    /**反选二级 */
    selectParent2(item) {
      this.data.forEach(v => {
        v.children.forEach( cv => {
          cv.children.forEach(ccv => {
            if (item.value == ccv.value) {
              this.selectItem2 = cv
              this.selectParent1(this.selectItem2)
            }
          })
        })
      })
    },
  }
}
</script>
<style lang='scss'>
.multiple_cascader {
  display: flex;
  align-items: center;
  .cascader_1 {
    width: 200px;
  }
  .cascader {
    .el-card__header {
      padding: 6px 20px;
    }
    .el-card__body {
      padding: 20px 0;
    }
    .item {
      cursor: pointer;
      padding: 9px 20px;
      font-size: 14px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .item:hover {
      background-color: #F2F6FC;
    }
  }
}
</style>
