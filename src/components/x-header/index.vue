<template>
  <div class="x-header">
    <div class="x-header-left">
      <a class="x-header-back" @click.preventDefault v-show="leftOptions.showBack" @click="onClickBack">{{leftOptions.backText}}</a>
      <slot name="left"></slot>
    </div>
    <h1 class="x-header-title"><slot></slot></h1>
    <div class="x-header-right">
      <a class="x-header-more" @click.preventDefault @click="$emit('on-click-more')" v-if="rightOptions.showMore"></a>
      <slot name="right"></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    leftOptions: {
      type: Object,
      default () {
        return {
          showBack: true,
          backText: 'Back',
          preventGoBack: false
        }
      }
    },
    rightOptions: {
      type: Object,
      default () {
        return {
          showMore: false
        }
      }
    }
  },
  methods: {
    onClickBack () {
      if (this.leftOptions.preventGoBack) {
        this.$emit('on-click-back')
      } else {
        history.back()
      }
    }
  }
}
</script>

<style>
.x-header {
  position: relative;
  padding: 3px 0;
  -webkit-box-sizing: border-box;
  background-color: #35495e;
}
.x-header .x-header-title,.x-header h1 {
  margin: 0 88px;
  margin-left: 100px;
  line-height: 40px;
  text-align: center;
  height: 40px;
  font-size: 18px;
  font-weight: 400;
  width: auto;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  color: #fff
}
.x-header .x-header-title a,.x-header .x-header-title a:active,.x-header h1 a,.x-header h1 a:active {
  color: #fff
}
.x-header .x-header-left,.x-header .x-header-right {
  position: absolute;
  top: 14px;
  display: block;
  font-size: 14px;
  line-height: 21px;
  color: #ccc
}
.x-header .x-header-left a,.x-header .x-header-left button,.x-header .x-header-right a,.x-header .x-header-right button {
  float: left;
  margin-right: 8px;
  color: #ccc
}
.x-header .x-header-left a:active,.x-header .x-header-left button:active,.x-header .x-header-right a:active,.x-header .x-header-right button:active {
  opacity: .5
}
.x-header .x-header-left {
  left: 18px
}
.x-header .x-header-left .x-header-back {
  padding-left: 16px
}
.x-header .x-header-left .x-header-back:before {
  content: "";
  position: absolute;
  display: block;
  top: 2px;
  left: 0;
  width: 12px;
  height: 12px;
  border: 1px solid #ccc;
  border-width: 1px 0 0 1px;
  margin-left: 3px;
  margin-top: 1px;
  transform: rotate(315deg)
}
.x-header .x-header-right {
  right: 15px
}
.x-header .x-header-right a,.x-header .x-header-right button {
  margin-left: 8px;
  margin-right: 0
}
.x-header .x-header-right .x-header-more:after {
  content: "\2022\0020\2022\0020\2022\0020";
  font-size: 16px;
}
</style>
