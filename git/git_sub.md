## 添加子模块，放入 doc/ 目录
git submodule add git@github.com:your-org/common-docs.git doc

## 修改并提交 common-docs 的内容(子模块的 Git 操作和普通仓库一样)
cd doc
git checkout -b xxx
git add .
git commit -m "你的提交信息"
git push origin xxx

## 上层仓库要单独提交引用更新,要不然母仓库感知不到doc的变更
cd ..
git status   # 会显示 doc 的指向变了(变成新的 commit 了)
git add doc  # 这里只是记录子模块指针的变化
git commit -m "Update common-docs submodule to latest commit"
git push origin your-branch
