
hello NC 和 NV 大小也是啟用 GPU 的執行個體。 這些是包含 NVIDIA GPU 卡並已針對不同情況和使用案例進行最佳化的特製化虛擬機器。 hello NV 大小會最佳化，並針對遠端的視覺效果、 資料流、 遊戲、 編碼和利用架構，例如 OpenGL 和 DirectX 的 VDI 案例所設計。 hello NC 大小更適合需要大量計算和網路密集應用程式和演算法，包括基礎 CUDA 和 OpenCL 應用程式和模擬。 


hello NV 執行個體由 NVIDIA 的 Tesla M60 GPU 卡和 NVIDIA 方格桌面加速應用程式和虛擬桌面客戶所在位置，可以 toovisualize 其資料或模擬。 使用者會無法 toovisualize hello NV 執行個體 tooget 上層的圖形功能其圖形密集工作流程並另外執行單精確度和等工作負載的編碼方式呈現。 hello Tesla M60 是雙重 GPU 設計，含有 too36 資料流的 1080p H.264 向上傳遞 4096 CUDA 核心。 

NVIDIA 的 Tesla K80 卡供電 hello NC 執行個體。 使用者現在可以藉由將 CUDA 用於能源探勘應用程式、當機模擬、光線追蹤轉譯、深入學習等等，更快速地處理資料。 hello Tesla K80 提供雙重 GPU 設計，too2.91 Teraflops 的雙精確度和向上 too8.93 的單精確度效能 Teraflops 4992 CUDA 核心。

## <a name="nv-instances"></a>NV 執行個體

| 大小 | vCPU | 記憶體：GiB | 暫存儲存體 (SSD) GiB | GPU | 資料磁碟數目上限 |
| --- | --- | --- | --- | --- | --- |
| Standard_NV6 |6 |56 |380 | 1 | 8 |
| Standard_NV12 |12 |112 |680 | 2 | 16 |
| Standard_NV24 |24 |224 |1440 | 4 | 32 |

1 GPU = 1/2 M60 卡。

## <a name="nc-instances"></a>NC 執行個體

| 大小 | vCPU | 記憶體：GiB | 暫存儲存體 (SSD) GiB | GPU | 資料磁碟數目上限 |
| --- | --- | --- | --- | --- | --- |
| Standard_NC6 |6 |56 | 380 | 1 | 8 |
| Standard_NC12 |12 |112 | 680 | 2 | 16 |
| Standard_NC24 |24 |224 | 1440 | 4 | 32 |
| Standard_NC24r* |24 |224 | 1440 | 4 | 32 |

1 GPU = 1/2 K80 卡。

*支援 RDMA


