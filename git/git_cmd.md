| 操作                | 命令 |
|---------------------|------|
| 克隆包含子模块      | `git clone --recurse-submodules your_repo_url` |
| 初始化子模块        | `git submodule update --init --recursive` |
| 更新子模块          | `git submodule update --remote --merge` |
| 合并分支            | `git checkout develop && git merge strategy/xxx` |
| 推送主分支和标签    | `git push origin main --tags` |
| 回滚到某个发布版本  | `git checkout tags/prod-2025-07-04` |