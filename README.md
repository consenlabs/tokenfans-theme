### INSTALL

配置中心 - 定制 - 导入 - 从互联网 - 填入 https://github.com/consenlabs/tokenfans-theme


### 工具

- [discourse_theme](https://github.com/discourse/discourse_theme)


### 参考

[Developer’s guide to Discourse Themes](https://meta.discourse.org/t/developer-s-guide-to-discourse-themes/93648)

[Beginners Guide to Install Discourse on macOS for Development](https://meta.discourse.org/t/beginners-guide-to-install-discourse-on-macos-for-development/15772)

[Beginner’s Guide to Creating Discourse Plugins](https://meta.discourse.org/t/beginners-guide-to-creating-discourse-plugins-part-1/30515)

### Notes

- 帖子 lock 图标在 category-link 92 行


### 升级

因为修改的方式是，通过覆盖原来的代码来实现的，而目前所做的修改是修改一些逻辑和页面DOM（把源代码复制过来，修改一下），那么当discourse升级，而页面结构变动后，需要重新检查一下是否有新的DOM等，否则会出现bug。

### 启动 discourse

```
brew services start redis
brew services start postgresql
brew services start nginx
bundle exec rails server
```

### DB

清除数据库并新建
```
rake db:drop db:create db:migrate
```

[Create Admin Account from Console](https://meta.discourse.org/t/create-admin-account-from-console/17274)

### icon

[Introducing Font Awesome 5 and SVG icons](https://meta.discourse.org/t/introducing-font-awesome-5-and-svg-icons/101643)

###### 全局

现在，部分的 icon 是通过覆盖 `d-icon`方法实现的：
```js
registerUnbound("d-icon", function (id, params) {
  if (REPLACER[id]) {
    return new Handlebars.SafeString(`<img src="${REPLACER[id]}" class="svg-icon svg-icon-${id}" />`);
  }
  return new Handlebars.SafeString(renderIcon("string", id, params));
});
```
但这种方式会导致，用在 button 里的 icon 也会被覆盖，而 img 元素不方便修改 svg 的颜色，导致：如果替换的 icon 是灰色的，那么 icon 就会看不到（因为 button 统一是黑色 background）。

`lib/icon-library` 经验证没有被覆盖，那么在 js 中通过调用 `iconNode` 渲染的 icon 就无法被替换，只能针对所使用到的地方，去替换。

##### 局部

如果看到要改哪个 icon，就覆写哪个组件，这会导致要覆写的组件非常多，将来难以维护。

### i18n

部分 i18n 无法被覆盖，如 `topic.create`