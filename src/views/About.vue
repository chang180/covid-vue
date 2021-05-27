<template>
  <div class="example">
    <h1>顯示圖形</h1>
    <!-- <select v-model="cityComputed"> -->
    <select v-model="citySelect">
      <template v-if="citySelect === null">
        <option :value="null">請選擇</option>
      </template>
      <option v-for="city of cities" :value="city" :key="city">{{
        city
      }}</option>
    </select>
    <select v-model="disSelect">
      <template v-if="disSelect === null">
        <option :value="null">請選擇</option>
      </template>
      <option
        v-for="(dis, index) of districts"
        :value="index"
        :key="dis.name"
        >{{ dis.name }}</option
      >
    </select>
    <template v-if="disSelect != null">
      {{ '顯示圖形' }}
    </template>
  </div>
</template>
<script>
const covid = require('@/assets/covid.json')
export default {
  data () {
    return {
      citySelect: null,
      disSelect: null
    }
  },
  computed: {
    covidData () {
      console.log(covid)
      return covid
    },
    cities () {
      // return ['台北市', '新北市']
      const set = new Set()
      const result = covid.filter(item =>
        !set.has(item['縣市']) ? set.add(item['縣市']) : false
      )
      // console.log(result)
      const cities = []
      result.forEach((element, index) => {
        cities.push(result[index]['縣市'])
      })
      // console.log(cities)
      return cities
    },
    districts () {
      const set = new Set()
      const result1 = covid.filter(item =>
        !set.has(item['鄉鎮']) ? set.add(item['鄉鎮']) : false
      )
      const districts = []
      result1.forEach((element, index) => {
        districts.push(result1[index]['鄉鎮'])
      })
      // if (this.citySelect !== null) {
      //   districts = this.covidData['鄉鎮']
      // }
      console.log(districts)
      return districts
    }
  },
  watch: {
    citySelect (nVal, oVal) {
      // console.log(nVal, postData[this.citySelect].districts.length)
      // this.disSelect = null
      if (this.disSelect >= this.postData[this.citySelect].districts.length) {
        this.disSelect = 0
      }
    }
  }
}
</script>
