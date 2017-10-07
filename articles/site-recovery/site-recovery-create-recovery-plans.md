---
title: "aaaCreate 復原計劃的容錯移轉和復原在 Azure Site Recovery |Microsoft 文件"
description: "描述如何 toocreate 和自訂復原計劃在 Azure Site Recovery，toofail 透過復原 Vm 和實體伺服器"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>建立復原方案


本文提供在 [Azure Site Recovery](site-recovery-overview.md) 中建立和自訂復原方案的相關資訊。

將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

 建立之後復原計劃 toodo hello:

* 定義會一起容錯移轉並啟動的機器群組。
* 將機器分到同一個復原計畫群組，藉以建立機器間的相依性。 例如，透過 toofail 並顯示特定應用程式，您分組 hello Vm hello 到該應用程式的所有相同復原計劃的群組。
* 執行容錯移轉。 您可以透過復原方案執行測試，以及執行規劃或未規劃的容錯移轉。


## <a name="create-a-recovery-plan"></a>建立復原計畫

1. 按一下 [復原計畫] > [建立復原計畫]。
   指定 hello 復原計劃，以及來源和目標的名稱。 hello 來源位置必須具有啟用容錯移轉和復原的虛擬機器。

    - 對於 VMM tooVMM 複寫，請選取**來源類型** > **VMM**，和 hello 來源與目標 VMM 伺服器。 按一下**HYPER-V** toosee 雲端所保護。
    - 針對 VMM tooAzure 選取**來源類型** > **VMM**。  選取 hello 來源 VMM 伺服器，和**Azure**為 hello 目標。
    - HYPER-V 複寫 tooAzure （無 VMM)，請選取**來源類型** > **HYPER-V 站台**。 選取 hello hello 來源站台和**Azure**為 hello 目標。
    - VMware VM 或實體內部部署伺服器 tooAzure，選取設定伺服器為 hello 來源和**Azure**為 hello 目標。
    - 對於 Azure tooAzure 復原計劃中，選取 Azure 區域為 hello 來源和次要 Azure 地區做為 hello 目標。 hello 次要 Azure 地區是只有這些 toowhich 虛擬機器受到保護。
2. 在**選取虛擬機器**，選取 hello 虛擬機器 （或複寫群組） 的 tooadd toohello 預設群組 (群組 1) hello 復原計劃中。

## <a name="customize-and-extend-recovery-plans"></a>自訂和擴充復原計畫

您可以自訂和擴充復原計畫：

- **新增群組**— 新增額外的復原計劃 （向上 tooseven) 群組 toohello 預設群組，然後再新增 更多的機器或複寫群組 toothose 復原計畫群組。 群組會以您新增的 hello 順序編號。 虛擬機器或複寫群組只能包含在一個復原計畫群組中。
- 新增手動動作 — 您可以新增手動動作，在建立復原方案群組之前或之後執行。 Hello 復原計劃執行時，會在插入 hello 手動動作的 hello 點停止。 出現對話方塊提示 toospecify hello 手動動作已完成。
- 新增指令碼 — 您可以新增指令碼，在建立復原計畫群組之前或之後執行。 當您將指令碼時，它會加入一組新的 hello 群組的動作。 例如，將建立一組前置步驟，針對群組 1 hello 名稱： 群組 1： 前置步驟。 所有前置步驟都會列於此動作集中。 如果您有部署的 VMM 伺服器，可以只 hello 主要站台上將指令碼。
- **新增 Azure Runbook**— 您可以使用 Azure runbook 擴充復原計畫。 例如，tooautomate 工作或 toocreate 單一步驟復原。 [深入了解](site-recovery-runbook-automation.md)。

## <a name="add-scripts"></a>新增指令碼

在您的復原計畫中，您可以使用 PowerShell 指令碼。

 - 請確定指令碼會使用 try catch 區塊，以便依正常程序處理 hello 例外狀況。
    - 如果沒有 hello 指令碼中的例外狀況，會停止執行，而且 hello 工作會顯示為失敗。
    - 如果發生錯誤，無法執行 hello 指令碼的任何其餘部分。
    - 如果當您執行非計劃性容錯移轉時，也會發生錯誤，會繼續 hello 復原計劃。
    - 如果當您執行規劃的容錯移轉時，就會發生錯誤，就會停止 hello 復原計劃。 您需要 toofix hello 指令碼，確認它如預期執行，然後執行 hello 復原方案一次。
