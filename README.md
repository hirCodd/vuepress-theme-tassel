## Vuepress-theme-tassel
> a good theme for vuepress

### Usage
yarn add vuepress-theme-tassel

在config.js中的themeConfig配置如下参数
```js
    valineConfig: {
      appId: '',
      appKey: '',
      notify: false,
      verify: false,
      avatar: 'mm',
      placeholder: 'just go go...',
      pageSize: 15,
      visitor: true,
      highlight: true,
      recordIP: true
    },
    homeConfig: {
      homeSrc: 'https://finen-1251602255.cos.ap-shanghai.myqcloud.com/blog/home/hero.png',
      nickname: 'finen',
      signature: '你好',
      urllink1: '',
      urllink1_text: '',
      urllink2: '',
      urllink2_text: '',
      footer: '你好jafkldajsfdlasjfdlasjfdasljfdaslf  jaslfjsalfdasjflsakjflasfjaslfdjasflasjfkdlsafjsal'
    },
    blogConfig: {
      tag: {
        location: 3,     // 在导航栏菜单中所占的位置，默认3
        text: 'Tag'      // 默认文案 “标签”
      }
    },
    author: 'finen',
```

### element-ui