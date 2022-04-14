<script>
import axios from 'axios';
export default {
  data() {
    return {
      address: '',
      distance: 500,
      list: []
    }
  },
  methods: {
    clear() {
      this.address = '';
      this.distance = 500;
      this.list = [];
    },
    async search() {
      // 请求接口
      const params = {
        input: this.address,
        distance: this.distance,
      };
       const res = await axios.post('https://8ucr04gpxf.execute-api.ap-southeast-1.amazonaws.com/dev/event', params)
       this.list = res.data.body;
       console.log(res.data.body);
    }
  }
}
</script>

<template>
  <div class="wrapper">
      <div class="form-item">
      <div class="label">Address/Postal Code:</div>
      <div class="">
        <input type="text" v-model="address">
      </div>
    </div>

    <div class="form-item">
      <div class="label">Distance:</div>
      <div class="">
        <select v-model="distance" name="distance" id="distance">
          <option value="300">300</option>
          <option value="500">500</option>
          <option value="600">600</option>
          <option value="700">700</option>
          <option value="800">800</option>
          <option value="900">900</option>
          <option value="1000">1000</option>
        </select>
      </div>
    </div>

    <div class="controls">
      <button @click="clear">clear</button>
      <button @click="search">search</button>
    </div>

    <div class="list">
      <div v-for="item in list">
        <div>{{item}}</div>

      </div>
    </div>
  </div>

</template>

<style>
@import './assets/base.css';

.wrapper {
  padding: 20px;
}

.form-item {
  display: flex;
  margin-top: 20px;
}

.label {
  margin-right: 5px;
  width: 150px;
  text-align: right;
}

.controls {
  margin-top: 20px;
}

.controls button {
  margin-right: 10px;
}
</style>
