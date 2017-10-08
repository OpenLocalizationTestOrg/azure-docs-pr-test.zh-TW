---
title: "aaaManage 堆疊 Azure 儲存體帳戶 |Microsoft 文件"
description: "了解 toofind，管理、 復原和回收堆疊 Azure 儲存體帳戶的方式"
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 350c92d6b5ce9b1582ede0256c4d3d23bdd94901
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a>在 Azure Stack 中管理儲存體帳戶
了解如何 toomanage 儲存體帳戶的 Azure 堆疊 toofind 復原，以及根據商務需求的儲存容量的回收。

## <a name="find"></a>尋找儲存體帳戶
hello hello 區域中的儲存體帳戶清單可以檢視由 Azure 堆疊中：

1. 在網際網路瀏覽器中，瀏覽至 https://adminportal.local.azurestack.external。
2. 登入 toohello 堆疊 Azure 系統管理入口網站為雲端操作員 （使用您在部署期間所提供的認證）
3. Hello 預設儀表板 – 上尋找 hello**區域管理**清單，然後按一下您想要 tooexplore hello 區域。 例如 **(local**)。
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. 選取**儲存體**從 hello**資源提供者**清單。
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. 現在，在 hello 儲存體資源提供者系統管理員 刀鋒視窗 – 向下捲動 hello**儲存體帳戶**索引標籤，然後按一下它。
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   hello 結果頁面是在該區域中的儲存體帳戶 hello 清單。
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

根據預設，hello 前 10 個帳戶會顯示。 您可以按一下 hello 更多選擇 toofetch**載入更多**hello hello 清單底端的連結。

或

如果您想要在特定的儲存體帳戶 – 您可以**篩選和 fetch hello 相關帳戶**只。


**toofilter 帳戶：**

1. 按一下**篩選**在 hello hello 刀鋒視窗最上方。
2. Hello 篩選刀鋒視窗中，它可讓您 toospecify**帳戶名稱**，**訂用帳戶 ID**或**狀態**toofine 微調 hello 清單的儲存體帳戶 toobe 顯示。 請適當地指定。
3. 按一下 [更新] 。 hello 清單應該據此重新整理。
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. tooreset hello 篩選： 按一下**篩選**、 清除選取項目和更新。

hello 搜尋 文字方塊中 （在 hello hello 儲存體帳戶清單刀鋒視窗頂端） 可讓您反白顯示 hello 帳戶清單中選取的 hello 文字。 Hello 完整名稱或識別碼無法輕鬆地使用時，這是在 hello 案例中非常有用。

您可以使用任意文字 toohelp 在這裡找到您感興趣的 hello 帳戶。

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a>查看帳戶詳細資料
一旦您找到您感興趣檢視的 hello 帳戶，您可以按一下 hello 特定帳戶 tooview 特定詳細資料。 新刀鋒視窗會開啟與 hello 帳戶詳細資料這類： hello hello 帳戶、 建立時間、 位置等等的類型。

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a>復原已刪除的帳戶
您可能需要 toorecover 的情況下已刪除的帳戶。

Azure 堆疊中沒有非常簡單的方式 toodo 的：

