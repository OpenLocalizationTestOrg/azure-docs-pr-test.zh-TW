---
title: "aaaMicrosoft Azure 堆疊疑難排解 |Microsoft 文件"
description: "Azure Stack 疑難排解。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a20bea32-3705-45e8-9168-f198cfac51af
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: e274e92bc12fd6b7a2594f2f21b69ff0b9de594b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-troubleshooting"></a>Microsoft Azure Stack 疑難排解
此文件提供 Azure Stack 的常見疑難排解資訊。 

Hello Azure 堆疊技術開發套件提供做為評估環境，因為沒有官方支援在 Microsoft 客戶支援服務。  如果您遇到未記載的問題，請確定 toocheck hello [Azure 堆疊 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack)如需進一步協助和資訊。  

本章節所述的問題進行疑難排解的建議 hello 衍生自多個來源和可能或可能無法解決您特定的問題。 程式碼範例係依現況提供，而且無法保證程式碼會產生預期結果。 這個區段是主體 toofrequent 編輯，以及改進 toohello 產品的更新中實作。

## <a name="deployment"></a>部署
### <a name="deployment-failure"></a>部署失敗
如果您在安裝期間遇到失敗，您可以使用 hello 部署指令碼 toorestart hello 部署的 hello 失敗的步驟從使用 hello 重新執行選項。  


### <a name="at-hello-end-of-hello-deployment-hello-powershell-session-is-still-open-and-doesnt-show-any-output"></a>Hello 部署結束時的 hello，hello PowerShell 工作階段仍為開啟且未顯示任何輸出
這種行為可能是只 hello 結果的 hello PowerShell 命令視窗中，預設行為，已選取時。 hello 開發套件部署實際上已成功，但選取 hello 視窗時，已暫停 hello 指令碼。 您可以確認這是尋找 hello word"select"hello 的 hello 命令視窗的標題列中的 hello 案例。  按下 esc 鍵 hello 金鑰 toounselect，且 hello 完成訊息應該會顯示它的後面。

## <a name="templates"></a>範本
### <a name="azure-template-wont-deploy-tooazure-stack"></a>Azure 範本不會將部署 tooAzure 堆疊
請確定：

* hello 範本必須使用 Microsoft Azure 服務已使用或 Azure 堆疊中的預覽。
* hello 用於特定資源的 Api 都支援 hello 本機堆疊 Azure 執行個體，以及所設定的目標是有效的位置 （「 本機 」 在 Azure 堆疊開發套件，vs hello 「 美國東部"或"印度南部及印度 」 在 Azure 中）。
* 您檢閱[本文](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/README.md)hello 測試 AzureRmResourceGroupDeployment cmdlet 相關的攔截 Azure 資源管理員語法的小差異。

