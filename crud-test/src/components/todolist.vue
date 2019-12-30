<template>
  <div class="crudlist">
    <h1>飲料訂單列表</h1>
    <!-- <form id="app"
      @submit="checkForm"
      action="/something"
      method="post"> -->
    <div>

      <label for="additemName">{{additemName}}</label>
      <input type="text"
        name="additemName"
        id="additemName"
        min="0"
        v-model.trim="imput">
      <!-- 2 -->
      <label for="additemNumber">{{additemNumber}}</label>
      <input type="text"
        name="additemNumber"
        id="additemNumber"
        min="0"
        v-model.trim="imput2">
      <!-- 3 -->
      <label for="additemUser">{{additemUser}}</label>
      <input type="text"
        name="additemUser"
        id="additemUser"
        min="0"
        v-model.trim="imput3">
      <!-- 4 -->
      <label for="additemOther">{{additemOther}}</label>
      <input type="text"
        name="additemOther"
        id="additemOther"
        min="0"
        v-model.trim="imput4">
      <button @click="addlist">新增訂單</button>
    </div>

    <!-- </form> -->

    <br>
    <hr>
    <table>
      <!-- title -->
      <tr>
        <th v-for="header in tableTitle"
          :key="header.title">{{header.title}}</th>
      </tr>

      <!-- content -->
      <tr v-for="item in results.data"
        :key="item._id">
        <td>{{item.name}}</td>
        <td>{{item.price}}</td>
        <td>{{item.username}}</td>
        <td>{{item.description}}</td>
        <button @click="editlist">編輯</button>
        <button @click="deletelist(results.data.id)">刪除</button>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "crudlist",
  props: {
    msg: String
  },
  data() {
    return {
      results: {},
      additemName: "飲料名稱",
      additemNumber: "價格",
      additemUser: "訂購人姓名",
      additemOther: "備註",
      checkForm: "",
      listid: "編號",
      imput: "",
      imput2: "",
      imput3: "",
      imput4: "",
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
      .get("https://restfull-api-todolist.herokuapp.com/api/v1/orders")
      .then(res => {
        this.results = res.data.data;
      });
  },
  methods: {
    addlist() {
      // var days = new Date();

      const url = "https://restfull-api-todolist.herokuapp.com/api/v1/orders";
      axios
        .post(
          url,
          {
            name: this.imput,
            price: this.imput2,
            username: this.imput3,
            description: this.imput4
          },
          {
            "Content-Type": "application / json"
          }
        )
        .then(res => {
          console.log(res.data);
          var priceTash = Number(this.res.data.price);
          this.results.push({
            name: this.res.data.name,
            price: priceTash,
            username: this.res.data.username,
            description: this.res.data.description
          });
        });
    },

    editlist() {},
    deletelist(id) {
      if (confirm("確認要刪除嗎?")) {
        axios
          .delete(
            `https://restfull-api-todolist.herokuapp.com/api/v1/orders/${id}`
          )
          .then(res => {
            console.log(res);
          });
      } else alert("已取消刪除操作");
    }
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
