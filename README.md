# 生信分析代码仓库模板

这是一个面向 **R / Python 生信分析** 的仓库层级，目标是：

- 代码与数据分离
- 分析流程可追踪、可复现
- 结果输出有固定位置，方便后续汇报与复盘

## 目录结构

```text
.
├── analysis/
│   ├── R/              # R 分析脚本（清洗、建模、可视化）
│   ├── python/         # Python 分析脚本
│   ├── notebooks/      # Jupyter/Rmd 探索性分析
│   ├── workflows/      # 流程脚本（如 Snakemake/Nextflow）
│   └── config/         # 参数配置（yaml/json/toml）
├── data/
│   ├── raw/            # 原始数据（只读，不直接修改）
│   ├── interim/        # 中间数据
│   ├── processed/      # 可直接用于统计/建模的数据
│   ├── external/       # 外部下载数据
│   └── metadata/       # 样本信息、注释表、字典
├── docs/               # 项目文档、说明
├── results/
│   ├── figures/        # 图
│   ├── tables/         # 表
│   └── reports/        # 报告（html/pdf/md）
├── scripts/            # 通用脚本（启动、同步、检查）
├── env/                # 环境文件（requirements.txt / environment.yml）
├── logs/               # 运行日志
└── tests/              # 测试代码
```

## 推荐工作约定

1. **原始数据只放 `data/raw/`，不改动原文件**。
2. 所有清洗后的数据放 `data/interim/` 或 `data/processed/`。
3. 可复现流程优先放在 `analysis/workflows/`。
4. 图表和最终产出统一放在 `results/`。
5. 运行前先固定环境依赖到 `env/`。

## 关于大数据文件（RDS/H5AD）

- 不建议将大体积二进制数据直接提交到 Git（仓库会迅速膨胀、版本管理效率变差）。
- 建议方案：
  - 小文件（例如 < 50MB）：可临时放仓库，但长期仍建议迁移。
  - 大文件：使用对象存储（S3/OSS/GCS）或数据盘路径，并在仓库中仅保存下载/同步脚本与数据清单。
  - 若确实要跟踪大文件版本，可考虑 Git LFS（仍需注意存储/带宽成本）。

## 下一步你可以做的事

- 把你现在的 R/Python 脚本放入 `analysis/R` 或 `analysis/python`。
- 提供一个最小分析任务（输入、脚本、预期输出），我可以继续帮你补齐一键运行流程。
