<template>
  <div class="hello">
    <h1>飲料訂單列表</h1>
    <button @click="addlist">新增訂單</button>
    <br>
    <li>
      <ul v-for="item in list"
        :key="item._id">
        {{item.name}}
        <button @click="editlist">編輯</button>
        <button @click="deletelist">刪除</button>
      </ul>
    </li>
  </div>
</template>

<script>
export default {
  name: "hello",
  props: {
    msg: String
  },
  data() {
    return {
      list: [
        {
          createdAt: "2019-12-24T08:38:51.412Z",
          _id: "5e01ced27c5181128689db2b",
          name: "巧克力奶茶",
          price: 40,
          username: "Vincent",
          description: "少冰半糖"
        },
        {
          createdAt: "2019-12-24T08:38:51.412Z",
          _id: "5e01c160f0cd15116ed6a848",
          name: "咖啡牛奶",
          price: 55,
          username: "王小明",
          description: "少冰全糖"
        },
        {
          createdAt: "2019-12-24T08:38:51.412Z",
          _id: "5e01cbef705d1712406b6074",
          name: "焦糖可可",
          price: 45,
          username: "jessica",
          description: "少冰全糖"
        }
      ]
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
