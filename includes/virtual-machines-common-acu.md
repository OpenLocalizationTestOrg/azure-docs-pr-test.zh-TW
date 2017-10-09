



我們已經建立 hello Azure 計算單位 (ACU) tooprovide 的方式來計算 (CPU) 的效能比較跨 Azure Sku 的 hello 的概念。 這可協助您輕鬆地識別的 SKU 是最有可能 toosatisfy 效能需求。  ACU 目前是以「小型 (Standard_A1)」VM 為標準 (數值為 100)，而所有其他 SKU 則大致上代表該 SKU 在執行標準基準測試上可以快多少。 

> [!IMPORTANT]
> hello ACU 是只是指導方針。  您的工作負載的 hello 結果會有所不同。 
> 
> 

<br>

| SKU 系列 | ACU \ vCPU |
| --- | --- |
| [A0](../articles/virtual-machines/windows/sizes-general.md) |50 |
| [A1-A4](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A5-A7](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A1_v2-A8_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A2m_v2-A8m_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A8-A11](../articles/virtual-machines/windows/sizes-hpc.md) |225* |
| [D1-D14](../articles/virtual-machines/windows/sizes-general.md) |160 |
| [D1_v2-D15_v2](../articles/virtual-machines/windows/sizes-general.md) |210 - 250* |
| [DS1-DS14](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160 |
| [DS1_v2-DS15_v2](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |210-250* |
| [D_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [Ds_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [E_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [Es_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [F1-F16](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [F1s-F16s](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [G1-G5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [GS1-GS5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [H](../articles/virtual-machines/windows/sizes-hpc.md) |290 - 300* |
| [L4s-L32s](../articles/virtual-machines/windows/sizes-storage.md) |180 - 240* |
| [M](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) | 160-180** |

標記為 ACUs * 使用 Intel® 快速技術 tooincrease CPU 頻率，並提供效能提升。  hello hello boost 數量可以隨著 hello VM 大小、 工作負載，以及在 hello 上執行其他工作負載相同的主機。

**超執行緒。 
