# TaxaScope（KRIBB-KCTC 生物信息学工具包）

[![Version](https://img.shields.io/badge/version-1.0-green.svg)](https://github.com/pyx647/TaxaScope-KRIBB-KCTC)
[![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)](https://github.com/pyx647/TaxaScope-KRIBB-KCTC)
[![License](https://img.shields.io/badge/license-Academic%20Use-orange.svg)](LICENSE)

韩国生物科学与生物技术研究院（KRIBB）韩国典型培养物保藏中心（KCTC）

TaxaScope 是一款集成化、图形界面驱动的生物信息学工具包，专为 Windows 生态系统下的微生物基因组分析而设计。它将复杂的命令行工作流与友好的研究应用相结合，在单一桌面界面中整合了工作流配置、容器化执行、结果预览和可重现性报告等功能。

## 文档

维护文档集中在 `docs/` 目录中。

- [文档索引](docs/README.md)
- [TaxaScope 用户手册](docs/TaxaScope_User_Manual.md)
- [HTML 用户指南（英文/中文/韩文，纯文本工作流版本）](docs/TaxaScope_User_Guide.html)
- [安装指南](docs/Installation_Guide.md)
- [软件可用性](docs/Software_Availability.md)
- [工具可重现性](docs/Tool_Reproducibility.md)

用户手册是面向审阅者的主要文档，详细介绍了 TaxaScope 实际实现的桌面工作流：首次环境配置、工作目录选择、一键数据库下载、离线或在线容器镜像处理、NCBI 或本地输入准备、模块参数配置、批量执行、结果查看、输出目录结构、故障排除，以及 HTML/Markdown/JSON 可重现性报告。

## 主要功能

- **一键分析**：支持 Prokka、BUSCO、CheckM2、dbCAN、antiSMASH、PhyloPhlAn 和 ANI/AAI 的自动化工作流。
- **NCBI 数据获取**：使用 GCA/GCF 登录号批量检索基因组。
- **容器化执行**：工具在隔离的 Podman/Docker 兼容容器环境中运行。
- **离线镜像处理**：网络受限时，用户可导入或导出预打包的容器镜像。
- **批量工作流配置**：用户可将多个模块组合成顺序工作流。
- **结果查看**：可在图形界面中查看输出文件、图表、报告和进化树。
- **可重现性报告**：运行结束后可导出包含软件、数据库、参数、时间戳、输入和输出元数据的 HTML、Markdown 和 JSON 报告。

## 架构

TaxaScope 采用四层架构以支持稳定性和可重现性：

1. **表示层**：基于 CustomTkinter 的图形用户界面。
2. **编排层**：用于任务调度、参数处理和数据流的 Python 和 PowerShell 脚本。
3. **分析核心层**：容器化生物信息学工具和本地数据库。
4. **基础设施层**：搭载 WSL2 和 Podman/Docker 后端的 Windows 主机系统。

<img width="1916" height="1029" alt="图 1. TaxaScope 架构" src="https://github.com/user-attachments/assets/69093f22-e0cb-4a13-b01a-d653ad878088" />

图 1. TaxaScope 架构。系统采用四层模型运行：用户界面、编排引擎、分析核心和基础设施。表示层提供用于参数调整和结果可视化的图形界面。编排层负责任务调度和资源分配。分析核心层在隔离的容器环境中执行生物信息学工具。基础设施层处理 Windows、WSL2、Podman/Docker 和数据输入/输出。

## 内置工具

| 工具 | 功能 |
| :--- | :--- |
| Prokka | 快速基因组注释 |
| ANI/AAI | 分类身份与物种界定 |
| dbCAN3 | 碳水化合物活性酶鉴定 |
| antiSMASH | 生物合成基因簇分析 |
| CheckM2 | 基于机器学习的质量评估 |
| BUSCO | 基于谱系的完整性评估 |
| PhyloPhlAn | 全基因组系统发育 |
| Get Data | NCBI 基因组批量下载 |

## 图形界面工作流

TaxaScope 图形界面工作流操作步骤如下：

1. 打开 `TaxaScope.exe`；首次使用时，点击 `Env Setup` 并等待界面提示 `Env Ready`。
2. 点击 `Select Work Directory`，选择将包含输入文件、数据库、中间文件、输出结果和报告的项目文件夹。
3. 点击 `Download DBs` 以填充 `TaxaScope_Databases` 并写入数据库来源文件。
4. 通过 `Get Data` 使用 GCA/GCF 登录号添加输入数据，或将本地 FASTA/FA/FNA/FAA/GBK/GBFF 文件放置在工作目录中。
5. 在 `Genome Stats`、`Prokka`、`CheckM`、`BUSCO`、`dbCAN`、`antiSMASH`、`PhyloPhlAn` 和 `AAI/ANI` 中配置模块参数。
6. 打开 `Batch`，使用 `Data Acquisition (Optional)` 和 `Analysis Sequence Setup`，根据需要保持报告生成启用状态，然后点击 `DEPLOY COMPLETE WORKFLOW`。
7. 使用 `Runtime`、`Console`、`File Browser` 和 `Preview` 监控进度、排查日志、查看输出并审阅报告。

完整说明请参阅 [TaxaScope 用户手册](docs/TaxaScope_User_Manual.md)。

## 系统要求

| 组件 | 推荐配置 |
| :--- | :--- |
| 操作系统 | Windows 11 64 位 |
| 内存 | 64 GB |
| CPU | 16 核 x86-64 |
| 磁盘 | 200 GB 可用空间（SSD） |

> **注意：** 在对大型基因组数据集同时运行 CheckM2、BUSCO 和 PhyloPhlAn 等内存密集型模块时，强烈建议使用 64 GB 内存。对于超过 50 个基因组的数据集，内存低于 32 GB 的系统分析速度可能明显变慢或出现失败。

## 快速开始

1. 下载最新版 TaxaScope。
2. 运行 `TaxaScope.exe`。
3. 首次使用时点击 `Env Setup` 初始化执行环境。
4. 点击 `Select Work Directory` 选择项目文件夹，然后点击 `Download DBs`。
5. 阅读 [TaxaScope 用户手册](docs/TaxaScope_User_Manual.md) 获取完整的图形界面工作流教程、输出结构和可重现性报告文档。

## 发表与引用

如果您在研究中使用了 TaxaScope，请引用：

> Peng, Y., Jiang, Y., Lee, Y. J., Lee, J. H., Kim, C. Y., & Lee, J. (2026). TaxaScope: a container-native, visualization-centric workstation for genome-based bacterial taxonomy. *Frontiers in Microbiology*, 17, 1809734.

## 许可证

本软件仅供学术使用。请参阅 [LICENSE](LICENSE) 文件，了解使用限制和署名的完整详情。

KCTC 标志是 KRIBB 的注册商标，不在开源授权范围内。
