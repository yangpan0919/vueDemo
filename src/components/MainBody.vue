<template>
  <div>
    <h2 v-show="firstView">请输入关键字搜索</h2>
    <h2 v-show="loading">请求中...</h2>
    <h2 v-show="errorMsg">{{errorMsg}}</h2>
    <div class="row" v-show="users.length>0">

      <div class="card" v-for="(user,index) in users" :key="index">
        <a :href="user.target_url" target="_blank">
          <img :src="user.pic_src" style='width: 100px'/>
        </a>
        <p class="card-text">{{user.name}}</p>
      </div>
    </div>
  </div>
</template>

<script>
  import PubSub from 'pubsub-js'
  import axios from 'axios'

  export default {
    name: 'MainBody',
    data () {
      return {
        firstView: true,
        loading: false,
        errorMsg: '',
        users: []
      }
    },
    mounted () {
      PubSub.subscribe('search', (msg, searchName) => {
        this.firstView = false
        this.loading = true
        this.errorMsg = ''
        this.users = []

        // 发ajax请求进行搜索
        const url = `https://api.github.com/search/users?q=${searchName}`
        axios.get(url)
          .then(response => {
// 成功了, 更新数据(成功)
              this.loading = false
              this.users = response.data.items.map(item => ({
                target_url: item.html_url,
                pic_src: item.avatar_url,
                name: item.login
              }))
            }
          )
          .catch(error => {
              // 失败了, 更新数据(失败)
              this.loading = false
              this.errorMsg = '请求失败!'
            }
          )

      })
    }
  }
</script>

<style scoped>
  .card {
    float: left;
    width: 33.333%;
    padding: .75rem;
    margin-bottom: 2rem;
    border: 1px solid #efefef;
    text-align: center;
  }

  .card > img {
    margin-bottom: .75rem;
    border-radius: 100px;
  }

  .card-text {
    font-size: 85%;
  }

</style>
