# Tool Usage Notes

Tool signatures are provided automatically via function calling.
This file documents non-obvious constraints and usage patterns.

## exec — Safety Limits

- Commands have a configurable timeout (default 60s)
- Dangerous commands are blocked (rm -rf, format, dd, shutdown, etc.)
- Output is truncated at 10,000 characters
- `restrictToWorkspace` config can limit file access to the workspace

## glob — File Discovery

- Use `glob` to find files by pattern before falling back to shell commands
- Simple patterns like `*.py` match recursively by filename
- Use `entry_type="dirs"` when you need matching directories instead of files
- Use `head_limit` and `offset` to page through large result sets
- Prefer this over `exec` when you only need file paths

## grep — Content Search

- Use `grep` to search file contents inside the workspace
- Default behavior returns only matching file paths (`output_mode="files_with_matches"`)
- Supports optional `glob` filtering plus `context_before` / `context_after`
- Supports `type="py"`, `type="ts"`, `type="md"` and similar shorthand filters
- Use `fixed_strings=true` for literal keywords containing regex characters
- Use `output_mode="files_with_matches"` to get only matching file paths
- Use `output_mode="count"` to size a search before reading full matches
- Use `head_limit` and `offset` to page across results
- Prefer this over `exec` for code and history searches
- Binary or oversized files may be skipped to keep results readable

## cron — Scheduled Reminders

- Please refer to cron skill for usage.



# 工具使用说明
工具签名会通过函数调用自动提供。
这个文件记录的是一些不那么显而易见的约束和使用模式。

## exec —— 安全限制
- 命令有可配置的超时时间（默认 60 秒）
- 危险命令会被拦截（如 `rm -rf`、`format`、`dd`、`shutdown` 等）
- 输出会在 10,000 个字符处被截断
- `restrictToWorkspace` 配置可以将文件访问限制在工作区内

## glob —— 文件发现
- 先用 `glob` 按模式查找文件，再考虑退回到 shell 命令
- 像 `*.py` 这样的简单模式会按文件名递归匹配
- 如果你需要匹配目录而不是文件，使用 `entry_type="dirs"`
- 对于大量结果，可用 `head_limit` 和 `offset` 分页
- 当你只需要文件路径时，优先用它而不是 `exec`

## grep —— 内容搜索
- 使用 `grep` 在工作区内搜索文件内容
- 默认行为只返回匹配的文件路径（`output_mode="files_with_matches"`）
- 支持可选的 glob 过滤，以及 `context_before` / `context_after`
- 支持 `type="py"`、`type="ts"`、`type="md"` 这类简写过滤器
- 若要搜索包含正则特殊字符的字面量关键字，使用 `fixed_strings=true`
- 如果只想拿到匹配文件路径，使用 `output_mode="files_with_matches"`
- 如果想先估算搜索规模，再决定是否读取完整匹配内容，使用 `output_mode="count"`
- 对大量结果可用 `head_limit` 和 `offset` 分页
- 在代码和历史搜索场景下，优先用它而不是 `exec`
- 为了保证结果可读性，二进制文件或过大的文件可能会被跳过

## cron —— 定时提醒
用法请参考 cron skill。