<template>
  <div class="title-content" v-if="pages.frontmatter.post == true">
    <el-card class="box-card" shadow="never">
      <h2>{{pages.frontmatter.title}}</h2>
      <!-- <el-tag>原创</el-tag><br/> -->
      <div class="page-info">
        <i class="fa fa-user" aria-hidden="true">{{ pages.author || $site.themeConfig.author }}</i>
        <i class="fa fa-tag" aria-hidden="true" v-for="tag in pages.frontmatter.tags">{{ tag }}</i>
        <i class="fa fa-calendar" aria-hidden="true">{{ pages.frontmatter.date }}</i>
        <span id="pages.frontmatter.title" class="leancloud-visitors" data-flag-title="pages.frontmatter.title">
          <i class="fa fa-eye" aria-hidden="true"></i>
          <i class="leancloud-visitors-count">1000000</i>
        </span>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "TitleContent",
  props: {
    pages: {
      type: Object,
      default: []
    }
  },
}
</script>

<style>
.title-content {
  max-width: 740px;
  margin: 0 auto;
  padding-top: 5.5rem;
}
.page-info i{
  padding: 3px;
}
.title-content>.el-card>.el-card__body h2{
  text-align: center
}
.tags>.el-tag {
  margin-left: 10px;
}
</style>


