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
v1.2.3                # 用于特定版本发布记录（可选）

## 3. 开发流程

### 开发新功能/策略：

```bash
# 创建分支
git checkout -b strategy/mean-reversion

# 正常开发,提交
git add .
git commit -m "add mean reversion strategy"

# 合并到 develop 做统一回测
git checkout develop
git merge strategy/mean-reversion
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
