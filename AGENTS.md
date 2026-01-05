# AI Assistant Guide

> 本文档指导 AI 助手在此仓库进行功能开发时的 Git 工作流。

## 分支结构

```
main                 # 与上游保持同步，不直接修改
├── feat/xxx         # 功能分支（从 main 创建）
├── fix/xxx          # 修复分支（从 main 创建）
└── local-custom     # 个人定制分支，合并所需功能
```

### 分支关系时间线

```
时间线 →

main:           A ─── B ─── C ─────── D (上游更新)
                │           │         │
feat/feature-1: └── E ─ F   │         │
                        │   │         │
feat/feature-2:         │   └── G ─ H │
                        │           │ │
local-custom:   ────────M1──────────M2─M3──→
                     (merge F)  (merge H) (merge D)
```

- `main` 保持与上游同步
- 功能分支从 `main` 分叉，独立开发
- `local-custom` 通过合并收集所需功能

## 开发流程

### 1. 创建功能分支

```bash
git checkout main && git pull origin main
git checkout -b feat/my-feature
```

### 2. 开发并提交

```bash
git add . && git commit -m "feat: description"
git push -u origin feat/my-feature
```

### 3. 合并到 local-custom

```bash
git checkout local-custom
git merge feat/my-feature -m "merge: my feature"
git push origin local-custom
```

### 4. 同步上游更新

```bash
git checkout main && git pull origin main
git checkout local-custom && git merge main -m "merge: sync upstream"
```

## 分支命名

| 前缀 | 用途 |
|------|------|
| `feat/` | 新功能 |
| `fix/` | 修复 |
| `refactor/` | 重构 |

## 原则

- 功能分支从 `main` 创建，保持独立
- `local-custom` 只做合并，不直接开发
- 合并信息使用 `merge: 功能描述` 格式

