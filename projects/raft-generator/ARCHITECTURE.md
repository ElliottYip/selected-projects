# RAFT Generator · 架构

以 Next.js 工作台组织创作入口，服务端负责鉴权、模型请求与生成任务持久化。

```mermaid
flowchart LR
 A[图片 / 视频 / 数字人工作台] --> B[Next.js API 路由]
 B --> C[鉴权与参数校验]
 C --> D[模型网关与 Provider Adapter]
 D --> E[模型服务]
 B --> F[Supabase Auth / Storage / 数据库]
 G[任务轮询] --> D
 G --> F
 F --> H[素材工作区与生成记录]
```

## 源码目录

| 路径 | 职责 |
|---|---|
| `src/app/` | 页面与服务端 API |
| `src/components/` | 创作、项目、数字人与工作区组件 |
| `src/lib/` | 数据访问、模型客户端、Provider 适配和环境工具 |
| `src/data/` | 静态内容与灵感条目 |
| `supabase/migrations/` | 数据库迁移 |
| `scripts/` | 检查与维护工具 |
| `public/` | 产品静态资源 |

## 关键设计

长任务需要清楚的提交、等待、失败和结果保存状态。模型参数与限制同时影响界面选项和服务端校验；素材管理承担结果复用，账号体系承接权限与用量。

这张图概括产品主要模块及其关系。

[返回项目](README.md)
