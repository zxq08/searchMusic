<template>
  <div>
    <div class="input-wrap">
      <i class="iconfont icon-sousuo"></i>
      <input class="search-input" type="text" v-model="searchName" name="" id="" placeholder="搜索歌曲">
      <i class="iconfont icon-guanbi" v-if="searchName"></i>
      <!-- <input class="search-input" type="text" v-model="searchName" name="" id="" placeholder="搜索歌曲" @input="inputSearch" @keyup.13="search">
      <i class="iconfont icon-guanbi" v-if="searchName" @click="clearSearch"></i> -->
    </div>
    <template v-if="searchType == 1">
      <!-- <div class="history-wrap">
        <div class="history-header">
          <div class="history-title">历史记录</div>
          <i class="iconfont icon-shanchu" @click="removeHistory('historyList')"></i>
        </div>
        <div class="history-list">
          <div class="history-item" v-for="(item, index) in historyList" :key="index" @click="searchHis(item)">{{ item }}</div>
        </div>
      </div> -->
      <div class="hot-wrap">
        <div class="hot-header">
          <div class="hot-title">热搜榜</div>
        </div>
        <ul class="hot-list">
          <li class="hot-item" v-for="(item, index) in hotList" :key="index">
            <div :class="index < 3? 'hotindex hot'+ index +'color' : 'hotindex'">
              {{ index + 1 }}
            </div>
            <div class="hotbody">
              <p class="hotname-wrap">
                <span>{{ item.searchWord }}</span>
                <img v-show="item.iconUrl" class="hot-img" :src="item.iconUrl" alt="">
              </p>
              <p class="hotdesc">
                <span>{{ item.content }}</span>
              </p>
            </div>
            <div class="hottimes">
              {{ item.score }}
            </div>
          </li>
        </ul>
      </div>
    </template>
    <template v-else-if="searchType == 2">
      <!-- <ul class="result-wrap">
        <li class="result-item" v-for="item in resultList" :key="item.id">
          <div class="result-info">
            <p class="result-name">
              {{ item.name }}
            </p>
            <p class="result-singer">
              <img v-if="item.isSq" class="tag-img" src="./assets/sq.png" alt="">
              <img v-if="item.isVip" class="tag-img" src="./assets/vip.png" alt="">
              {{ item.artists[0].name }} - {{ item.album.name }}
            </p>
          </div>
          <div class="result-play">
            <i class="iconfont icon-shipin" @click="play(item)"></i>
          </div>
        </li>
      </ul> -->
    </template>
    <template v-else-if="searchType == 3">
      <!-- <ul class="result-wrap" v-if="searchName">
        <li class="search-tips" @click="search()">
          搜索"{{ searchName }}"
        </li>
        <li class="search-item" v-for="(item, index) in searchList" :key="index" @click="searchEnter(item.keyword)">
          <i class="iconfont icon-sousuo"></i>
          <span>{{ item.keyword }}</span>
        </li>
      </ul> -->
    </template>
  </div>
</template>
<script>
import "@/style/iconfont.css"
import { reactive, ref, toRefs, onMounted } from '@vue/composition-api'
import axios from 'axios'

export default {
  name: 'searchV3',
  setup() {
    const searchName = ref('')
    const searchType = ref(1)
    const { hotList } = useSearchHot()

    return {
      searchName,
      searchType,
      hotList
    }
  }
}

function useSearchHot () {
  const state = reactive({
    hotList: []
  })
  onMounted(() => {
    axios.get('/search/hot/detail').then(res => {
      state.hotList = res.data.data
    })
  })
  return toRefs(state)
}
</script>
<style>
* {
  margin: 0;
}
html, body, #app {
  height: 100%;
}
ul {
  list-style: none;
}
.input-wrap {
  margin: 0 auto;
  position: relative;
}
.search-input {
  width: calc(100% - 40px);
  font-size: 14px;
  outline: none;
  border-radius:10px;
  border: none;
  background-color: #f3f3f3;
  margin: 20px 0 0 20px;
  padding: 5px 30px 5px 30px;
  box-sizing: border-box;
  color: #333;
}
.input-wrap .icon-sousuo,.input-wrap  .icon-guanbi {
  position: absolute;
  top: 28px;
  z-index: 99;
  font-size: 14px;
  color: #333;
}
.input-wrap .icon-guanbi {
  right: 30px;
}
.input-wrap .icon-sousuo {
  left: 30px;
  top: 25px;
  font-size: 16px;
}
.history-wrap, .hot-wrap {
  margin-top: 30px;
}
.history-header, .history-list, .hot-header {
  padding: 10px 20px;
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}
.history-title, .hot-title {
  font-size: 16px;
  font-weight: 700;
  color: #555;
}
.history-list {
  justify-content: flex-start;
  flex-wrap: wrap;
}
.history-item {
  margin: 5px;
  border-radius: 20px;
  background-color: #ebebeb;
  padding: 5px 15px;
  font-size: 14px;
}
.hot-list {
  list-style: none;
  padding: 0 20px;
}
.hot-item {
  display: flex;
  /* justify-content: flex-start; */
  align-items: center;
  margin: 25px 0;
}
.hotindex {
  font-size: 20px;
  flex-basis: 5%;
}
.hot0color {
  color: red;
}
.hot1color {
  color: orangered;
}
.hot2color {
  color: orange;
}
.hotbody {
  flex-basis: 70%;
  margin: 0 10px;
}
.hotname-wrap {
  display: flex;
}
.hot-img {
  width: 30px;
  height: 24px;
  margin: -2px 0 0 5px;
}
.hotdesc {
  font-size: 12px;
  color: #ddd;
}
.hottimes {
  color: #aaa;
}
.result-wrap {
  list-style: none;
  padding: 20px;
}
.result-item {
  padding: 10px 0 10px 5px;
  border-bottom: 1px solid #ddd;
  display: flex;
  justify-content: space-between;
}
.result-item:first-child {
  border-top: 1px solid #ddd;
}
.result-info {
  display: flex;
  flex-direction: column;
}
.result-name {
  font-size: 18px;
  color: #296ce5;
}
.result-singer {
  display: flex;
  align-items: center;
  font-size: 14px;
  color: #555;
}
.tag-img {
  width: 20px;
  height: 20px;
  margin-right: 2px;
}
.result-play {
  flex-basis: 10%;
  display: flex;
  align-items: center;
}
.result-play > .iconfont {
  font-size: 24px;
}
</style>
<style>
.search-tips {
  padding: 5px 0 10px 0;
  font-size: 14px;
  color: #296ce5;
}
.search-item {
  padding: 10px 5px;
}
.search-item .iconfont {
  margin-right: 10px;
}
.search-item > span {
  font-size: 14px;
  color: #555;
}
</style>
