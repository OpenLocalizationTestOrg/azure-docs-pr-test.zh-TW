<!-- A-series - compute-intensive instances, H-series -->

hello 大小 A8 A11 和 H 數列也是*大量計算執行個體*。 設計和適合需要大量計算執行這些大小的 hello 硬體和網路密集應用程式，包括高效能運算 (HPC) 叢集應用程式、 建模和模擬。 hello A8 A11 數列使用 Intel Xeon E5-2670 @ 2.6 GHZ 和 hello H 數列使用 Intel Xeon E5 2667 v3，3.2 GHz @。 

Azure H 系列虛擬機器是 hello 下一個產生高效能運算 Vm 旨在高階運算需求，例如屬於分子模型和計算流體動力學。 這些 8 到 16 vCPU Vm 之上 hello Intel Haswell E5 2667 V3 處理器技術將設為特色 DDR4 記憶體和 SSD 基底暫存儲存位置。 

此外 toohello 大量 CPU 能力 hello H 系列提供低延遲 RDMA 網路使用 FDR InfiniBand 和數個記憶體組態 toosupport 記憶體密集運算需求的不同選項。



## <a name="h-series"></a>H 系列

ACU：290 - 300

| 大小 | vCPU | 記憶體：GiB | 暫存儲存體 (SSD) GiB | 最大資料磁碟 | 最大磁碟輸送量︰IOPS | 最大 NIC |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16 x 500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32 x 500 |4 |
| Standard_H8m |8 |112 |1000 |16 |16 x 500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32 x 500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32 x 500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32 x 500 |4 |

*對於 MPI 應用程式，FDR InfiniBand 網路會啟用專用 RDMA 後端網路，以提供超低延遲和高頻寬。

<br>



## <a name="a-series---compute-intensive-instances"></a>A 系列 - 大量計算執行個體

ACU：225

| 大小 | vCPU | 記憶體：GiB | 暫存儲存體 (HDD)：GiB | 最大資料磁碟 | 最大資料磁碟輸送量︰IOPS | 最大 NIC|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16x500 |2 |
| Standard_A9* |16 |112 |382 |16 |16x500 |4 |
| Standard_A10 |8 |56 |382 |16 |16x500 |2  |
| Standard_A11 |16 |112 |382 |16 |16x500 |4 |

*對於 MPI 應用程式，FDR InfiniBand 網路會啟用專用 RDMA 後端網路，以提供超低延遲和高頻寬。

<br>