- hello Write-host 命令無法在復原計劃的指令碼，並 hello 指令碼會失敗。 toocreate 輸出，建立 proxy 指令碼，接著執行主要指令碼。 請確定所有輸出會經由管道都輸出使用 hello >> 命令。
  * hello 指令碼逾時，如果它不會在 600 秒內傳回。
  * 如果任何項目會寫出 tooSTDERR，hello 指令碼之分類為失敗。 這項資訊會顯示在 hello 指令碼執行詳細資料。

如果您在部署中使用 VMM：

* Hello hello VMM 服務帳戶內容中，執行復原計劃中的指令碼。 請確定此帳戶具有 hello 遠端共用的 hello 指令碼所在的 「 讀取 」 權限。 測試 hello 指令碼 toorun 在 hello VMM 服務帳戶權限層級。
* 會在 Windows PowerShell 模組中傳遞 VMM Cmdlet。 當您安裝 hello VMM 主控台安裝 hello 模組。 它可以載入到您的指令碼，使用下列命令 hello 指令碼中的 hello:
   - Import-Module -Name virtualmachinemanager。 [深入了解](https://technet.microsoft.com/library/hh875013.aspx)。
* 確認您的 VMM 部署中至少有一部程式庫伺服器。 根據預設，VMM 伺服器 hello 程式庫共用路徑位於本機 hello 與 hello 資料夾名稱 MSCVMMLibrary 的 VMM 伺服器上。
    * 如果您的程式庫共用路徑遠端 （或本機但是並未與 MSCVMMLibrary 共用），請設定 hello 共用，如下所示 (使用\\libserver2.contoso.com\share\ 做為範例):
      * 開啟 hello 登錄編輯器並瀏覽過**HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure 網站 Recovery\Registration**。
      * 編輯 hello 值**ScriptLibraryPath** ，並將它當做\\libserver2.contoso.com\share\. 指定 hello 完整的 FQDN。 提供 toohello 共用位置的權限。
      * 請務必測試 hello 指令碼 hello 相同的使用者帳戶權限為 hello VMM 服務帳戶。 這會檢查該獨立測試中執行的指令碼 hello 相同方式與它們會依照復原方案。 Hello VMM 伺服器上，設定 hello 執行原則 toobypass 如下所示：
        * 開啟 hello 64 位元 Windows PowerShell 主控台，使用提高的權限。
        * 類型： **Set-executionpolicy bypass**。 [深入了解](https://technet.microsoft.com/library/ee176961.aspx)。

## <a name="add-a-script-or-manual-action-tooa-plan"></a>新增指令碼或手動動作 tooa 計劃

新增 Vm 或複寫群組 tooit，及建立 hello 計劃之後，您可以加入指令碼 toohello 預設復原計畫群組。

1. 開啟 hello 復原計劃。
2. 按一下項目在 hello**步驟**清單，然後再按**指令碼**或**手動動作**。
3. 指定 toowant tooadd hello 指令碼或動作之前或之後 hello 選取項目。 使用 hello**移**和**下移**按鈕，toomove hello hello 指令碼的位置向上或向下。
4. 如果您新增 VMM 指令碼，請選取**容錯移轉 tooVMM 指令碼**。 在**指令碼路徑**，型別 hello 相對路徑 toohello 共用。 您可以在 hello VMM 面範例中，指定 hello 路徑： **\RPScripts\RPScript.PS1**。
5. 如果您加入 Azure 自動化執行活頁簿時，指定 hello Azure 自動化帳戶中的 hello runbook 是 hello，並選取適當的 Azure runbook 指令碼。
6. Hello 復原計劃的容錯移轉，如預期般運作 toomake 確定 hello 指令碼。


### <a name="add-a-vmm-script"></a>新增 VMM 指令碼

如果您有 VMM 來源站台，您可以 hello VMM 伺服器上，建立指令碼，並將它包含在復原計劃。

1. Hello 程式庫共用中建立新的資料夾。 例如，\<VMMServerName>\MSSCVMMLibrary\RPScripts。 將它放在 hello 來源與目標 VMM 伺服器。
2. 建立 hello 指令碼 (例如 RPScript)，並檢查它如預期般運作。
3. Hello 指令碼置於 hello 位置\<> \MSSCVMMLibrary，hello 來源和目標 VMM 伺服器上的。


## <a name="next-steps"></a>後續步驟

[深入了解](site-recovery-failover.md) 如何執行容錯移轉。
