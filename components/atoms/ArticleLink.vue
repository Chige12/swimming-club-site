<template lang="pug">
.article_link_box
  nuxt-link(:to="`/${type}_page/${list.sourceBase.slice(0,-3)}`").article_link
    .article_sub_info
      .article_created_at {{createdAt}} 作成
      .article_new(v-if="list.new_article") NEW!
    .article_text
      .article_title {{list.title}}
      .article_place(v-if="list.place") @{{list.place}}
</template>
<script>
export default {
  props:["list","type"],
  computed:{
    createdAt(){
      return this.list.created_at.split('T')[0].split('-').join('/')
    }
  }
}
</script>
<style lang="scss" scoped>
@import "~/assets/style/normalize.scss";
@import "~/assets/style/variables.scss";
@import "~/assets/style/mixin.scss";

.article_link_box{
  margin: 6px 0;
  padding: 4px 12px;
  transition: .3s $bezier-ease-out;
  position: relative;
  z-index: 0;
  &::after{
    content: "";
    position: absolute;
    top: 0%;
    bottom: 0;
    left: 0;
    margin:auto;
    width: 100%;
    height: 0;
    background: #fff;
    z-index: -1;
    transition: .3s $bezier-ease-out;
  }
  &:hover{
    &::after{
      height: 100%;
      background-color: rgba($theme-blue,.04);
    }
    .article_title, .article_place{
      color: $theme-sky;
    }
  }
}
.article_sub_info{
  display: flex;
  flex-wrap: nowrap;
}
.article_new {
  padding-left: 20px;
  font-weight: bold;
  color: #f00f66;
}


.article_text {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}
.article_title{
  @include noto-font(2.2rem,$theme-blue);
  transition: .3s $bezier-ease-out;
  margin-right: 25px;
}
.article_place {
  @include noto-font(1.8rem,$theme-blue);
  transition: .3s $bezier-ease-out;
  margin-left: 2px;
}
</style>