1. 瀏覽 toohello 儲存體帳戶清單。 如需詳細資訊，請參閱本主題中的[尋找儲存體帳戶](#find)。
2. Hello 清單中，找出該特定的帳戶。 您可能需要 toofilter。
3. 檢查 hello*狀態*的 hello 帳戶。 它應該指出 [已刪除]。
4. 按一下以開啟刀鋒視窗中的帳戶詳細資料 hello hello 帳戶。
5. 在這個刀鋒視窗中，找出 hello**復原**按鈕，然後按一下它。
6. 按一下**是**tooconfirm。
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. hello 正在復原現在*...處理稍候*是否有指出已順利完成。
   您也可以按一下上方的 hello 入口網站來檢視進度指示 hello hello"鈴鐺 」 圖示。
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   Hello 復原帳戶已順利同步處理，才能使用一次。

### <a name="some-gotchas"></a>注意事項
* 已刪除的帳戶顯示 [不再保留] 狀態。
  
  這表示已超過 hello 保留期限 hello 刪除帳戶，而且可能無法復原。
* 已刪除的帳戶不會顯示 hello 帳戶清單中。
  
  這可能表示 hello 刪除帳戶已經過記憶體回收。 在此情況下，便無法復原該帳戶。 請參閱本主題中的[回收容量](#reclaim)。

## <a name="set-hello-retention-period"></a>設定 hello 保留期限
hello 保留期限設定可讓雲端操作員 toospecify 天數 （介於 0 到 9999 天） 中的時間範圍期間的任何已刪除的帳戶可能已復原。 hello 預設保留週期設 too15 天。 設定 hello 值太"0"，則表示立即超出保留已刪除的帳戶，並標示為定期記憶體回收。

**toochange hello 保留期限：**

1. 在網際網路瀏覽器中，瀏覽至 https://adminportal.local.azurestack.external。
2. 登入 toohello 堆疊 Azure 系統管理入口網站為雲端操作員 （使用您在部署期間所提供的認證）
3. Hello 預設儀表板 – 上尋找 hello**區域管理**清單，然後按一下您想要 tooexplore – 例如 hello 區域**(本機**)。
4. 選取**儲存體**從 hello**資源提供者**清單。
5. 按一下**設定**在 hello 頂端 tooopen hello 設定刀鋒視窗。
6. 按一下**組態**然後編輯 hello 保留週期值。

   設定 hello 的天數，然後將它儲存。
   
   此值會立即生效，而且會設定您的整個區域。

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <a name="reclaim"></a>回收容量
其中一個 hello 副作用的保留期限是已刪除的帳戶將繼續 tooconsume 容量，直到它來自 hello 保留期限。 為雲端您可能需要方法 tooreclaim hello 的運算子會刪除帳戶空間，即使 hello 保留期間尚未過期。

您可以回收容量使用 hello 入口網站或 PowerShell。

**tooreclaim 容量使用 hello 入口網站：**
1. 瀏覽 toohello 儲存體帳戶 刀鋒視窗。 請參閱[尋找儲存體帳戶](#find)。
2. 按一下**回收空間**在 hello hello 刀鋒視窗最上方。
3. 閱讀 hello 訊息，然後按**確定**。

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. 等候 hello 入口網站中的成功通知，請參閱 hello 鈴鐺圖示。

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. 重新整理 hello 儲存體帳戶 頁面。 hello 刪除帳戶不再是 hello 清單中顯示，因為已遭清除。

您可以也使用 PowerShell tooexplicitly 覆寫 hello 保留期限，並立即回收容量。

**使用 PowerShell tooreclaim 容量：**   

1. 確認您已安裝並設定 Azure PowerShell。 否則，請使用下列指示的 hello: 
   * tooinstall hello 最新的 Azure PowerShell 版本並將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。
   如需有關 Azure Resource Manager Cmdlet 的詳細資訊，請參閱[搭配使用 Azure PowerShell 與 Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)
2. 執行下列 cmdlet 的 hello:

> [!NOTE]
> 如果您執行這個指令程式永久刪除 hello 帳戶和其內容。 無法復原。 使用時請務必小心。


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


如需詳細資訊，請參閱太[Azure 堆疊 powershell 文件。](https://msdn.microsoft.com/library/mt637964.aspx)
 

## <a name="migrate-a-container"></a>移轉容器
Toouneven 儲存體租用戶所使用，因為雲端運算子可能會發現其中一個或多基礎租用戶共用使用比其他更多空間。 如果發生這種情況，hello 雲端操作員可以手動移轉某些 blob 容器 tooanother 共用嘗試 toofree 出一些空間在 hello 注重重音的共用。 

您必須使用 PowerShell toomigrate 容器。
> [!NOTE]
>Blob 容器移轉不支援即時移轉，而且目前是離線作業。 在移轉期間，該容器中的 hello 基礎 blob 完成之前無法使用，而且是 「 離線 」 狀態。 

**使用 PowerShell toomigrate 容器：**

1. 確認您已安裝並設定 Azure PowerShell。 否則，請使用下列指示的 hello:
    * tooinstall hello 最新的 Azure PowerShell 版本並將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。 如需有關 Azure Resource Manager Cmdlet 的詳細資訊，請參閱[搭配使用 Azure PowerShell 與 Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)
2. 收到 hello 伺服陣列名稱： 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. 取得 hello 共用： 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. 取得指定的共用 hello 容器。 請注意，count 和 intent 都是選擇性參數：
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   接著，檢查 $containers：

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. 取得 hello 容器移轉 hello 最佳目的共用：

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    接著，檢查 $destinationshares：

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. 開始進行移轉的容器，請注意這是非同步實作，因此一個可以迴圈中使用 hello 傳回的作業識別碼的共用及追蹤 hello 狀態的所有容器。

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    接著，檢查 $jobId：

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. 檢查它的作業識別碼 hello 移轉作業的狀態。Hello 容器移轉完成時，MigrationStatus 設定太 「 已完成 」。

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. 您可以取消進行中的移轉工作。 這仍然是非同步作業，而且可以使用 $jobid 來追蹤：

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    您可以再次檢查 hello hello 移轉取消 5d; 狀態：

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  