---
title: "從自訂映像的 aaaProvision Azure Batch 集區 |Microsoft 文件"
description: "您可以建立自訂映像 tooprovision 從集區計算節點，其中包含 hello 軟體和您的應用程式所需的資料批次。 自訂映像可以有效率地 tooconfigure 計算節點 toorun 批次的工作負載。"
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>使用自訂映像 toocreate 虛擬機器的集區

當您在 Azure 批次中建立的虛擬機器的集區時，您會指定為 hello 集區中每個計算節點提供 hello 作業系統的虛擬機器 (VM) 映像。 使用 Azure Marketplace 映像，或提供您已備妥的自訂 VHD 映像，即可建立虛擬機器的集區。 當您提供的自訂映像時，您可以控制在每個運算節點會佈建的 hello 階段 hello 作業系統的設定方式。 自訂映像也可以包含應用程式和參考資料所提供的 hello 計算節點，因為它已佈建。

使用自訂映像可以節省時間在取得集區的計算節點準備 toorun 您批次的工作負載。 雖然您一律可以使用 Azure Marketplace 映像，並且在每個已佈建的計算節點上安裝軟體，但相較於使用自訂映像，這種方法可能比較沒有效率。 

某些原因 toouse 自訂映像已針對您的案例包括需要：

- **設定 hello 作業系統 (OS)** hello 作業系統的任何特殊組態可對 hello 自訂映像。 
- **安裝大型應用程式。** 相較於在佈建完成後，在每個計算節點上安裝應用程式，在自訂映像上安裝應用程式會更有效率。
- **複製大量資料。** 如果 hello 資料複製的 toohello 自訂映像，它只需要 toobe 複製一次，而不是 tooeach 計算節點，進而節省時間與頻寬。
- **Hello 安裝程序期間，重新啟動 hello VM。** 正在重新啟動 hello VM 可以是費時的程序，尤其是如果您的運算節點數目。

## <a name="prerequisites"></a>必要條件

- **批次建立的帳戶與 hello 使用者訂用帳戶集區配置模式。** toouse 自訂映像 tooprovision 虛擬機器集區，建立您的 Batch 帳戶以 hello 使用者訂用帳戶[集區配置模式](batch-api-basics.md#pool-allocation-mode)。 在此模式中，批次集區配置到 hello hello 帳戶所在的訂用帳戶。 請參閱 hello[帳戶](batch-api-basics.md#account)一節中[開發大規模的平行計算與批次的解決方案](batch-api-basics.md)如需設定 hello 集區配置模式下，當您建立批次帳戶資訊。

- **Azure 儲存體帳戶**。 您需要標準的一般用途的 Azure 儲存體帳戶中 hello toocreate 使用自訂映像的虛擬機器的集區，相同的訂用帳戶和地區。 如果您從 Azure VM 中建立自訂映像，您將會複製 hello 映像 toohello 儲存體帳戶 hello VM 之 OS 磁碟位於何處，而且您不需要 toocreate 個別儲存體帳戶。 
    
## <a name="prepare-a-custom-image"></a>準備自訂映像

tooprepare 用於批次的自訂映像，您必須一般化 Linux 或 Windows 的現有安裝。 將作業系統安裝一般化可移除機器專屬資訊。 hello 結果是可以安裝在其他電腦或 Vm 映像。  

> [!IMPORTANT]
> 批次目前不支援使用 Azure 受管理的映像 tooprovision 集區。 hello 自訂映像您使用的 tooprovision 集區必須儲存在 Azure 儲存體。 
>
> 當您準備自訂映像，請注意 hello 下列點：
> - 請確定該 hello 基本 OS 映像使用的 tooprovision 您批次集區並沒有任何預先安裝 Azure 擴充功能，例如 hello 自訂指令碼延伸模組。 如果 hello 映像包含預先安裝的擴充功能，則 Azure 可能會遇到部署 hello VM 的問題。
> - 請確定該 hello 基本 OS 映像您提供使用 hello 預設暫存磁碟機，如 hello 批次節點代理程式目前必須要有 hello 預設暫存磁碟機。
>
>

您可以使用任何現有已備妥的 Windows 或 Linux 映像作為自訂映像。 例如，如果您想 toouse 本機映像，則上傳 hello 映像 tooan Azure 儲存體帳戶中的 hello 相同訂用帳戶和區域，所以您批次帳戶使用[AzCopy](../storage/storage-use-azcopy.md)或另一個上傳工具。

您也可以從新的或現有的 Azure VM 準備自訂映像。 如果您要建立新的 VM，您可以使用 Azure Marketplace 映像做為 hello 基底映像自訂映像，然後加以自訂。 toocustomize hello 基底映像，建立 Azure VM，並加入您的應用程式或資料 tooit。 然後一般化 hello VM tooserve 與自訂映像，並將它儲存 tooAzure 儲存體。 

tooprepare 自訂映像從 Azure VM，請遵循下列步驟：

1. 從 Azure Marketplace 映像建立**未受管理的**的 Azure VM。 Azure Marketplace 包括 [Windows](../virtual-machines/windows/quick-create-portal.md) 和 [Linux](../virtual-machines/linux/quick-create-portal.md) 的映像。
    
    在步驟 3 中的 hello VM 建立程序，請確定您選取**否**如**存放裝置： 使用管理磁碟**選項。 也請記 hello VM 之 OS 磁碟，hello 儲存體帳戶名稱做為這個儲存體帳戶也，Azure 會在其中儲存自訂映像：

    ![建立未受管理的 VM 和附註 hello 儲存體帳戶名稱](media/batch-custom-images/vm-create-storage.png)
 
2. 完成建立您的 VM 的 hello 程序，並等候 toobe Azure 所配置。 以下是示範 hello hello 執行狀態中的 Azure 入口網站中的 VM 映像：

    ![從市集映像建立 VM](media/batch-custom-images/vm-status-running.png)

3. Hello VM 開始執行之後，連接 tooit 透過 （適用於 Windows) 的 RDP 或 SSH （適用於 Linux)。 安裝任何必要的軟體，或複製所需的資料，並再一般化 hello VM。 中所述步驟 hello[一般化 hello VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm)。 
   
