## 1. 分支结构说明

| 分支名         | 用途说明 |
|----------------|----------|
| `main`         | 稳定的生产环境代码(实盘运行) |
| `develop`      | 用于功能集成、回测和测试验证 |
| `feature/xxx`  | 开发新功能，如风控模块、行情接口等 |
| `strategy/xxx` | 开发新策略，便于回测与迭代 |
| `infra/xxx`    | 底层基础设施相关改动，如撮合系统、数据库适配等 |
| `hotfix/xxx`   | 用于修复生产环境中的紧急 bug |


## 2. 命名规范

### 分支命名：
feature/data-source-ctp
strategy/mean-reversion-alpha
infra/redis-migration
hotfix/data-latency

### 标签命名：
prod-2025-07-04       # 某次实盘上线版本
backtest-alpha001     # 某次回测策略快照
v1.2.3                # 用于特定版本发布记录(可选)

## 3. 开发流程

### 开发新功能/策略：

```bash
# 创建分支
git checkout -b feature/observe

# 正常开发,提交
git add .
git commit -m "add mean reversion strategy"


#git merge 操作步骤(保守安全派,多人协作、需要保留真实历史)

# 切换到 dev 分支
git checkout dev
# 拉取远程最新的 dev
git pull origin dev
# 合并 feature 分支(会生成一个 merge commit)
git merge --squash feature/observe
# 推送 dev
git push origin dev

#git rebase 操作步骤(整洁线性派)

#查看有多少提交是相对于 dev 的
git log dev..HEAD --oneline

# 确保在 feature 分支
git checkout feature/observe

# 拉取并切回最新 dev
git fetch origin
git checkout dev
git pull origin dev
git checkout feature/observe

# 执行 rebase
git rebase dev

# 修改冲突文件
git add <冲突文件>
git rebase --continue

#开始交互式 rebase 并 squash 提交
git rebase -i dev
git push origin feature/observe --force

#编辑最终的提交信息
# 删除远程分支
git push origin --delete feature/observe
# 删除本地分支
git branch -d feature/observe
```


## 4. 发布流程

### 代码上线实盘：

```bash
# 确保 develop 稳定可上线
git checkout main
git merge develop

# 打标签记录上线
git tag -a prod-2025-07-04 -m "上线均值回复策略+风控模块改进"

# 推送主分支和标签
git push origin main
git push origin prod-2025-07-04
```

---

## 5. 标签 (Tag) 使用

### 标记实盘发布版本：

```bash
git tag -a prod-2025-07-04 -m "上线策略X，优化撮合模块"
```

### 标记策略回测结果：

```bash
git tag backtest-strategy-v1
```

### 查看和删除标签：

```bash
git tag                   # 查看所有标签
git tag -d tag-name       # 删除本地标签
git push origin :refs/tags/tag-name  # 删除远程标签
```

## 📎 建议事项

- 所有实盘上线 **必须打标签**；
- 策略开发尽量使用独立分支，不直接在 `develop` 操作；
- 每次回测结果要记录策略参数、数据版本、标签快照；
- 可结合 CI/CD 系统（如 GitLab Runner）自动回测并生成报告。
