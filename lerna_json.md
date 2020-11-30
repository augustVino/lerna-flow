```json
{
  "packages": ["packages/*"],
  // 存储库的当前版本。
  "version": "1.1.0",
  // 用于指定用于运行命令的特定客户端（也可以基于每个命令来指定）。更改为"yarn"使用yarn运行所有命令。默认为“ npm”。
  "npmClient": "yarn",
  "publish": {
    "ignoreChanges": ["ignored-file", "*.md"],
    "message": "chore(release): publish"
  },
  "bootstrap": {
    // 将npm install在lerna bootstrap命令期间作为参数直接传递到的字符串数组
    "npmClientArgs": ["--no-lockfile"]
  },
  "command": {
    "init": {
      "exact": true
    }
  }
}
```
