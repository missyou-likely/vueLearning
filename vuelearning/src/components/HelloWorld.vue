<template>
  <div class="hello">
    <!-- 购物车数据渲染 -->
    <div v-for="(item, index) in arr" :key="index">
      <p>
        <input
          type="checkbox"
          v-model="item.ischeck"
          @click="changeOne(index)"
        />
        {{ item.name }} -------价格：{{ item.price }}
      </p>
    </div>
    <!-- 底部 -->
    <div class="footer">
      <input
        type="checkbox"
        v-model="checkAll"
        @click="changeAlls(checkAll)"
      />全选---
    </div>
    <div style="margin-top: 20px">总价：{{ allPrice }}</div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      //模拟购物车数据arr
      arr: [
        {
          ischeck: false, //默认为false
          name: "篮球",
          price: 98,
        },
        {
          ischeck: false, //默认为false
          name: "足球",
          price: 10,
        },
        {
          ischeck: false, //默认为false
          name: "羽毛球",
          price: 5,
        },
        {
          ischeck: false, //默认为false
          name: "排球",
          price: 100,
        },
      ],
      checkAll: false,
      allPrice: 0,
    };
  },
  methods: {
    // 封装计算总价方法，在每次勾选单选框或者全选框时，便利arr数组里isCheck的值为true的集合，相加它们的价格，通过v-model计算总价
    countPrice() {
      let _price = 0;
      this.arr.forEach((item) => {
        if (item.ischeck) {
          _price = _price + item.price;
        }
      });
      this.allPrice = _price;
    },
    //关键步一，单选时，便利数组，使用findIndex方法，确定this.checkAll的值
    all() {
      let _index = this.arr.findIndex((item) => {
        return !item.ischeck;
      });
      //findIndex会传入一个函数，return值为true的第一个元素的位置，
      //如果没有符合条件的元素则返回-1
      if (_index === -1) {
        this.checkAll = true;
      } else {
        this.checkAll = false;
      }
      this.countPrice();
    },
    // 勾选全选框时，将this.checkAll的值赋给所有的单选项
    changeAlls() {
      let checkAllValue = !this.checkAll;
      this.arr.forEach((item) => {
        return (item.ischeck = checkAllValue);
      });
      this.countPrice();
    },
    changeOne(item) {
      this.arr[item].ischeck = !this.arr[item].ischeck;
      this.all();
      this.countPrice();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
</style>
