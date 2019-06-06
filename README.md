### INSTALL

配置中心 - 定制 - 导入 - 从互联网 - 填入 https://github.com/consenlabs/tokenfans-theme


### 工具

- [discourse_theme](https://github.com/discourse/discourse_theme)


### 参考

[Developer’s guide to Discourse Themes](https://meta.discourse.org/t/developer-s-guide-to-discourse-themes/93648)

[Beginners Guide to Install Discourse on macOS for Development](https://meta.discourse.org/t/beginners-guide-to-install-discourse-on-macos-for-development/15772)

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
