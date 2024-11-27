<template>
  <el-checkbox-group v-model="checkedCities">
    <el-checkbox v-for="city in cities" :label="city.name" :key="city.name" :checked="city.isSeclected">{{city.name}}</el-checkbox>
  </el-checkbox-group>
</template>
<script>
export default {
  data () {
    return {
      checkedCities: [],
      cities: [{name: '上海', isSeclected: true, key: 1, value: 1},
        {name: '北京', isSeclected: false, key: 2, value: 2}
      ]
    }
  },
  methods: {
    handleData () {
      this.cities = [].concat([
        {name: '上海', isSeclected: true, key: 1, value: 1},
        {name: '北京', isSeclected: true, key: 2, value: 2}
      ])
      this.checkedCities = this.cities
        .filter(city => city.isSeclected)
        .map(city => city.name)
      console.log(this.cities, this.checkedCities)
    }
  }
}
</script>
<style scoped></style>
