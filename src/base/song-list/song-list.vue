<template>
  <div class="song-list">
    <ul>
    	<li class="item" v-for="(song, index) in songs" @click="selectItem(song, index)">
    		<div class="rank" v-show="rank">
    			<span :class="getRankCls(index)"></span>
    		</div>
    		<div class="content">
    			<h2 class="name">{{song.name}}</h2>
    			<p class="desc">{{getDesc(song)}}</p>
    		</div>
    	</li>
    </ul>
  </div>
</template>

<script  type="text/ecmascript-6">
export default {
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  props: {
    songs: {
      type: Array,
      default: []
    },
    rank: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    getRankCls (index) {
      return index <= 2 ? `icon icon${index}` : 'text'
    },
    getDesc (song) {
      return `${song.singer}-${song.album}`
    },
    // 点击选择播放的歌曲
    selectItem (item, index) {
      this.$emit('select', item, index)
    }
  },
  watch: {
    songs (newSongs) {
      // console.log(newSongs)
    }
  }
}
</script>


<style scoped lang="stylus" rel="stylesheet/stylus" >
@import "~common/stylus/variable"
@import "~common/stylus/mixin"

.song-list
  .item
    display: flex
    align-items: center
    box-sizing: border-box
    height: 64px
    font-size: 14px
    .rank
      flex: 0 0 25px
      width: 25px
      margin-right: 30px
      text-align: center
      .icon
        display: inline-block
        width: 25px
        height: 24px
        background-size: 25px 24px
        &.icon0
          bg-image('first')
        &.icon1
          bg-image('second')
        &.icon2
          bg-image('third')
      .text
        color: $color-theme
        font-size: $font-size-large
    .content
      flex: 1
      line-height: 20px
      overflow: hidden
      .name
        no-wrap()
        color: $color-text
      .desc
        no-wrap()
        margin-top: 4px
        color: $color-text-d
</style>
