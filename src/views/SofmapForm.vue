<template>
  <div id="app">
    <div>
        <h3>Sofmap</h3>
        <label for="detail">祖父地図の内容</label>
        <textarea
        id="detail"
        cols="30"
        rows="3"
        v-model="eventData.detail"
        ></textarea>
        <p style="white-space: pre;">{{eventData.detail}}</p>
        <p>地域</p>
        <input
        type="radio"
        id="akiba"
        value="秋葉原"
        v-model="eventData.region"
        >
        <label for="akiba">秋葉原</label>
        <input
        type="radio"
        id="ponbashi"
        value="日本橋"
        v-model="eventData.region"
        >
        <label for="ponbashi">日本橋</label>
        <p>{{eventData.region}}</p>
        <!---->
        <p>ソフト・ハード</p>
        <input
        type="checkbox"
        id="soft"
        value="ソフト"
        v-model="eventData.softhard"
        >
        <label for="soft">ソフト</label>
        <input
        type="checkbox"
        id="hard"
        value="ハード"
        v-model="eventData.softhard"
        >
        <label for="hard">ハード</label>
        <p>{{eventData.softhard}}</p>
        <!---->
        <p>プラットフォーム</p>
        <select v-model="eventData.platform">
            <option
            v-for="pf in platforms"
            :key="pf"
            >{{pf}}</option>
        </select>
        <p>{{eventData.platform}}</p>
        <button @click="postInfo">情報を送信</button>
        <p>{{apiResult1}}</p>
        <button @click="getShop">店舗を取得</button>
        <h3>店舗</h3>
        <p>{{apiResult2}}</p>
        <ul>
            <li v-for='(value, index) in apiResult2' :key='index'>{{value}}</li>
        </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  data() {
    return {
      msg2: 'Welcome Sofmap',
      platforms: ["PS4", "XboxOne", "Switch"],
      eventData: {
        title: "タイトル",
        detail: "",
        region: "秋葉原",
        regionCode: "akiba",
        softhard: [],
        platform: "PS4"
      },
      apiResult1: "",
      apiResult2: []
    };
  },
  created() {
      axios.get('https://[server]/getSofmapInfo?region=aaa')
      .then(response => {
              this.apiResult2 = response.data.shop
          }).catch(error => {
              this.apiResult2 = error
          });
  },
  methods: {
      postInfo() {
          if(this.eventData.region == "秋葉原") {
              this.eventData.regionCode = "akiba"
          } else if(this.eventData.region == "日本橋") {
              this.eventData.regionCode = "ponbashi"
          } else {
              this.eventData.regionCode = "not spec"
          }
          axios.post('https://[server]/postSofmapConditions',
            {
            regions: this.eventData.regionCode,
            foo: "bar",
            x: [1, 2, 3],
            foo2: "bar2",
            }, {
            'Content-Type': 'application/json'
            }
          ).then(response => {
              this.apiResult1 = response.data
          }).catch(error => {
              this.apiResult1 = error
          });
      },
      getShop() {
        axios.get('https://[server]/getSofmapInfo?region='+this.eventData.regionCode)
        .then(response => {
                this.apiResult2 = response.data.shop
            }).catch(error => {
                this.apiResult2 = error
            });
      }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
