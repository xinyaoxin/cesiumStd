<template>
  <div>
    <div class="wrap">
      <div class="left">
        运算方法:
        <ul>
          <li @click="addition">+</li>
          <li @click="subtraction">-</li>
          <li @click="multiplication">*</li>
          <li @click="division">/</li>
        </ul>
      </div>
      <div class="middle">
        运算展示
        <div>
          <ul class="paramsLeft">
            参数：
            <li v-for="item in calcuNum" :key="item" @click="delNum(item)">
              {{ item.num }}
            </li>
            <div>
              运算过程：
              <p>{{ resStr }}</p>
            </div>
          </ul>
        </div>
      </div>
      <div class="right">
        <ul>
          数据
          <li v-for="item in getDta" :key="item.id" @click="addNum(item)">
            {{ item.num }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, reactive } from "vue";

export default {
  setup() {
    const resStr = ref("");
    const res = ref([]);
    const arr = [1, 2, 3, 45, 5];
    const calcuNum = ref([]);
    const getDta = ref([
      {
        id: 0,
        num: 99,
      },
      {
        id: 1,
        num: 88,
      },
      {
        id: 2,
        num: 92,
      },
      {
        id: 3,
        num: 83,
      },
      {
        id: 4,
        num: 99,
      },
      {
        id: 5,
        num: 88,
      },
    ]);
    return {
      calcuNum,
      getDta,
      arr,
      res,
      resStr,
    };
  },
  methods: {
    addNum($event) {
      const num = $event;
      this.calcuNum.push(num);
      console.log(11, this.calcuNum);
    },
    delNum($event) {
      const delNumId = $event.id;
      this.calcuNum = this.calcuNum.filter((item) => item.id != delNumId);
      console.log(this.calcuNum);
    },
    addition() {
      for (let ch of this.calcuNum) {
        this.res.push(ch.num);
      }
      this.calcuNum = [];

      this.resStr = this.res.join("+");
      this.resStr.splice(0, 0, "(");

      //   this.res.push(")");
      //   this.res.unshift("(");
      //   console.log(this.resStr);
    },
    subtraction() {},
    multiplication() {},
    division() {},
  },
};
</script>
<style scoped>
.wrap {
  display: flex;
  justify-content: space-around;
}
.left {
  width: 90px;
  height: 200px;
  border: 1px solid;
}
.middle {
  width: 500px;
  height: 200px;
  border: 1px solid;
}
.right {
  width: 90px;
  height: 200px;
  border: 1px solid;
}
.paramsLeft {
  float: left;
}
</style>