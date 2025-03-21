# cp 命令：最后一个参数是否为目录的影响

## 场景 1：最后一个参数是目录

命令：`cp file1 file2 Dir`

效果：

- `file1` 和 `file2` 都被复制到 `Dir` 目录中
- 结果：`Dir/file1` 和 `Dir/file2`

## 场景 2：最后一个参数不是目录

命令：`cp file1 file2 destination`

效果：

- 如果 `file1` 存在，它的内容被复制到 `destination`
- `file2` 被忽略
- 结果：创建或覆盖名为 `destination` 的文件，内容与 `file1` 相同

## 场景 3：只有两个参数

命令：`cp source destination`

效果：

- 如果 `destination` 是目录：创建 `destination/source`
- 如果 `destination` 不是目录：创建或覆盖 `destination` 文件，内容与 `source` 相同

## 注意事项：

- 当有多个源文件时，最后一个参数必须是目录
- 如果最后一个参数不是目录，cp 只会处理第一个源文件
- 使用 `cp -r` 可以递归复制目录及其内容
