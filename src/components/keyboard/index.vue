
<!--
 * @SendWord:该组件向外传的参数
 * @keyboardSubmit  点击付款触发
 * @keyboardDelete  点击删除
 * @keyboardClickNumber 数字每改变一次 就会把新数组作为参数传递出去
 *
-->

<template>
  <!-- 键盘 -->
  <div class="Keyboard" @click="addKeyboard">
    <div>
      <div v-for="(item, index) in Keyboard1" :key="index" class="item">{{ item }}</div>
    </div>

    <div>
      <!-- <div v-for="(item, index) in Keyboard2" :key="index" class="item">{{ item }}</div> -->
      <div class="item" @click="addICON">
        <img src="../../assets/icon/KeyboardDeleteOutlined.png" class="item-img">
      </div>
      <div class="item" :class="pry ? 'action-pry' : ''">付款</div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      Keyboard1: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '.',],
      Keyboard2: ['删除', '付款'],
      pry: '',
    }
  },
  watch: {
    // pry() {
    //   const regex = /(^[1-9]([0-9]+)?(\.[0-9]{1,2})?$)|(^(0){1}$)|(^[0-9]\.[0-9]([0-9])?$)/;
    //   if (!regex.test(temporarilyPry)) {
    //     this.pry = this.pry.slice(0, -1);
    //   } else {
    //     // 返回数字
    //   }
    // }
  },
  methods: {
    // 点击删除
    addICON() {
      this.pry = this.pry.slice(0, -1)
      this.$emit('keyboardDelete')
    },
    addKeyboard(e) {
      if (e.target.classList.contains('item')) {  // 如果点击的是clss为item的元素
        let keyboardText = e.target.textContent
        if (keyboardText == '付款') {
          this.pry = ''
          this.$emit('keyboardSubmit')
          return
        }
        console.log(e.target);
        this.pry = this.pry + keyboardText
        this.$emit('keyboardClickNumber', keyboardText)
        // return

      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.action-pry {
  background-color: #05C160 !important;

}

// 键盘
.Keyboard {
  display: flex;
  box-sizing: border-box;
  // border-top: 1px solid #CFCFCF;
  // border-left: 1px solid #CFCFCF;

  >div {
    &:nth-child(1) {
      display: flex;
      flex-wrap: wrap;
      width: 558px;
      height: 456px;
      box-sizing: border-box;

      .item {
        width: 186px;
        height: 114px;
        background-color: #fff;
        display: flex;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        border-right: 1px solid #CFCFCF;
        border-bottom: 1px solid #CFCFCF;
        font-size: 48px;


        &:nth-child(10) {
          width: 372px;

        }
      }
    }

    &:nth-child(2) {
      width: 191px;
      height: 456px;
      display: flex;
      flex-direction: column;
      box-sizing: border-box;

      .item {
        width: 191px;
        height: 114px;
        background-color: #fff;
        display: flex;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        border-right: 1px solid #CFCFCF;
        border-bottom: 1px solid #CFCFCF;

        .item-img {
          width: 62px;
          height: 60px;
        }

        &:nth-child(2) {
          height: 342px;
          background-color: #67e7a5;
          font-size: 36px;
          color: #fff;
        }
      }
    }
  }
}
</style>
