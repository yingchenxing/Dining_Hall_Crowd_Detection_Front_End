<template>
  <el-container style="height: 100%; border: 1px solid #eee">
    <el-aside width="200px" style="background-color: rgb(238, 241, 246);height: 100%">
      <div style="height: 60px;line-height: 60px;text-align: center">
        <img src="../assets/logo.png" alt="" style="width: 150px;position: relative;top:5px;margin-left: 5px">
      </div>
      <el-menu :default-openeds="['1', '3']">
        <el-menu-item index="1-2">Dining Hall</el-menu-item>
      </el-menu>
    </el-aside>

    <el-container>
      <el-header style="text-align: right; font-size: 12px;background-color: #841f41;color: white">
        <el-dropdown>
          <i class="el-icon-setting" style="margin-right: 15px"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>view</el-dropdown-item>
            <el-dropdown-item>log out</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
        <span>Admin</span>
      </el-header>

      <el-main>
        <el-table :data="tableData">
          <el-table-column prop="id" label="ID">
          </el-table-column>
          <el-table-column prop="name" label="Name">
          </el-table-column>
          <el-table-column prop="number" label="Number of people">
          </el-table-column>
          <el-table-column prop="isOpen" label="Open">
            <template slot-scope="scope">
              <el-switch v-model="scope.row.isOpen" active-color="#13ce66" inactive-color="#ccc"
                         @change="changeEnable(scope.row)"
                         :active-value=true
                         :inactive-value=false></el-switch>
            </template>
          </el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </el-container>
</template>

<style>
.el-header {
  background-color: #B3C0D1;
  color: #333;
  line-height: 60px;
}

.el-aside {
  color: #333;
}
</style>

<script>
export default {
  name: 'HomeView',
  data() {

    return {
      tableData: [],
    }
  },
  created() {
    this.load();
  },
  methods: {
    load() {
      // this.request.get("/hall").then(res => {
      //   console.log(res)
      //   this.tableData = res.data
      //   // this.total = res.data.total
      // })
      fetch("http://localhost:8080/hall").then(res => res.json()).then(res => {
        console.log(res),
            this.tableData = res
      })
    },
    changeEnable(item){
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(item)
      };
      fetch("http://172.29.45.214:8080/hall", requestOptions)
          .then(response => response.json())
    }


  }
};
</script>