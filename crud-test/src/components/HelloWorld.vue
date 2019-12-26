<template>
  <div class="crudlist">
    <h1>飲料訂單列表</h1>
    <form id="app"
      @submit="checkForm"
      action="/something"
      method="post">
      <div>
        <label for="additemName">{{additemName}}</label>
        <input type="text"
          name="additemName"
          id="additemName"
          min="0">
        <!-- 2 -->
        <label for="additemNumber">{{additemNumber}}</label>
        <input type="text"
          name="additemNumber"
          id="additemNumber"
          min="0">
        <!-- 3 -->
        <label for="additemUser">{{additemUser}}</label>
        <input type="text"
          name="additemUser"
          id="additemUser"
          min="0">
        <!-- 4 -->
        <label for="additemOther">{{additemOther}}</label>
        <input type="text"
          name="additemOther"
          id="additemOther"
          min="0">
        <button @click="addlist">新增訂單</button>
      </div>

    </form>

    <br>
    <hr>
    <table>
      <!-- title -->
      <tr>
        <th v-for="header in tableTitle"
          :key="header.title">{{header.title}}</th>
      </tr>

      <!-- content -->
      <tr v-for="item in list"
        :key="item._id">
        <td>{{item.name}}</td>
        <td>{{item.price}}</td>
        <td>{{item.username}}</td>
        <td>{{item.description}}</td>
        <button @click="editlist">編輯</button>
        <button @click="deletelist">刪除</button>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "crudlist",
  apiurl:
    "https://restfull-api-todolist.herokuapp.com/api/v1/orders?limit=3&page=1",
  props: {
    msg: String
  },

  data() {
    return {
      results: [],
      additemName: "飲料名稱",
      additemNumber: "價格",
      additemUser: "訂購人姓名",
      additemOther: "備註",
      checkForm: "",
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
      ],
      tableTitle: [
        {
          title: "飲料名稱"
        },
        {
          title: "價格"
        },
        {
          title: "訂購人姓名"
        },
        {
          title: "備註"
        }
      ]
    };
  },
  mounted() {
    axios
      .get(
        "https://restfull-api-todolist.herokuapp.com/api/v1/orders?limit=3&page=1"
      )
      .then(response => {
        this.results = response.data.results;
      });
  },
  methods: {
    addlist() {
      var days = new Date();
      this.list.push({
        createdAt: days
        // name: this.additem,
        // price: this.addprice,
        // username: this.username,
        // description: this.description
      });
    },
    editlist() {},
    deletelist() {}
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
