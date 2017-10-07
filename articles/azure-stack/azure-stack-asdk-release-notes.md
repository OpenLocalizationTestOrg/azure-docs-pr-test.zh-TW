---
title: "aaaMicrosoft Azure 堆疊開發套件版本資訊 |Microsoft 文件"
description: 
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: helaw
ms.openlocfilehash: c1644f224933a63e1f0265b6ef4113789900cf12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-development-kit-release-notes"></a>Azure Stack 開發套件版本資訊
這些版本資訊提供新功能和已知問題的相關資訊。

## <a name="release-build-201706271"></a>版本組建 20170627.1
開頭為 hello [20170627.1](azure-stack-updates.md#determine-the-current-version)版本中，Azure 堆疊概念證明已重新命名的 tooAzure 堆疊開發套件。  就像 hello Azure 堆疊 POC，Azure 堆疊開發套件是 toobe 開發和評估環境使用 tooexplore Azure 堆疊功能，並提供開發平台的 Azure 堆疊。

### <a name="whats-new"></a>新功能
- 您現在可以使用命令列的 CLI 2.0 toomanage Azure 堆疊資源受歡迎的作業系統上。
- DSV2 虛擬機器大小支援 Azure 和 Azure Stack 之間的範本可攜性。
- 雲端操作員可以預覽 hello 容量管理刀鋒視窗中的 hello 容量管理經驗。
- 您現在可以從您的虛擬機器使用 hello Azure 診斷擴充功能 toogather 診斷資料。  在分析工作負載效能及調查問題時，收集此資料會非常有用。
- 新的[部署體驗](azure-stack-run-powershell-script.md)取代了先前已編寫指令碼的部署步驟。  hello 新的部署經驗提供通用的圖形化介面，透過 hello 整個部署生命週期。
- 現在部署期間支援 Microsoft 帳戶 (MSA)。
- 現在部署期間也支援 Multi-Factor Authentication (MFA)。  之前在部署期間必須停用 MFA。

### <a name="known-issues"></a>已知問題
#### <a name="deployment"></a>部署
* 您可能會注意到部署時使用的時間比舊版長。 
* Get AzureStackLogs 會產生診斷記錄檔，不過，不會記錄進度 toohello 主控台。
* 您必須使用 hello 新[部署經驗](azure-stack-run-powershell-script.md)toodeploy Azure 堆疊或部署可能會失敗。

#### <a name="portal"></a>入口網站
* 您可能會看見 hello 入口網站中的空白儀表板。  您可以在 hello 右上方的 hello 入口網站中，選取 hello 齒輪，然後選取 [還原預設設定] 來復原 hello 儀表板。
* 租用戶可以 toobrowse hello 完整 marketplace 沒有訂用帳戶，而且將會看到像計劃和優惠的系統管理項目。  這些項目包含非功能性 tootenants。
* 在選取基礎結構角色執行個體時，您會看到顯示參考錯誤的錯誤。 使用 hello 瀏覽器的重新整理功能 toorefresh hello 管理入口網站。
* hello 「 移動 」 按鈕已停用 hello 資源群組 刀鋒視窗。  這是預期的行為，因為目前不支援在訂用帳戶之間移動資源群組。
* 您將會收到和已完成下載之聯合市集項目有關的重複通知。
* 您不能 tooview 權限 tooyour 使用 hello Azure 堆疊入口網站的訂用帳戶。  解決方法是，可以使用 Powershell 確認權限。
* 您必須新增`-TenantID`做為從 hello 入口網站的自動化指令碼匯出已完成的部署時的旗標。

#### <a name="services"></a>服務
* 金鑰保存庫服務必須建立從 hello 租用戶入口網站或租用戶 API。  如果您以系統管理員身分登入，請確定 toouse hello 租用戶入口網站 toocreate 新的金鑰保存庫保存庫、 機密資料，並且索引鍵。
* 雖然可以透過範本建立虛擬機器擴展集，但是沒有可用於建立它們的市集體驗。
* 您無法將負載平衡器與 hello 入口網站透過後端 」 網路。  此工作可以透過 PowerShell 或透過範本來完成。
* VM 可用性設定組只能設定一個容錯網域和一個更新網域。  
* 租用戶必須有現有的儲存體帳戶，才能建立新的 Azure Function。
* VM 可能會失敗並報告 「 無法繫結引數 tooparameter 'VM 網路介面卡' 因為它是 null。 」  重新部署的 hello 虛擬機器就會成功。  
* 刪除租用戶訂用帳戶會導致產生孤立的資源。  因應措施是，先刪除租用戶資源或整個資源群組，然後再刪除租用戶訂用帳戶。 
* 建立網路負載平衡器時，您必須建立 NAT 規則，或當您嘗試 tooadd NAT 規則建立 hello 負載平衡器後，您會收到錯誤。
* 租用戶可以建立大於配額允許大小的虛擬機器。  此行為是因為未強制套用計算配額。
* 租用戶不指定的 hello 選項 toocreate 具有地理備援儲存體的虛擬機器。  此組態導致虛擬機器建立 toofail。
* 它可能會佔用 tooan 小時之前租用戶可以在新的 SQL 或 MySQL SKU 中建立資料庫。 
* 建立直接在 SQL 和 MySQL 主控伺服器不會執行 hello 資源提供者上的項目不支援，以及可能會導致不相符的狀態。
* AzureRM PowerShell 1.2.10 需要額外的設定步驟：
    * 請在執行 Azure AD 部署的 Add-AzureRMEnvironment 之後執行此作業。  提供使用 hello 輸出 hello 名稱] 和 [GraphAudience 值`Add-AzureRMEnvironment`。
      
      ```PowerShell
      Set-AzureRmEnvironment -Name <Environment Name> -GraphAudience <Graph Endpoint URL>
      ```
    * 請在執行 AD FS 部署的 Add-AzureRMEnvironment 之後執行此作業。  提供使用的 hello 輸出 hello 名稱] 和 [GraphAudience 值`Add-AzureRMEnvironment`。
      
      ```PowerShell
      Set-AzureRmEnvironment <Environment Name> -GraphAudience <Graph Endpoint URL> -EnableAdfsAuthentication:$true
      ```
    
    例如，hello 下列可用於 Azure AD 環境：

    ```PowerShell
      Set-AzureRmEnvironment AzureStack -GraphAudience https://graph.local.azurestack.external/
    ```

#### <a name="fabric"></a>網狀架構
* hello 計算資源提供者顯示未知的狀態。
* hello 必要節點資訊的延展單位中未顯示 hello BMC IP 位址 （& s） 模型。  這是 Azure Stack 開發套件中的預期行為。
* 不應該使用 hello 計算控制器基礎結構角色 （AzS XRP01 執行個體） 上的重新啟動動作。
* hello 備份刀鋒視窗中不應使用的基礎結構。
