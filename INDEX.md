# Steam 游戏入库清单与本体资源总索引

> 自动维护汇总 `manifests/` 目录下所有已归档的游戏入库清单、本体网盘与硬件流畅运行指南。  
> **基准配置参考**：`Intel Core i5-9600K / NVIDIA GeForce RTX 2060 6GB / 16GB RAM`（参考 doesitrun.com 跑分模型与实测调优）。  
> 最后更新：2026-10-05

---

## 资源与硬件运行概况一览表

| AppID | 游戏中文名 | 英文名 | 清单状态 | 推荐画质 (1080p) | 预估 FPS | 完整本体 (按需下载) | 目录详情 |
|---|---|---|---|---|---|---|---|
| `2001760` | 轮回之兽 | Beast of Reincarnation | ✅ 已下载 (495 B) | **1080p 中画质 (Medium) + DLSS 质量模式 (Quality)** | `50 ~ 60 FPS（平稳流畅）` | [33.4 GB 网盘](https://pan.quark.cn/s/747744f7330c) | [📂 详情](./manifests/2001760%20-%20Beast%20of%20Reincarnation%20-%20%E8%BD%AE%E5%9B%9E%E4%B9%8B%E5%85%BD/) |
| `2584270` | 致命躯壳2 | Mortal Shell II | ✅ 已下载 (305 B) | **1080p 中低混合画质 (Medium-Low) + DLSS 平衡模式 (Balanced)** | `45 ~ 55 FPS（战斗可玩，复杂光照场景有波动）` | [64.7 GB 网盘](https://pan.quark.cn/s/6644b5f49df5) | [📂 详情](./manifests/2584270%20-%20Mortal%20Shell%20II%20-%20%E8%87%B4%E5%91%BD%E8%BA%AF%E5%A3%B32/) |
| `2825860` | 沉没之城2 | The Sinking City 2 | ✅ 已下载 (365 B) | **1080p 中画质 (Medium) + DLSS 质量模式 (Quality)** | `48 ~ 58 FPS（雨水潮湿场景维持平稳，探索流畅）` | [47.2 GB 网盘](https://pan.quark.cn/s/d44225018952) | [📂 详情](./manifests/2825860%20-%20The%20Sinking%20City%202%20-%20%E6%B2%89%E6%B2%A1%E4%B9%8B%E5%9F%8E2/) |
| `3669870` | 控制：共振 | CONTROL Resonant | ✅ 已下载 (528 B) | **1080p 中高画质 (Medium-High) + DLSS 质量模式 (Quality)，光追关闭** | `55 ~ 65 FPS（关光追下丝滑满帧，物理爆破平稳）` | [100.1 GB 网盘](https://pan.quark.cn/s/f5f0bb3da079) | [📂 详情](./manifests/3669870%20-%20CONTROL%20Resonant%20-%20%E6%8E%A7%E5%88%B6%EF%BC%9A%E5%85%B1%E6%8C%AF/) |
| `3841510` | 真・三国无双２ with 猛将传 Remastered | DYNASTY WARRIORS 3 Complete Edition Remastered | ✅ 已下载 (231 B) | **1080p 极高画质 (Ultra) 或 2K (1440p) 高画质** | `60 FPS（稳定锁定满帧，千人同屏无掉帧）` | [34.7 GB 网盘](https://pan.quark.cn/s/553575497f0c) | [📂 详情](./manifests/3841510%20-%20DYNASTY%20WARRIORS%203%20Complete%20Edition%20Remastered%20-%20%E7%9C%9F%E3%83%BB%E4%B8%89%E5%9B%BD%E6%97%A0%E5%8F%8C%EF%BC%92%20with%20%E7%8C%9B%E5%B0%86%E4%BC%A0%20Remastered/) |

---

## ⚙️ 硬件配置文件规范 (.user_specs.json / user_specs.json)

本仓库基于硬件基准配置，结合 `doesitrun.com` 跑分模型与游戏引擎特性（UE5 / Northlight / RE Engine 等），为全库游戏提供定制化的**流畅运行画质推荐、预估帧率与避坑指南**。

### 1. 配置文件放置路径与读取优先级

工具按以下优先级自动识别硬件基准配置：

1. **仓库本地配置文件（最高优先）**：`steam-manifests/.user_specs.json` 或 `user_specs.json`
2. **系统环境变量**：`STEAM_SPECS_CPU`, `STEAM_SPECS_GPU`, `STEAM_SPECS_RAM`, `STEAM_SPECS_VRAM`, `STEAM_SPECS_RESOLUTION` 或 `STEAM_HARDWARE_SPECS`
3. **用户全局配置文件**：`~/.config/steam-manifests/user_specs.json`

> **隐私与 Git 隔离提示**：`.user_specs.json` 默认已加入 `.gitignore`，若无需公开个人硬件信息可直接放置该隐藏文件；如需作为公开基准，可直接提交 `user_specs.json`（仓库已提供模板 `user_specs.example.json`）。

### 2. 字段规范要求

| 字段名 | 类型 | 必需 | 说明与示例 |
|---|---|---|---|
| `cpu` | string | **必填** | 处理器型号，例如 `"Intel Core i5-9600K"` 或 `"AMD Ryzen 5 5600X"` |
| `gpu` | string | **必填** | 显卡完整型号及显存容量，例如 `"NVIDIA GeForce RTX 2060 6GB"` |
| `ram` | string | **必填** | 系统运行内存大小，例如 `"16GB"` 或 `"32GB"` |
| `vram` | string | 建议 | 独立显存容量，例如 `"6GB"`（用于大作与虚幻5防爆显存专项调优） |
| `resolution` | string | 建议 | 目标基准分辨率，默认为 `"1080p"`（可选 `"1080p"`、`"1440p"`、`"4K"` 等） |
| `notes` | string | 可选 | 硬件特殊属性或调优备忘，例如 `"6核6线程无超线程，Turing架构6G显存，支持DLSS 2，大作建议关光追控制纹理"` |

### 3. 配置示例模板 (`.user_specs.json`)

```json
{
  "cpu": "Intel Core i5-9600K",
  "gpu": "NVIDIA GeForce RTX 2060 6GB",
  "ram": "16GB",
  "vram": "6GB",
  "resolution": "1080p",
  "notes": "6核6线程无超线程，Turing架构6G显存，支持DLSS 2，大作建议关光追控制纹理"
}
```

### 4. 刷新索引与调优指南命令

修改配置文件或添加新游戏后，在仓库根目录执行以下命令，即可全自动依据最新配置刷新全库指南与总表：

```bash
node scripts/index_updater.js
```

---

## 各游戏详细概况与配置指南

### [2001760] 轮回之兽 (Beast of Reincarnation)

- **Steam AppID**：`2001760`
- **游戏归档目录**：[`manifests/2001760 - Beast of Reincarnation - 轮回之兽/`](./manifests/2001760%20-%20Beast%20of%20Reincarnation%20-%20%E8%BD%AE%E5%9B%9E%E4%B9%8B%E5%85%BD/)
- **📌 清单状态**：已下载 (495 B)，已就绪于目录中供 SteamTools / 入库工具读取
  - 备用清单网盘：https://pan.quark.cn/s/c79ed2d83a55
- **📦 完整本体 (用户手动下载)**：[下载链接](https://pan.quark.cn/s/747744f7330c) (体积: 33.4 GB，解压即玩)
- **🎮 本机硬件 (Intel Core i5-9600K / NVIDIA GeForce RTX 2060 6GB / 16GB RAM) 运行指南**：
  - **推荐画质**：1080p 中画质 (Medium) + DLSS 质量模式 (Quality)
  - **预估帧率**：50 ~ 60 FPS（平稳流畅）

### [2584270] 致命躯壳2 (Mortal Shell II)

- **Steam AppID**：`2584270`
- **游戏归档目录**：[`manifests/2584270 - Mortal Shell II - 致命躯壳2/`](./manifests/2584270%20-%20Mortal%20Shell%20II%20-%20%E8%87%B4%E5%91%BD%E8%BA%AF%E5%A3%B32/)
- **📌 清单状态**：已下载 (305 B)，已就绪于目录中供 SteamTools / 入库工具读取
  - 备用清单网盘：https://pan.quark.cn/s/e8386b2de337
- **📦 完整本体 (用户手动下载)**：[下载链接](https://pan.quark.cn/s/6644b5f49df5) (体积: 64.7 GB，解压即玩)
- **🎮 本机硬件 (Intel Core i5-9600K / NVIDIA GeForce RTX 2060 6GB / 16GB RAM) 运行指南**：
  - **推荐画质**：1080p 中低混合画质 (Medium-Low) + DLSS 平衡模式 (Balanced)
  - **预估帧率**：45 ~ 55 FPS（战斗可玩，复杂光照场景有波动）

### [2825860] 沉没之城2 (The Sinking City 2)

- **Steam AppID**：`2825860`
- **游戏归档目录**：[`manifests/2825860 - The Sinking City 2 - 沉没之城2/`](./manifests/2825860%20-%20The%20Sinking%20City%202%20-%20%E6%B2%89%E6%B2%A1%E4%B9%8B%E5%9F%8E2/)
- **📌 清单状态**：已下载 (365 B)，已就绪于目录中供 SteamTools / 入库工具读取
  - 备用清单网盘：https://pan.quark.cn/s/455d03edd9c7
- **📦 完整本体 (用户手动下载)**：[下载链接](https://pan.quark.cn/s/d44225018952) (体积: 47.2 GB，解压即玩)
- **🎮 本机硬件 (Intel Core i5-9600K / NVIDIA GeForce RTX 2060 6GB / 16GB RAM) 运行指南**：
  - **推荐画质**：1080p 中画质 (Medium) + DLSS 质量模式 (Quality)
  - **预估帧率**：48 ~ 58 FPS（雨水潮湿场景维持平稳，探索流畅）

### [3669870] 控制：共振 (CONTROL Resonant)

- **Steam AppID**：`3669870`
- **游戏归档目录**：[`manifests/3669870 - CONTROL Resonant - 控制：共振/`](./manifests/3669870%20-%20CONTROL%20Resonant%20-%20%E6%8E%A7%E5%88%B6%EF%BC%9A%E5%85%B1%E6%8C%AF/)
- **📌 清单状态**：已下载 (528 B)，已就绪于目录中供 SteamTools / 入库工具读取
  - 备用清单网盘：https://pan.quark.cn/s/4d0c7cddca97
- **📦 完整本体 (用户手动下载)**：[下载链接](https://pan.quark.cn/s/f5f0bb3da079) (体积: 100.1 GB，解压即玩)
- **🎮 本机硬件 (Intel Core i5-9600K / NVIDIA GeForce RTX 2060 6GB / 16GB RAM) 运行指南**：
  - **推荐画质**：1080p 中高画质 (Medium-High) + DLSS 质量模式 (Quality)，光追关闭
  - **预估帧率**：55 ~ 65 FPS（关光追下丝滑满帧，物理爆破平稳）

### [3841510] 真・三国无双２ with 猛将传 Remastered (DYNASTY WARRIORS 3 Complete Edition Remastered)

- **Steam AppID**：`3841510`
- **游戏归档目录**：[`manifests/3841510 - DYNASTY WARRIORS 3 Complete Edition Remastered - 真・三国无双２ with 猛将传 Remastered/`](./manifests/3841510%20-%20DYNASTY%20WARRIORS%203%20Complete%20Edition%20Remastered%20-%20%E7%9C%9F%E3%83%BB%E4%B8%89%E5%9B%BD%E6%97%A0%E5%8F%8C%EF%BC%92%20with%20%E7%8C%9B%E5%B0%86%E4%BC%A0%20Remastered/)
- **📌 清单状态**：已下载 (231 B)，已就绪于目录中供 SteamTools / 入库工具读取
  - 备用清单网盘：https://pan.quark.cn/s/5b108a194318
- **📦 完整本体 (用户手动下载)**：[下载链接](https://pan.quark.cn/s/553575497f0c) (体积: 34.7 GB，解压即玩)
- **🎮 本机硬件 (Intel Core i5-9600K / NVIDIA GeForce RTX 2060 6GB / 16GB RAM) 运行指南**：
  - **推荐画质**：1080p 极高画质 (Ultra) 或 2K (1440p) 高画质
  - **预估帧率**：60 FPS（稳定锁定满帧，千人同屏无掉帧）

