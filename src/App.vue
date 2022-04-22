<script>
import axios from 'axios';
import ListItem from './ListItem.vue';
export default {
    data() {
        return {
            formvalue: {},
            list: []
        };
    },
    methods: {
        clear() {
            this.formvalue = {};
            this.list = [];
        },
        async search() {
            // 请求接口
            const params = this.formvalue;
            const res = await axios.post("https://8ucr04gpxf.execute-api.ap-southeast-1.amazonaws.com/dev/event", params);
            this.list = res.data.body[0].ResultList;
        }
    },
    components: { ListItem }
}
</script>

<template>
  <div class="wrapper">

      <div class="header">
        <div class="logo">
          <img src="./assets/logo.png" alt="">
        </div>
        <div class="title">
          <h1>EBD team 7</h1>
          <h1>Carpark Recommendation System</h1>
        </div>
      </div>

      

      <el-card shadow="always" class="card">
        <el-form
          ref="form"
          :model="formvalue"
          label-width="auto"
          size="large"
        >
          <el-form-item class="form-item" label="Address/Postal Code">
            <el-input class="form-field"   v-model="formvalue.input" />
          </el-form-item>

          <el-form-item label="Distance" class="form-item">
            <el-select
              v-model="formvalue.distance"
              placeholder="please select your distance"
              class="form-field"
            >
              <el-option label="300m" :value="300" />
              <el-option label="500m" :value="500" />
              <el-option label="1000m" :value="600" />
            </el-select>
          </el-form-item>
          
        </el-form>

        <div class="controls">
          <el-button type="primary" color="#48c78e" size="large" @click="clear">Clear</el-button>
          <el-button type="primary" color="#48c78e" size="large" @click="search">Search</el-button>
        </div>
        
      </el-card>

      <el-collapse class="list">
        <el-collapse-item v-for="(item, index) in list" :key="item.Address" :title="`${item.Address}  ====>>     Available Lots:${item.Current_Lots_Available}  `">
          <ListItem :data="item" :index="index" />
        </el-collapse-item>
      </el-collapse>
  </div>

</template>

<style>
@import './assets/base.css';

.header {
  display: flex;
}

.header .logo img {
  width: 200px;
  height: 200px;
}

h1 {
  font-weight: 900;
  font-size: 60px;
  margin-left: 20px;
}

.card {
  margin-top: 50px;
  background-color: #effaf5;
  border-radius: 10px;
  height: 400px;
}

.card .el-form-item__label {
  color: #48c78e;
  font-size: 30px;
}

.card .form-field {
  width: 500px
}

.wrapper {
  padding: 20px;
}

.form-item {
  margin-bottom: 50px;
}

.form-item input, .form-item select {
  height: 60px !important;
  font-size: 20px;
}

.label {
  margin-right: 5px;
  width: 150px;
  text-align: right;
}

.controls {
  margin-top: 20px;
  margin-left: 285px;
}

.controls button {
  margin-right: 50px;
  color: #fff;
  width: 150px;
  height: 50px;
  font-size: 24px;
}

.list {
  margin-top: 20px;
  margin-left: 10px;
  width: calc(100% - 20px);
}

.list .el-collapse-item__header {
  font-weight: 600;
  font-size: 30px;
}

.list .el-collapse-item__content {
  font-size: 20px;
}

.list .el-collapse-item__header {
  color: #2cd8a1;
  background-color: #effaf5;
  height: 80px;
  padding-left: 20px;
}
</style>
