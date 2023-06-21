<template>
  <div class="box">
    <div class="box-item">
      <!-- 背景 -->
      <div class="img">

        <!-- 头部 -->
        <div class="top">
          <div>自助收银</div>
          <div class="avatar">
            <img src="../assets/03.png" alt="Avatar">
          </div>
          <div>商家名称</div>
        </div>

        <!-- 卡片区域 -->
        <div class="card">
          <!-- 第一卡 -->
          <div class="card1">
            <div>支付金额</div>
            <input class="card1-inp" v-model="pry" :class="pry ? 'wei-red-pry' : ''">
            <div>添加备注</div>
          </div>

          <div class="card-small" @click="addYouHui">
            <div class="card2-left">
              <img src="../assets/icon/优惠券.png" class="youhui-icon" style="padding-right: 10px;">
              <div class="small-text">优惠券</div>
            </div>
            <div class="card2-right">
              <text>图标</text>
              <img src="../assets//icon//right.png" class="right-icon">
            </div>
          </div>

          <div class="card-small">
            <div class="small-text">
              <img src="../assets/icon/积分.png" class="jifen-icon" style="padding-right: 10px;">
              积分
            </div>
            <el-switch v-model="value" active-color="#13ce66" inactive-color="#000" :width='50' class="el-sw">
            </el-switch>
          </div>

          <div class="card-small">
            <div class="small-text">实付金额</div>
            <div class="red-pry" :class="pry ? 'wei-red-pry' : ''">{{ pry }}</div>
          </div>
        </div>


        <!-- 键盘 -->
        <Keyboard @keyboardClickNumber="keyboardClickNumber" @keyboardDelete="keyboardDelete"
          @keyboardSubmit="keyboardSubmit" class="Keyboard"></Keyboard>

      </div>

      <Popup ref="popup"></Popup>

    </div>

  </div>
</template>

<script>
import Popup from './popup/index.vue'
import Keyboard from './keyboard/index.vue'
export default {
  name: 'HelloWorld',
  components: {
    Keyboard,
    Popup
  },
  data() {
    return {
      pry: '',
      value: false
    }
  },
  watch: {
    pry() {
      const regex = /(^[1-9]([0-9]+)?(\.[0-9]{0,2})?$)|(^(0){1}$)|(^[0-9]+(\.[0-9]{0,2})?$)/;
      if (!regex.test(this.pry)) {
        this.pry = this.pry.slice(0, -1)
      }
    }
  },
  methods: {
    keyboardClickNumber(singlePry) {
      this.pry = this.pry + singlePry
    },
    // 删除
    keyboardDelete() {
      this.pry = this.pry.slice(0, -1)
    },
    // 付款
    keyboardSubmit() {
      if (this.pry[this.pry.length - 1] == '.') {
        alert('请输入正确的金额')
        return
      }
      alert('付款')
      this.pry = ''
    },
    // 点击优惠券
    addYouHui() {
      this.$nextTick(() => {
        this.$refs.popup.alterDrawer()
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input:focus {
  outline: none;
}

.box {
  width: 100%;
  display: flex;
  justify-content: center;

  .box-item {
    width: 750px;
    height: 1604px;
    background-color: #F4F4F4;
    position: relative;

    .top {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      >div {
        &:nth-child(1) {
          font-size: 34px;
          margin: 20px 0 20px 0;
        }

        &:nth-child(3) {
          font-size: 42px;
          margin-bottom: 20px;
        }
      }

      // 头像
      .avatar {
        width: 141px;
        height: 141px;
        border-radius: 16px;
        overflow: hidden;
        /* 裁剪超出框的内容 */
        border: 1px solid #000;
        /* 设置边框样式和颜色 */
        margin: 20px 0 20px 0;

      }

    }

    // 卡片区域
    .card {
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;


      .card1 {
        width: 710px;
        height: 314px;
        background-color: #fff;
        border-radius: 16px;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        box-sizing: border-box;
        padding-left: 40px;

        .card1-inp {
          height: 65px;
          border-bottom: 1px solid #F7F7F7;
          font-size: 80.1px;
        }

        >div {
          &:nth-child(1) {
            font-size: 36px;
            font-weight: 500;
          }

          &:nth-child(3) {
            font-size: 28px;
            color: #9F9F9F;
          }
        }
      }

      .card-small {
        width: 710px;
        height: 108px;
        background-color: #fff;
        border-radius: 16px;
        margin-top: 10px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        box-sizing: border-box;
        padding-left: 40px;
        padding-right: 40px;
        margin-top: 20px;

        >div {
          &:nth-child(1) {
            display: flex;

            >div {
              &:nth-child(2) {
                font-size: 28px;
              }
            }
          }
        }
      }
    }
  }
}

.small-text {
  font-size: 28px;
  font-weight: 500;
}

// 背景图
.img {
  width: 750px;
  height: 481px;
  background-image: url("../assets/01.png");
  background-size: cover;
}

.red-pry {
  color: red;
  font-size: 30px;
}

.wei-red-pry {
  &::before {
    content: "￥";

  }
}

.youhui-icon {
  width: 43px;
  height: 37px;
}

.Keyboard {
  position: absolute;
  bottom: 0;
}

.el-sw {
  height: 50px;
}

.jifen-icon {
  width: 40px;
  height: 40px;
}

.right-icon {
  width: 30px;
  height: 39px;
}

input {
  border: 0;
  /*清除自带的2px的边框*/
  padding: 0;
  /*清除自带的padding间距*/
}

// ::v-deep {
//   .el-switch {
//     .el-switch__core {
//       height: 30px;

//       &::after {
//         width: 28px;
//         height: 28px;
//       }
//     }
//   }

// }
</style>
