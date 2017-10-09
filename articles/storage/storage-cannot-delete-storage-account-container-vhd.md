---
title: "在傳統的部署中刪除 Azure 儲存體帳戶、 容器或 Vhd aaaTroubleshoot |Microsoft 文件"
description: "針對在傳統部署中刪除 Azure 儲存體帳戶、容器或 VHD 進行疑難排解"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>針對在傳統部署中刪除 Azure 儲存體帳戶、容器或 VHD 進行疑難排解
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

當您嘗試在 hello toodelete hello Azure 儲存體帳戶、 容器或 VHD 時，您可能會收到錯誤[Azure 入口網站](https://portal.azure.com/)或 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)。 hello 問題可能被因下列情況下的 hello:

* 當您刪除 VM 時，hello 磁碟和 VHD 不會自動刪除。 可能 hello 上刪除儲存體帳戶的失敗原因。 我們不刪除 hello 磁碟，以便您可以使用 hello 磁碟 toomount 另一個 VM。
* 仍與 hello 磁碟相關聯的磁碟或 hello blob 上的租用。
* 仍有正在使用 Blob、容器或儲存體帳戶的 VM 映像。

如果這份文件中並未提及您的 Azure 問題，請瀏覽 hello Azure 論壇上[MSDN 和 hello 堆疊溢位](https://azure.microsoft.com/support/forums/)。 您可以在這些論壇張貼您的問題或too@AzureSupportTwitter 上。 此外，您可以藉由選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options/)站台。

## <a name="symptoms"></a>徵兆
hello 下列區段會列出當您嘗試 toodelete hello Azure 儲存體帳戶、 容器或 Vhd 時，您可能會收到的常見錯誤。

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>案例 1： 無法 toodelete 儲存體帳戶
當您瀏覽 toohello 傳統儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com/)選取**刪除**，您可能會看到阻止 hello 儲存體帳戶刪除的物件清單：

  ![錯誤的映像時刪除 hello 儲存體帳戶](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

當您瀏覽 toohello 儲存體帳戶中 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)選取**刪除**，您可能會看到下列錯誤 hello 的其中一個：

- 儲存體帳戶 StorageAccountName 包含 VM 映像。確認這些 VM 映像已移除之後再刪除此儲存體帳戶。

- *無法 toodelete 儲存體帳戶 < vm 的儲存體帳戶的名稱 >。無法 toodelete 儲存體帳戶 < vm 的儲存體帳戶的名稱 >: ' < vm 的儲存體帳戶的名稱 > 的儲存體帳戶有一些作用中的映像及/或磁碟。確認這些映像及/或磁碟已移除之後再刪除此儲存體帳戶。」*

- *儲存體帳戶 <vm-storage-account-name> 有某些作用中的映像及/或磁碟，例如 xxxxxxxxx- xxxxxxxxx-O-209490240936090599。確認這些映像及/或磁碟已移除之後再刪除此儲存體帳戶。*

- *儲存體帳戶 <vm-storage-account-name> 已有 1 個具備作用中映像及/或磁碟成品的容器。請移除這些成品，hello 映像儲存機制中刪除這個儲存體帳戶之前*。

- *提交失敗的儲存體帳戶 <vm-storage-account-name> 已有 1 個具備作用中映像及/或磁碟成品的容器。請刪除這個儲存體帳戶之前先移除這些成品從 hello 映像儲存機制。當您嘗試 toodelete 儲存體帳戶且有與其相關聯的磁碟仍在作用中時，您會看到訊息，告知您有使用中磁碟需要刪除 toobe*。

### <a name="scenario-2-unable-toodelete-a-container"></a>案例 2： 無法 toodelete 容器
當您嘗試 toodelete hello 儲存體容器時，您可能會看到下列錯誤 hello:

*失敗的 toodelete 儲存體容器<container name>。錯誤: ' 目前沒有租用 hello 容器和 hello 要求中指定任何租用識別碼*。

或

*hello 下列虛擬機器磁碟使用在此容器中的 blob，因此無法刪除 hello 容器： VirtualMachineDiskName1、 VirtualMachineDiskName2，...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>案例 3： 無法 toodelete VHD
刪除 VM，然後再試一次 toodelete hello blob hello 相關聯的 Vhd 之後，您可能會收到下列訊息的 hello:

*失敗的 toodelete blob ' 路徑/XXXXXX XXXXXX-os-1447379084699.vhd'。錯誤: ' 目前沒有租用 hello blob 上，而且 hello 要求中指定任何租用識別碼。*

或

*Blob 'BlobName.vhd' 是正當做虛擬機器磁碟 'VirtualMachineDiskName'，因此無法刪除 hello blob。*

## <a name="solution"></a>方案
tooresolve hello 最常見的問題，請嘗試下列方法 hello:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>步驟 1： 刪除任何導致無法刪除 hello 儲存體帳戶、 容器或 VHD 的磁碟
1. 切換 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)。
2. 選取 [虛擬機器] > [磁碟]。

    ![Azure 傳統入口網站上虛擬機器上的磁碟影像。](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. 找出 hello 與 hello 儲存體帳戶、 容器或您想 toodelete VHD 相關聯的磁碟。 當您檢查 hello hello 磁碟位置時，您會發現 hello 相關聯的儲存體帳戶、 容器或 VHD。

    ![顯示 Azure 傳統入口網站上磁碟的位置資訊的影像](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. 使用其中一種 hello 下列方法刪除 hello 磁碟：

  - 如果沒有任何 VM 就會列在 hello**附加至**欄位的 hello 磁碟，您可以直接刪除 hello 磁碟。

  - 如果資料磁碟 hello 磁碟，請遵循下列步驟：

    1. 請檢查的 hello hello 磁碟的 VM 連接至 hello 名稱。
    2. 跳過**虛擬機器** > **執行個體**，然後找出 hello VM。
    3. 請確定不會主動使用 hello 磁碟。
    4. 選取**卸離磁碟**底部 hello hello 入口 toodetach hello 磁碟。
    5. 跳過**虛擬機器** > **磁碟**，並等候 hello**附加至**欄位 tooturn 空白。 這表示已成功中斷與 hello VM 連結 hello 磁碟。
    6. 選取**刪除**底部的 hello**虛擬機器** > **磁碟**toodelete hello 磁碟。

  - 如果 hello 磁碟是作業系統磁碟 (hello**包含 OS**欄位有值，例如 Windows) 及附加的 tooa VM，請遵循下列步驟 toodelete hello VM。 無法中斷 hello 作業系統磁碟，因此我們 toodelete hello VM toorelease hello 租用。

    1. 請檢查資料磁碟附加至 hello 虛擬機器 hello hello 名稱。  
    2. 跳過**虛擬機器** > **執行個體**，並選取 hello hello 磁碟的 VM 會附加至。
    3. 請確定不會主動使用 hello 虛擬機器，並確認您不再需要 hello 虛擬機器。
    4. 選取 hello VM hello 磁碟已連接，然後選取**刪除** > **刪除 hello 附加磁碟**。
    5. 跳過**虛擬機器** > **磁碟**，並等候 hello 磁碟 toodisappear。  可能需要幾分鐘，讓此 toooccur，，您可能需要 toorefresh hello 頁面。
    6. 如果 hello 磁碟並未消失，等候 hello**附加至**欄位 tooturn 空白。 這表示已完全中斷與 hello VM 連結 hello 磁碟。  接著，選取 hello 磁碟，並選取**刪除**底部 hello hello 分頁 toodelete hello 磁碟。


   > [!NOTE]
   > 如果磁碟已附加的 tooa VM，就能 toodelete 它。 磁碟會以非同步的方式中斷連接已刪除的 VM。 可能需要幾分鐘後，設定此欄位 tooclear 刪除 hello VM。
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>步驟 2： 刪除，無法刪除 hello 儲存體帳戶或容器的 VM 映像
1. 切換 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)。
2. 選取**虛擬機器** > **映像**，然後再刪除 hello 與 hello 儲存體帳戶、 容器或 VHD 相關聯的映像。

    在這之後，重試 toodelete hello 儲存體帳戶、 容器或 VHD。

> [!WARNING]
> 刪除 hello 帳戶之前，您有想 toosave 來確定 tooback 任何項目。 刪除 VHD、blob、資料表、佇列或檔案就是永久刪除。 請確認 hello 資源不是使用中。
>
>

## <a name="about-hello-stopped-deallocated-status"></a>關於 hello 已停止 （取消配置） 狀態
建立 hello 傳統部署模型中，並保留的 Vm 將會有 hello**已停止 （取消配置）**狀態任一 hello [Azure 入口網站](https://portal.azure.com/)或[Azure 傳統入口網站](https://manage.windowsazure.com/).

**Azure 傳統入口網站**：

![Azure 入口網站上 VM 的已停止 (已解除配置) 狀態。](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Azure 入口網站**︰

![Azure 傳統入口網站上 VM 的已停止 (已解除配置) 狀態。](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

「 已停止 （取消配置） 」 狀態釋放 hello 電腦資源，例如 hello CPU、 記憶體和網路。 hello 磁碟，不過，仍保留，因此您可以快速 hello VM 必要時重新建立。 這些磁碟都建立在由 Azure 儲存體提供的 VHD 上。 hello 儲存體帳戶的這些 Vhd，並 hello 磁碟的 Vhd 上的租用。

## <a name="next-steps"></a>後續步驟
* [刪除儲存體帳戶](storage-create-storage-account.md#delete-a-storage-account)