您也可以使用 hello 中已經提供的 hello Azure 堆疊範本[GitHub 儲存機制](http://aka.ms/AzureStackGitHub/)toohelp 您立即開始。

## <a name="virtual-machines"></a>虛擬機器
### <a name="default-image-and-gallery-item"></a>預設映像與資源庫項目
在 Azure Stack 中部署 VM 之前，您必須先新增 Windows Server 映像與資源庫項目。

### <a name="after-restarting-my-azure-stack-host-some-vms-may-not-automatically-start"></a>重新啟動我的 Azure Stack 主機之後，某些 VM 可能不會自動啟動。
將您的主機重新開機之後，您可能會注意到 Azure Stack 服務並非立即可用。  這是因為 Azure 堆疊[基礎結構 Vm](azure-stack-architecture.md#virtual-machine-roles)和 RPs 採取有點 toocheck 一致性，但最終將會自動啟動。

您也可能會注意到 hello Azure 堆疊開發套件主應用程式的重新開機後自動啟動 Vm，不該租用戶。  這是已知的問題，因此只需要幾個手動步驟 toobring 上線：

1.  在 [hello Azure 堆疊開發套件主機上啟動**容錯移轉叢集管理員**從 hello 開始] 功能表。
2.  選取 hello 叢集**S Cluster.azurestack.local**。
3.  選取 [角色]。
4.  租用戶 VM 將會顯示為「已儲存」狀態。  基礎結構的所有 Vm 正在都執行，以滑鼠右鍵按一下 hello 租用戶 Vm，並選取**啟動**tooresume hello VM。

### <a name="i-have-deleted-some-virtual-machines-but-still-see-hello-vhd-files-on-disk-is-this-behavior-expected"></a>我已刪除一些虛擬機器，但仍看見 hello 磁碟上的 VHD 檔案。 這是不是預期行為？
是，這是預期行為。 將它設計成這樣的原因是：

* 當您刪除 VM 時，不會刪除 VHD。 磁碟是 hello 資源群組中的個別資源。
* 取得刪除儲存體帳戶，hello 刪除會顯示立即透過 Azure 資源管理員 （網站、 PowerShell），但執行記憶體回收之前仍 hello 磁碟，它可能包含存放在儲存體。

如果您看到 「 字串 」 Vhd 時，很重要 tooknow 如果它們是 hello 資料夾已刪除的儲存體帳戶的一部分。 如果未刪除 hello 儲存體帳戶，這是正常它們仍然會有。

閱讀更多有關設定 hello 保留臨界值和隨回收中的[管理儲存體帳戶](azure-stack-manage-storage-accounts.md)。

## <a name="storage"></a>儲存體
### <a name="storage-reclamation"></a>儲存體回收
它可能需要向上 hello 入口網站中的回收的容量 tooshow toofourteen 小時。 空間回收取決於各種因素，包括區塊 Blob 存放區中內部容器檔案的使用量百分比。 因此，根據多少資料都會刪除，並不保證 hello 記憶體回收行程執行時，無法回收的空間數量。

## <a name="powershell"></a>PowerShell
### <a name="resource-providers-not-registered"></a>資源提供者未註冊
當使用 PowerShell 連線 tootenant 訂用帳戶，您會發現 hello 資源提供者不會自動註冊。 使用 hello [Connect 模組](https://github.com/Azure/AzureStack-Tools/tree/master/Connect)，或執行的 hello PowerShell 中的下列命令 (之後[安裝，而且連接](azure-stack-connect-powershell.md)租用戶身分): 
  
       Get-AzureRMResourceProvider | Register-AzureRmResourceProvider

## <a name="cli"></a>CLI

* hello CLI 互動式模式也就是 hello `az interactive` Azure 堆疊中尚不支援命令。
* 提供使用 hello Azure 堆疊中的虛擬機器映像 tooget hello 清單`az vm images list --all`命令而不是 hello`az vm image list`命令。 指定 hello`--all`選項可確保回應會傳回提供 Azure 堆疊環境中的 hello 映像。 
* Azure 提供的虛擬機器映像別名可能不適用 tooAzure 堆疊。 當使用虛擬機器映像，您必須使用 hello 整個 URN 參數 (Canonical: UbuntuServer:14.04.3-LTS:1.0.0) 而不是 hello 映像的別名。 與這個 URNmust 符合 hello 映像規格，為衍生自 hello`az vm images list`命令。
* 根據預設，CLI 2.0 會使用"Standard_DS1_v2 」 為 hello 預設虛擬機器映像大小。 不過，這個大小尚無法使用 Azure 堆疊中，因此，您需要 toospecify hello`--size`建立虛擬機器時，明確的參數。 您可以取得 hello 使用 hello 都可以在 Azure 堆疊中的虛擬機器大小清單`az vm list-sizes --location <locationName>`命令。


## <a name="windows-azure-pack-connector"></a>Windows Azure 套件連接器
* 如果您變更 hello hello azurestackadmin 帳戶密碼，在您部署 Azure 堆疊開發套件之後，您不再可以設定多個雲端模式。 因此，不是可能 tooconnect toohello 目標 Windows Azure Pack 環境。
* 當您設定多雲端模式之後：
    * 使用者可以看到 hello 儀表板，他們重設 hello 入口網站設定之後，才。 （在 hello 使用者入口網站中，按一下 hello 入口網站設定圖示 （hello 右上角的齒輪圖示）。 在 [還原預設設定] 下，按一下 [套用])。
    * hello 儀表板標題可能不會出現。 若發生此問題，您必須手動將它們新增回來。
    * 有些方塊可能不會顯示正確當您初次加入它們 toohello 儀表板。 toofix 這個問題，請重新整理 hello 瀏覽器。



