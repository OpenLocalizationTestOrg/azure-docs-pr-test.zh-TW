---
title: "應用程式升級主題 aaaAdvanced |Microsoft 文件"
description: "本文涵蓋有關 tooupgrading Service Fabric 應用程式的某些進階的主題。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>Service Fabric 應用程式升級：進階主題
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>在應用程式升級期間加入或移除服務
如果以升級加入 tooan 應用程式已經部署，並發行新的服務，就會 hello 新服務加入的 toohello 部署應用程式。  這類升級不會影響任何 hello 服務已經過 hello 應用程式的一部分。 不過，已加入的 hello 服務的執行個體必須啟動 hello 新服務 toobe 作用中 (使用 hello `New-ServiceFabricService` cmdlet)。

服務也可從應用程式以升級的方式移除。 不過，必須停止 hello 要刪除服務的所有目前的執行個體繼續執行 hello 升級 (使用 hello `Remove-ServiceFabricService` cmdlet)。

## <a name="manual-upgrade-mode"></a>手動升級模式
> [!NOTE]
> hello 未受監視的手動模式只應該考量失敗或已暫停的升級。 hello 受監視的模式是 hello 建議 Service Fabric 應用程式的升級模式。
>
>

Azure Service Fabric 提供多個升級模式 toosupport 開發和生產叢集。 選擇的部署選項可能會因不同的環境而不同。

受監視的 hello 輪流應用程式升級為 hello 最常見升級的 toouse hello 實際執行環境中。 當 hello 升級指定原則時，Service Fabric 可確保 hello 應用程式狀況良好，才 hello 升級會繼續執行。

 hello 應用程式系統管理員可以使用 hello 手動復原應用程式升級模式 toohave 的完整控制權 hello 升級進度 hello 透過各種 「 升級 」 網域。 自訂或複雜的健全狀況評估原則是必要的或發生非傳統升級時，此模式非常有用 （例如，hello 應用程式已在資料遺失）。

最後，hello 自動化的應用程式輪流升級是適用於開發或測試環境 tooprovide 快速的反覆項目循環期間服務開發。

## <a name="change-toomanual-upgrade-mode"></a>變更 toomanual 升級模式
**手動**-hello 目前 UD 和變更 hello 停止 hello 應用程式升級升級模式 tooUnmonitored 手冊。 hello 系統管理員必須 toomanually 呼叫**MoveNextApplicationUpgradeDomainAsync**以 hello tooproceed 升級，或藉由初始化新的升級觸發復原。 一旦 hello 升級進入 hello 手動模式時，它會保持在 hello 手動模式起始新的升級之前。 hello **GetApplicationUpgradeProgressAsync**命令會傳回網狀架構\_應用程式\_升級\_狀態\_循環\_向前\_擱置。

## <a name="upgrade-with-a-diff-package"></a>使用差異封裝進行升級
Service Fabric 應用程式可以藉由佈建完整、獨立式應用程式封裝來升級。 也可以使用包含唯一的 hello 更新應用程式檔案的差異比對封裝來升級應用程式，hello 更新應用程式資訊清單和 hello 服務資訊清單檔案。

完整的應用程式套件包含所有 hello 檔案需要 toostart 和執行 Service Fabric 應用程式。 Diff 封裝包含只有 hello hello 最後一個佈建與 hello 目前升級時，之間變更的檔案加上 hello 完整的應用程式資訊清單和 hello 服務資訊清單檔案。 Hello 應用程式資訊清單或 hello 組建版面配置中找不到的服務資訊清單中的任何參考搜尋 hello 映像存放區中。

完整的應用程式套件所需的應用程式 toohello 叢集 hello 第一次安裝。 後續更新可以是完整應用程式封裝或差異封裝。

有時候使用差異封裝也是很好的選擇：

* 當您有大型應用程式封裝參考數個服務資訊清單檔案及/或數個程式碼封裝、組態封裝或資料封裝時，最好使用差異封裝。
* 您有部署系統，直接從您的應用程式建置程序產生 hello 組建版面配置時，最好使用差異封裝。 在此情況下，雖然 hello 碼未變更，新建立的組件會得到不同的總和檢查碼。 使用完整的應用程式封裝需要您 tooupdate hello 版本所有的程式碼封裝。 使用 差異比對封裝，您僅提供變更的 hello 檔案及 hello hello 版本已變更的資訊清單的檔案。

使用 Visual Studio 升級應用程式時，便會自動發行 hello 差異封裝。 手動 hello toocreate 差異比對封裝的應用程式資訊清單中，與 hello 服務資訊清單必須加以更新，但只有變更的 hello 封裝應該包含在 hello 最終的應用程式套件。

例如，讓我們開始 hello 下列應用程式 （為了便於了解所提供的版本號碼）：

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

現在，假設您想要 tooupdate 只有 hello 程式碼封裝的 service1 使用差異比對封裝使用 PowerShell。 現在，您更新的應用程式具有下列資料夾結構的 hello:

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

在此情況下，您更新應用程式資訊清單 too2.0.0 hello 和 hello 服務 service1 tooreflect hello 程式碼封裝更新資訊清單。 應用程式套件的 hello 資料夾中會有下列結構的 hello:

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。

[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。

使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。

讓應用程式升級相容所學習如何 toouse[資料序列化](service-fabric-application-upgrade-data-serialization.md)。

藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。
