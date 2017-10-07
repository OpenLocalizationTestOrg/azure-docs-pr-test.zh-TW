---
title: "aaaUse hello Azure 批次轉譯服務 toorender hello 定域機組中的 |Microsoft 文件"
description: "Azure 虛擬機器上的轉譯作業直接由 Maya 提供且按使用次數付費。"
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Hello 轉譯批次服務快速入門

hello Azure 批次轉譯服務提供了雲端規模支付每次使用為基礎的轉譯能力。 hello 轉譯批次服務會處理工作排程和排入佇列、 管理失敗重試次數，以及適用於您的轉譯作業的自動調整。 hello 轉譯批次服務支援 Autodesk 馬雅 3ds Max 和 Arnold，即將推出的其他應用程式的支援。 hello 馬雅 2017年外掛程式的批次可輕鬆 toostart 轉譯作業在 Azure 上直接從您的桌面。 

## <a name="supported-applications"></a>支援的應用程式

hello 轉譯批次服務目前支援下列應用程式的 hello:

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>必要條件

toouse hello 轉譯批次服務，您需要：

- [Azure 帳戶](https://azure.microsoft.com/free/)。 
- **Azure Batch 帳戶**。 如需 hello Azure 入口網站中建立批次帳戶的指引，請參閱[的 hello Azure 入口網站來建立批次帳戶](batch-account-create-portal.md)。
- **Azure 儲存體帳戶**。 Azure 儲存體中儲存 hello 資產用於轉譯工作。 當您設定 Batch 帳戶時，可以自動建立儲存體帳戶。 您也可以使用現有的儲存體帳戶。 toolearn 進一步了解儲存體帳戶，請參閱[toocreate，如何管理或刪除 hello Azure 入口網站的儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-create-storage-account)。

toouse hello 批次馬雅外掛程式，必須：

- **Maya 2017**
- **Arnold for Maya**

您也可以使用 hello [Azure 入口網站](https://portal.azure.com)toocreate 集區與馬雅 3ds 預先設定的虛擬機器的最大值和 Arnold。 您可以使用 hello 入口 toomonitor 作業並下載應用程式記錄檔，並從遠端連線使用 RDP 或 SSH tooindividual Vm 診斷失敗的工作。

## <a name="basic-batch-concepts"></a>基本 Batch 概念

在您開始使用 hello 轉譯批次服務之前，很有幫助 toobe 熟悉幾個批次概念，包括計算節點、 集區和工作。 Azure 批次的相關一般情況下，請參閱的 toolearn[與批次中執行本質平行的工作負載](batch-technical-overview.md)。

### <a name="pools"></a>集區

Batch 是一項平台服務，用於在**計算節點**的**集區**上執行計算密集工作 (例如轉譯)。 集區中的每個計算節點不是執行 Linux 就是執行 Windows 的 Azure 虛擬機器 (VM)。 

如需有關批次集區和計算節點的詳細資訊，請參閱 hello[集區](batch-api-basics.md#pool)和[計算節點](batch-api-basics.md#compute-node)中[開發大規模的平行計算與批次的解決方案](batch-api-basics.md)。

### <a name="jobs"></a>工作

批次**作業**是 hello 執行的工作集合中的計算節點集區。 當您提交轉譯作業時，批次將 hello 工作分割成多個工作，並將散發 hello 工作 toohello hello 集區 toorun 中的計算節點。

如需有關批次作業的詳細資訊，請參閱 hello[作業](batch-api-basics.md#job)一節中[開發大規模的平行計算與批次的解決方案](batch-api-basics.md)。

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>使用 hello plug-in for 馬雅 toosubmit 轉譯作業的批次

以 hello 馬雅外掛程式的批次，您可以提交作業 toohello 直接從馬雅轉譯批次服務。 hello 下列各節說明如何 tooconfigure hello 從 hello 外掛程式的工作，並提交。 

### <a name="load-hello-batch-plug-in-in-maya"></a>載入 hello 批次中馬雅外掛程式

hello 外掛程式的批次並用於[GitHub](https://github.com/Azure/azure-batch-maya/releases)。 解壓縮您選擇的 hello 封存 tooa 目錄。 您可以直接從 hello 載入外掛程式 hello *azure_batch_maya*目錄。

tooload hello 馬雅外掛程式：

1. 執行 Maya。
2. 開啟 [視窗] > [設定/喜好設定] > [外掛程式管理員]。
3. 按一下 [瀏覽] 。
4. 瀏覽 tooand 選取*azure_batch_maya/plug-in/AzureBatch.py*。

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>驗證存取 tooyour 批次和儲存體帳戶

toouse hello 外掛程式，您必須使用您的 Azure 批次和 Azure 儲存體帳戶金鑰 tooauthenticate。 tooretrieve 儲存帳戶金鑰：

1. 顯示 hello 馬雅外掛程式和選取 hello **Config**  索引標籤。
2. 瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。
3. 選取**批次帳戶**hello 左側功能表。 如有必要，按一下 [更多服務]並依照 [批次] 篩選。
4. Hello 清單中，找出所需的 hello Batch 帳戶。
5. 選取 hello**金鑰**功能表項目 toodisplay 您的帳戶名稱、 帳戶 URL 和存取金鑰：
    - Hello 批次帳戶 URL 貼入 hello**服務**hello 外掛程式的批次中的欄位。
    - 貼上的 hello 帳戶名稱貼入 hello**批次帳戶**欄位。
    - 貼上的 hello 主要帳戶金鑰貼入 hello**批次金鑰**欄位。
7. 從 hello 左側功能表中選取儲存體帳戶。 如有必要，按一下 [更多服務]並依照 [儲存體] 篩選。
8. Hello 清單中，找出 hello 需要儲存體帳戶。
9. 選取 hello**便捷鍵**功能表項目 toodisplay hello 儲存體帳戶名稱和金鑰。
    - 貼上的 hello 儲存體帳戶名稱貼入 hello**儲存體帳戶**hello 外掛程式的批次中的欄位。
    - 貼上的 hello 主要帳戶金鑰貼入 hello**儲存體金鑰**欄位。
10. 按一下**驗證**hello 外掛程式的 tooensure 可以存取這兩個帳戶。

一旦您已順利通過驗證，hello 外掛程式設定可太 hello 狀態欄位**驗證**: 

![驗證 Batch 和儲存體帳戶](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>設定轉譯作業的集區

您已驗證 Batch 和儲存體帳戶之後，請針對您的轉譯作業設定集區。 hello 外掛程式會將儲存您的工作階段之間的選擇。 設定慣用的組態之後, 您不需要 toomodify 它除非它會變更。

hello 下列各節逐步引導您完成 hello 可用的選項，用於 hello**送出** 索引標籤：

#### <a name="specify-a-new-or-existing-pool"></a>指定新的或現有集區

由 toorun hello render 作業，選取 hello 集 toospecify**送出** 索引標籤。此索引標籤會提供建立集區或選取現有集區的選項：

- 您可以**自動佈建這項作業的集區**(hello 預設選項)。 當您選擇此選項時，批次建立 hello 集區專用的 hello 目前的工作，並會自動刪除 hello 集區時 hello 轉譯工作已完成。 當您有單一的轉譯作業 toocomplete 時，這個選項最適合。
- 您可以**重複使用現有的永續性集區**。 如果您有現有的集區處於閒置狀態時，您可以指定該集區執行 hello render 作業從 hello 下拉式清單中選取它。 重複使用現有的持續性資料庫可節省 hello 所需時間 tooprovision hello 集區。  
- 您可以**建立新的永續性集區**。 選擇此選項會建立新的集區執行 hello 作業。 它不會刪除 hello 集區 hello 工作完成時，以便您可以在未來作業重複使用。 當您有連續需要 toorun 轉譯作業時，請選取此選項。 在後續的工作，您可以選取**重複使用現有的持續性集區**toouse hello hello 第一份工作所建立的永續性集區。

![指定集區、OS 映像、VM 大小和授權](./media/batch-rendering-service/submit.png)

如需有關如何產生費用 Azure Vm 的詳細資訊，請參閱 hello [Linux 價格常見問題集](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq)和[Windows 價格常見問題集](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq)。

#### <a name="specify-hello-os-image-tooprovision"></a>指定 hello OS 映像 tooprovision

您可以指定在 hello 的 hello 集區中的 hello 類型的作業系統映像 toouse tooprovision 運算節點**Env** (Environment) 索引標籤。批次目前支援下列轉譯作業的映像選項 hello:

|作業系統  |映像  |
|---------|---------|
|Linux     |Batch CentOS 預覽 |
|Windows     |Batch Windows 預覽 |

#### <a name="choose-a-vm-size"></a>選擇 VM 大小

您可以指定 hello VM 大小上 hello **Env**  索引標籤。如需可用 VM 大小的詳細資訊，請參閱 [Azure 中的 Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes)和 [Azure 中的 Windows VM 大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)。 

![Hello Env 索引標籤上指定 hello VM OS 映像和大小](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>指定授權選項

您可以指定要在 hello toouse hello 授權**Env**  索引標籤。選項包括：

- **Maya**，預設會啟用。
- **Arnold**，如果 Arnold 馬雅中的 hello 作用中的轉譯引擎偵測到啟用的。

 如果您想 toorender 使用自己的授權，您可以藉由新增 hello 適當的環境變數 toohello 資料表設定您授權的結束點。 如果您這樣做，會確定 toodeselect hello 預設授權選項。

> [!IMPORTANT]
> 您所要支付 hello 授權的使用時 Vm 會 hello 集區中執行，即使 hello Vm 不目前正在使用的轉譯。 tooavoid 額外費用，瀏覽 toohello**集區**索引標籤，然後調整大小 hello 集區 too0 節點直到您準備好 toorun 其他轉譯工作。 
>
>

#### <a name="manage-persistent-pools"></a>管理永續性集區

您可以管理現有的持續性集區上 hello**集區** 索引標籤。從 hello 清單中選取集區會顯示 hello hello 集區的目前狀態。

從 hello**集區**索引標籤上，您也可以刪除 hello 集區，並調整 hello hello 集區中的 Vm 數目。 您可以調整支出成本之間的工作負載集區 too0 節點 tooavoid。

![檢視、調整大小和刪除集區](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>設定轉譯作業以便提交

一旦您已經指定要執行 hello render 作業 hello 集區的 hello 參數，設定 hello 工作本身。 

#### <a name="specify-scene-parameters"></a>指定場景參數

hello 外掛程式的批次中馬雅偵測到您目前使用的轉譯引擎，並顯示 hello 適當呈現 hello 上的設定**送出** 索引標籤。這些設定包括 hello 開始框架、 結束框架、 輸出前置詞和框架的步驟。 您可以在 hello 外掛程式中指定不同的設定，以覆寫 hello 場景檔案轉譯設定。 變更 toohello 外掛程式設定不保存後 toohello 場景檔案轉譯設定，因此您可以變更工作的工作為基礎而不需要 tooreupload hello 場景檔案。

hello 外掛程式會警告您如果 hello 呈現您選取在馬雅引擎不支援。

如果開啟 hello 外掛程式時，您就會載入新的場景，按一下 hello**重新整理**按鈕 toomake 確定 hello 設定會更新。

#### <a name="resolve-asset-paths"></a>解析資產路徑

當您載入 hello 外掛程式時，它會掃描 hello 場景檔案的任何外部檔案參考。 這些參考會顯示在 [hello**資產**] 索引標籤。如果無法解析參考的路徑，hello 外掛程式嘗試 toolocate hello 檔案，在少數的預設位置，包括：

- hello hello 場景檔案位置 
- hello 目前專案的_sourceimages_目錄
- hello 目前工作目錄。 

如果 hello 資產仍然找不到，它會列出警告圖示：

![遺失的資產會顯示警告圖示](./media/batch-rendering-service/missing_assets.png)

如果您知道 hello 的無法解析的檔案參考的位置，您可以按一下 hello 警告圖示 toobe 提示 tooadd 搜尋路徑。 hello 然後外掛程式會使用此搜尋路徑 tooattempt tooresolve 任何遺失的資產。 您可以新增任意數目的其他搜尋路徑。

解析參考時，它會以綠燈圖示列示：

![解析的資產會顯示綠燈圖示](./media/batch-rendering-service/found_assets.png)

如果您場景需要其他檔案該外掛程式的 hello 未偵測到，您可以加入其他檔案或目錄。 使用 hello**加入檔案**和**新增目錄**按鈕。 如果開啟 hello 外掛程式時，您就會載入新的場景，是確定 tooclick**重新整理**tooupdate hello 場景的參考。

#### <a name="upload-assets-tooan-asset-project"></a>上傳資產 tooan 資產專案

當您提交 render 作業 hello 所參考的檔案顯示在 [hello**資產**] 索引標籤會自動上傳的 tooAzure 為資產專案的儲存體。 您也可以上傳 hello 與轉譯作業無關的資產檔案使用 hello**上傳**按鈕 hello**資產** 索引標籤 hello 資產專案的名稱指定在 hello**專案**欄位，預設為 hello 目前馬雅專案之後。 如果資產檔案上傳時，會保留 hello 本機檔案結構。 

一旦上傳，資產即可由任意數量的轉譯作業參考。 所有上傳的資產是可用 tooany 作業參考 hello 資產的專案，不論是否包含在 hello 場景。 toochange hello 資產專案參考的下一個工作，變更 hello 名稱在 hello**專案**欄位 hello**資產** 索引標籤。如果您想從上傳 tooexclude 的參照的檔案時，取消選取這些電腦使用 hello 清單旁邊的綠色 hello 按鈕。

#### <a name="submit-and-monitor-hello-render-job"></a>提交和監視 hello 轉譯作業

Hello 呈現工作設定在 hello 外掛程式之後，按一下 hello**提交作業**按鈕 hello**送出**toosubmit hello 作業 tooBatch 索引標籤上：

![送出 hello render 作業](./media/batch-rendering-service/submit_job.png)

您可以監視正在從 hello 進行作業**作業**hello 外掛程式 索引標籤。 Hello 清單 toodisplay hello 目前作業的狀態 hello 從選取的作業。 您也可以使用此索引標籤 toocancel 和刪除作業，以及 toodownload hello 輸出和呈現記錄檔。 

toodownload 輸出修改 hello**輸出**欄位 tooset hello 所需的目的地目錄。 按一下 hello 齒輪圖示 toostart 監看 hello 作業並下載輸出進展的背景處理序： 

![檢視作業狀態並下載輸出](./media/batch-rendering-service/jobs.png)

您可以關閉馬雅而不會中斷 hello 下載程序。

## <a name="next-steps"></a>後續步驟

toolearn 進一步了解批次，請參閱[與批次中執行本質平行的工作負載](batch-technical-overview.md)。