4. 請依照下列步驟 hello 太[登入 tooAzure PowerShell](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell)。 tooinstall Azure PowerShell，請參閱[Azure PowerShell 概觀](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0)。 

5. 接下來，請依照下列步驟 hello 太[Deallocate hello VM 和集 hello 狀態 toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized)。 

    在 hello Azure 入口網站，請注意該 VM 解除配置的 hello:

    ![請確認 VM 解除配置該 hello](media/batch-custom-images/vm-status-deallocated.png)

6.  建立並儲存 hello VM 映像 tooAzure 儲存體使用 hello[儲存 AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) PowerShell cmdlet。 請依照下列所述的 hello 指示[建立 hello 圖像](../virtual-machines/windows/sa-copy-generalized.md#create-the-image)。
    
    hello VM 映像會儲存 toohello Azure 儲存體帳戶建立 hello VM 建立時，這個程序的步驟 1 所示。 hello 儲存 AzureRmVMImage cmdlet 會將儲存 hello 映像 toohello**系統**該儲存體帳戶中的容器。 hello`-DestinationContainername`參數名稱的虛擬目錄內 hello**系統**容器。 hello`-VHDNamePrefix`參數會指定 hello blob 名稱的前置詞。 此前置詞是預留的 toohello blob 名稱與連字號。 

    例如，假設您呼叫 Save AzureRmVMImage 以 hello 下列參數：  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    hello 產生的影像會儲存 toohello 位置和 blob 名稱，如下所示：

    ![系統容器中儲存 VHD 的位置](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Azure 未受管理的 VM 會針對不同用途建立數個儲存體帳戶。 如果您沒有記下 hello hello 儲存體容器名稱時 hello hello OS 磁碟 VM 已建立，然後尋找 hello 相關聯的儲存體帳戶包含 hello**系統**容器。 瀏覽 hello**系統**容器 toofind hello 自訂映像使用您指定的 hello 值 hello**儲存 AzureRmVMImage**命令。

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>建立集區從 hello 入口網站中的自訂映像

一旦您儲存自訂映像且知道它的位置之後，就可以從該映像建立 Batch 集區。 從 hello Azure 入口網站，請遵循這些步驟 toocreate 集區：

1. 瀏覽 tooyour hello Azure 入口網站中的批次帳戶。 此帳戶必須是在 hello 相同訂用帳戶和區域，所以 hello 儲存體帳戶包含 hello 自訂映像。 
2. 在 hello**設定**視窗上 hello 左，請選取 hello**集區**功能表項目。
3. 在 hello**集區**視窗中，選取 hello**新增**命令。
4. 在 hello**新增集區**視窗中，選取**自訂映像 (Linux/Windows)** hello 從**映像類型**下拉式清單。 hello 入口網站會顯示 hello**自訂映像**選擇器。 瀏覽 toohello 自訂映像所在的儲存體帳戶，然後選取 hello 從 hello 容器所需的 VHD。 
5. 選取正確的 hello **Sku/方案發行者/**針對您自訂的 VHD。
6. 指定 hello 剩餘需要設定，包括 hello**節點大小**，**目標專用的節點**，和**低優先權的節點**，以及所需的任何選擇性設定。

    例如，Microsoft Windows Server Datacenter 2016 自訂映像，hello**新增集區** 視窗隨即出現，如下所示：

    ![從自訂 Windows 映像新增集區](media/batch-custom-images/add-pool-custom-image.png)
  
toocheck 是否現有集區為基礎的自訂映像，請參閱 hello**作業系統**屬性中的 hello hello 資源摘要區段**集區**視窗。 如果從自訂映像已建立 hello 集區，它會設定太**自訂 VM 映像**。

集區相關聯的所有自訂 Vhd 會顯示在集區 hello**屬性**視窗。
 
## <a name="next-steps"></a>後續步驟

- 如需 Batch 的深入概觀，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md)。
- 如需建立 Batch 帳戶的資訊，請參閱[的 hello Azure 入口網站來建立批次帳戶](batch-account-create-portal.md)。
