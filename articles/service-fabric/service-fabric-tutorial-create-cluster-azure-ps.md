---
title: "在 Azure 中的 aaaCreate Service Fabric 叢集 |Microsoft 文件"
description: "了解如何 toocreate Windows 或 Linux Service Fabric 叢集使用 PowerShell 在 Azure 中。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>使用 PowerShell 在 Azure 上建立安全叢集
本教學課程告訴您如何 toocreate Service Fabric 叢集 （Windows 或 Linux） 的執行在 Azure 中。 當您完成時，您會有叢集，您可以將應用程式部署的 hello 雲端中執行。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 使用 PowerShell 在 Azure 中建立安全的 Service Fabric 叢集
> * 使用 X.509 憑證的安全 hello 叢集
> * Toohello 叢集使用 PowerShell 連線
> * 刪除叢集

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前：
- 如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- 安裝 hello [Service Fabric SDK 及 PowerShell 模組](service-fabric-get-started.md)
- 安裝 hello [Azure Powershell 模組版本 4.1 或更高版本](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

hello 遵循程序會建立單一節點 （單一虛擬機器） 預覽 Service Fabric 叢集。 取得與 hello 叢集一起建立，然後放置在金鑰保存庫的自我簽署憑證以保護 hello 叢集。 單一節點叢集無法擴充超過一部虛擬機器，並預覽叢集不能升級的 toonewer 版本。

導致 Service Fabric 叢集正在使用 Azure hello toocalculate 成本[Azure 定價計算機](https://azure.microsoft.com/pricing/calculator/)。
如需建立 Service Fabric 叢集的詳細資訊，請參閱[使用 Azure Resource Manager 來建立 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。

## <a name="create-hello-cluster-using-azure-powershell"></a>建立 hello 叢集使用 Azure PowerShell
1. 從 hello 下載 hello Azure Resource Manager 範本與 hello 參數檔案的本機副本[Azure Resource Manager 範本適用於 Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub 儲存機制。  *azuredeploy.json* hello Azure 資源管理員範本可定義 Service Fabric 叢集。 *azuredeploy.parameters.json* toocustomize hello 叢集部署是為您的參數檔案。

2. 來自訂下列參數在 hello hello *azuredeploy.parameters.json*參數檔案：

   | 參數       | 說明 | 建議的值 |
   | --------------- | ----------- | --------------- |
   | clusterLocation | hello Azure 地區 toowhich toodeploy hello 叢集。 | *例如 westeurope、eastasia、eastus* |
   | clusterName     | 名稱要 toocreate 的 hello 叢集。 | *例如 bobs-sfpreviewcluster* |
   | adminUserName   | hello hello 叢集虛擬機器上的本機系統管理員帳戶。 | *任何有效的 Windows Server 使用者名稱* |
   | adminPassword   | Hello hello 叢集虛擬機器上的本機系統管理員帳戶的密碼。 | *任何有效的 Windows Server 密碼* |
   | clusterCodeVersion | hello Service Fabric 版本 toorun。 (255.255.X.255 是預覽版本)。 | **255.255.5718.255** |
   | vmInstanceCount | hello （可以是 1 或 3-99） 叢集中的虛擬機器數目。 | **1** | *對於預覽叢集，請僅指定一部虛擬機器* |

3. 開啟 PowerShell 主控台中，登入 tooAzure，並選取您想 toodeploy hello 叢集在 hello 訂用帳戶：

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. 建立並加密 hello 憑證 toobe Service Fabric 所使用的密碼。

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. 執行下列命令的 hello 建立 hello 叢集和其憑證：

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >hello`-CertificateSubjectName`參數應符合的 hello 參數檔案中指定的 hello clusterName 參數、 以及 hello 繫結的網域 toohello Azure 區域為您選擇，例如： `clustername.eastus.cloudapp.azure.com`。

一旦 hello 組態完成時，它會輸出建立在 Azure 中的 hello 叢集的相關資訊。 它也會複製 hello 叢集憑證 toohello-CertificateOutputFolder 目錄上 hello 這個參數所指定的路徑。 您需要此憑證 tooaccess Service Fabric 總管和檢視 hello 健全狀況的叢集。

記下您的叢集，可能會類似 toohello hello URL 下列 URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>修改 hello 憑證 （& s) 存取 Service Fabric 總管 ##

1. 按兩下 hello 憑證 tooopen hello 憑證匯入精靈。

2. 使用預設設定，但請確定 toocheck hello**標示成可匯出此機碼。** 在 [hello] 核取方塊，**私密金鑰保護**步驟。 稍後在本教學課程設定 Azure 容器登錄中 tooService Fabric 叢集驗證時，visual Studio 需要 tooexport hello 憑證。

3. 現在，您可以在瀏覽器中開啟 Service Fabric Explorer。 toodo，瀏覽 toohello **ManagementEndpoint**供您使用網頁瀏覽器，並選取 hello 憑證儲存在您的電腦的叢集 URL。

>[!NOTE]
>由於您使用自我簽署的憑證，因此開啟 Service Fabric Explorer 時會顯示憑證錯誤。 在 Edge 中，您有 tooclick*詳細資料*然後 hello 和*toohello 網頁上移*連結。 在 Chrome 中，您有 tooclick*進階*然後 hello 和*繼續*連結。

>[!NOTE]
>如果 hello 叢集建立失敗，您永遠可以重新執行 hello 命令，就會更新已部署的 hello 資源。 如果失敗的 hello 部署的一部分建立憑證時，會產生一個新。 tootroubleshoot 建立叢集，請參閱[使用 Azure Resource Manager 建立 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。

## <a name="connect-toohello-secure-cluster"></a>Toohello 安全叢集連線
使用 hello 與 hello Service Fabric SDK 一起安裝的 Service Fabric PowerShell 模組的 toohello 叢集連線。  首先，將 hello 憑證安裝到您的電腦上的 hello 目前使用者 hello 個人 (My) 存放區。  執行下列 PowerShell 命令的 hello:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

現在您已經準備就緒 tooconnect tooyour 安全叢集。

hello **Service Fabric** PowerShell 模組提供許多 cmdlet 來管理 Service Fabric 叢集、 應用程式和服務。  使用 hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello 安全叢集。 hello 憑證指紋，並從上一個步驟的 hello 輸出中找到連接端點詳細資料。

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

請檢查您已連線，且 hello 叢集狀況良好使用 hello [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet。

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>清除資源

叢集所組成的其他 Azure 資源此外 toohello 叢集資源本身。 hello 最簡單方式 toodelete hello 叢集及它會取用所有 hello 資源是 toodelete hello 資源群組。

登入 tooAzure，並選取您要與其 tooremove hello 叢集 hello 訂用帳戶 ID。  您可以找到您的訂用帳戶 ID 登入 toohello [Azure 入口網站](http://portal.azure.com)。 刪除 hello 資源群組和所有 hello 叢集資源使用 hello[移除 AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup)。

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 在 Azure 中建立 Service Fabric 叢集
> * 使用 X.509 憑證的安全 hello 叢集
> * Toohello 叢集使用 PowerShell 連線
> * 刪除叢集

接下來，前進 toohello 如何遵循教學課程 toolearn toodeploy 現有的應用程式。
> [!div class="nextstepaction"]
> [透過 Docker Compose 部署現有的 .NET 應用程式](service-fabric-host-app-in-a-container.md)
