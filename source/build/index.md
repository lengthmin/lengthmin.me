---
title: build..
comments: false
toc: true
date: 2016-09-03 22:01:48
---

Here are what have I did and how to do that.

<!-- more -->
***
### 2018-01-17 设置更新时间
next主题在设置中可以开启

### 2018-01-14 更新最新版[NexT.Pisces](https://github.com/iissnan/hexo-theme-next)主题
1. 修改主题中language/zh-Hans.yml
    ```yml
  copyright:
    author: 原文作者
    link: 本文链接
    history: 更新历史
    cc: "署名-非商用-相同方式共享 4.0"
    notice: "转载请保留原文链接及作者。"
    license_title: 许可协议
    license_content: '本博客所有文章除特别声明外，均采用
      <a href="%s" rel="external nofollow" target="_blank">%s</a> 许可协议。转载请注明出处！'
    ```
    ```yaml
footer:
  powered: "Powered by %s "
  theme: Theme

    ```
2. 修改主题中layout/_macro/post-copyright.swig
    目的是为了添加copyright中的：
    ```yml
本文链接：
更新历史： Blame ,  .md Raw
许可协议：  "署名-非商用-相同方式共享 4.0" 转载请保留原文链接及作者。
    ```
    在yelee上觉得这种copyright很有意思，很符合开源精神。遂移植到next
    ```html
  <ul class="post-copyright">
    <li class="post-copyright-link">
      <strong>{{ __('post.copyright.link') + __('symbol.colon') }}</strong>
      <a href="{{ post.permalink }}" title="{{ post.title }}">{{ post.permalink }}</a>
      <span class="copy-path" data-clipboard-text=" 原文链接： {{ post.permalink }}　作 者 ：{{ post.copyright.author }}" title=" 点击复制文章链接 "><i class="fa fa-clipboard"></i></span>
      <script src="{{ theme.CDN.clipboard }}"> var clipboard = new Clipboard('.copy-path'); </script>
    </li>

    <li class="post-copyright-history">
      <strong>{{ __('post.copyright.history') + __('symbol.colon') }}</strong>
        <i class="fa fa-github"> </i><a href="https://github.com/lengthmin/blog-backup/blame/master/source/_posts/{{ post.date.format("YYYYMMDD") }}{{ post.slug }}.md" title="顺序查看markdown源文件各部分修改记录" target = "_blank">Blame</a>
                    , <i class="fa fa-file-text-o"></i> <a href="https://raw.githubusercontent.com/lengthmin/blog-backup/master/source/_posts/{{ post.date.format("YYYYMMDD") }}{{ post.slug }}.md" title="查看markdown源文件" target = "_blank">.md Raw</a>

    </li>
 <li class="post-copyright-license">
      <strong>{{ __('post.copyright.license_title') + __('symbol.colon') }} </strong>
 <i class="fa fa-creative-commons"></i> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/" title="CC BY-NC-SA 4.0 International" target = "_blank">"{{ __('post.copyright.cc') }}"</a> {{ __('post.copyright.notice') }}
    </li>
    </ul>
    ```
3. 修改主题中layout/_partials/footer.swig
添加coding的声明
    ```html
<div class="copyright">{#
#}{% set current = date(Date.now(), "YYYY") %}{#
#}&copy; {% if theme.footer.since and theme.footer.since != current %}{{ theme.footer.since }} &mdash; {% endif %}{#
#}<span itemprop="copyrightYear">{{ current }}</span>
  <span class="with-love">
    <i class="fa fa-{{ theme.footer.icon }}"></i>
  </span>
  <span class="author" itemprop="copyrightHolder">{{ theme.footer.copyright || config.author }}</span>

  {% if config.symbols_count_time.total_symbols %}
    <span class="post-meta-divider">|</span>
    <span class="post-meta-item-icon">
      <i class="fa fa-area-chart"></i>
    </span>
    {% if theme.symbols_count_time.item_text_total %}
      <span class="post-meta-item-text">{{ __('post.totalcount') }}&#58;</span>
    {% endif %}
    <span title="{{ __('post.totalcount') }}">{#
    #}{{ symbolsCountTotal(site) }}{#
  #}</span>
  {% endif %}

  {% if config.symbols_count_time.total_time %}
    <span class="post-meta-divider">|</span>
    <span class="post-meta-item-icon">
      <i class="fa fa-coffee"></i>
    </span>
    {% if theme.symbols_count_time.item_text_total %}
      <span class="post-meta-item-text">{{ __('post.totaltime') }}&#58;</span>
    {% endif %}
    <span title="{{ __('post.totaltime') }}">{#
    #}{{ symbolsTimeTotal(site, theme.symbols_count_time.awl, theme.symbols_count_time.wpm) }}{#
  #}</span>
  {% endif %}
</div>

<div class="powered-by">
  {{ __('footer.powered', '<a class="theme-link" href="https://hexo.io" style="font-weight: bold">Hexo</a>') }}
</div>

{% if theme.footer.powered and theme.footer.theme.enable %}
  <span class="post-meta-divider">|</span>
{% endif %}

<div class="theme-info">
  Hosted by <a href="https://pages.coding.me" style="font-weight: bold">Coding Pages</a>
</div>


<div>
    {{ __('footer.theme') }} -
  <a class="theme-link" href="https://github.com/iissnan/hexo-theme-next">
    NexT.{{ theme.scheme }}
  </a> by iissnan
</div>
    ```
    
  添加声明之后手机效果看起来不好，
  修改主题中/source/css/_schemes/Pisces/_layout.styl 第39-47行
  ```css
.main {
  clearfix();
  +tablet() {
    padding-bottom:  100px;
  }
  +mobile() {
    padding-bottom: $footer-height + 100px;
  }
}
  ```
4. 配置config
5. 

### 2016-12-06 在config中配置默认端口
```yaml
server:
  port: 8082
```
默认hexo s进入8082端口
### 2016-12-06 增加更新历史

### 2016-08-20 增加手机端的分类图标

把下面几行代码删掉就会显示了
/source/css/_partial/mobile.styl#L190
```css
.article-category::before{
    display: none;
}
.article-tag::before {
     display: none;
}
```

### 2016-07-06 yelee添加置顶博客

在博文的 `front-matter` 添加`top: 1`

### 2016-07-05 添加腾讯分析

用的主题是yelee，没有腾讯分析，自己加了一个。
在`主题目录`下操作。
在`_config.yml`中添加
```yml
tencent-analytics:
在冒号后面配置你的腾讯分析id，id就是获取到的代码的数字部分
```
在`layout/_partial/`中创建一个新的`tencent-analytics.ejs`文件,
加入如下代码
```ejs
<% if (theme.tencent_analytics){ %>
<script type="text/javascript" src="http://tajs.qq.com/stats?sId=<%= theme.tencent_analytics %>" charset="UTF-8"></script>

<script type="text/javascript">
    var _speedMark = new Date();
</script>
<% } %>
```
上面的代码包括了腾讯分析了。
在`layout/_partial/`中修改`head.ejs`：
```ejs
#随便找一行添加如下代码，让用户在打开网页时加载腾讯分析。
<%- partial('tencent-analytics') %>
```
然后在主题的`_config.yml`中输入你的腾讯分析id。
执行
```
hexo clean
hexo g -d
```
就ok了。

### 2016-05-26 启用yelee主题

目前在用的主题是yelee
hexo有很多主题，推荐一下next跟yelee，两个都是简洁风的主题，但是yelee比较和我口味。