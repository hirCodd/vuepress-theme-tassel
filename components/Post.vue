<template>
  <div class="post-content" style="margin-top: 50px">
    <div class="content-top">Posts</div>
    <hr/>
    <div class="post-card">
      <el-card v-for="item in PostsArray.slice((currentPage-1)*pagesize, currentPage*pagesize)">
        <p class="article-title">
          <router-link :to="item.regularPath">{{ item.frontmatter.title }}</router-link>
        </p>
        <div class="abstract" v-html="item.excerpt">{{item.excerpt}}</div>
        <hr/>
        <div class="archives-tag">
          <i class="fa fa-user" aria-hidden="true">{{ item.frontmatter.author || $site.themeConfig.author }}</i>
          <i class="fa fa-calendar" aria-hidden="true">{{ item.frontmatter.date }}</i>
          <i class="fa fa-tag" aria-hidden="true" v-for="tag in pages.frontmatter.tags">{{ tag }}</i>
        </div>
      </el-card>
    </div>
    <div class="pages-data">
      <el-pagination
        background
        layout="prev, pager, next"
        :page-size="15"
        :current-page.sync="currentPage"
        :total="PostArrayLength">
      </el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  name: "Post",
  data() {
    return {
      currentPage:1, //初始页
      pagesize:15,    //    每页的数据
      PostsArray: [],
      PostArrayLength: 0
    };
  },
  mounted: function() {
    this.filterPostsList();
  },
  methods: {
    /**
     * @description: select post=true
     * @param {type}
     * @return:
     */
    filterPostsList() {
      this.$site.pages.forEach(element => {
        if (element.frontmatter.post == true) {
          element.frontmatter.date = this.formatDate(
            element.frontmatter.date
          );
          element.ArticleDate = this.formatDate(element.frontmatter.date);
          this.PostsArray.push(element);
        }
      });
      // 通过时间进行排序
      this.PostsArray.sort(this.compare('ArticleDate'));
      // count Archives length
      this.PostArrayLength = this.PostsArray.length;
    },
    /**
     * @description: format date
     * @param {type}
     * @return:
     */
    formatDate(time) {
      var dateTime = new Date(new Date(time).getTime());
      var y = dateTime.getFullYear();
      var month = dateTime.getMonth() + 1;
      var m = month < 10 ? "0" + month : month;
      var d =
        dateTime.getDate() < 10 ? "0" + dateTime.getDate() : dateTime.getDate();
      var sendDate = y + "-" + m + "-" + d;
      return sendDate;
    },
    /**
     * @description: 对时间进行排序
     * @param {type}
     * @return:
     */
    compare(pro) {
      return function(obj1, obj2) {
        var val1 = obj1[pro];
        var val2 = obj2[pro];
        if (val1 < val2) {
          //正序
          return 1;
        } else if (val1 > val2) {
          return -1;
        } else {
          return 0;
        }
      };
    }
  }
};
</script>
<style>
.post-content > .content-top {
  margin: 5px 0 15px 0px;
  font-size: 18px;
  font-weight: 600;
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB",
    "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
}
.post-card {
  margin-top: 20px;
}
.post-card>.el-card {
  margin: 10px 0;
}
.archives-tag i{
  padding: 3px;
}
.el-timeline-item__content > .el-card > .el-card__body {
  text-align: left;
}
.el-card > .el-card__body > .article-title {
  font-size: 1.3em;
  color: black;
  font-weight: 600;
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB",
    "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
}
.archives-tag > .article-tag {
  font-size: 14px;
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB",
    "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
}
.archives-tag > .article-tag > .el-tag {
  margin-left: 5px;
}
</style>
