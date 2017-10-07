---
title: "Azure Service Fabric 叢集 aaaSet |Microsoft 文件"
description: "快速入門 - 在 Azure 上建立 Windows 或 Linux Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>在 Azure 上建立您的第一個 Service Fabric 叢集
[Service Fabric 叢集](service-fabric-deploy-anywhere.md)是一組由網路連接的虛擬或實體機器，可用來將您的微服務部署到其中並進行管理。 本快速入門可協助您 toocreate 五個節點的叢集，執行 Windows 或 Linux 上透過 hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248)或[Azure 入口網站](http://portal.azure.com)短短幾分鐘內。  

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。


## <a name="use-hello-azure-portal"></a>使用 hello Azure 入口網站

登入 toohello 在 Azure 入口網站[http://portal.azure.com](http://portal.azure.com)。

### <a name="create-hello-cluster"></a>建立 hello 叢集

1. 按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。
2. 選取**計算**從 hello**新增**刀鋒視窗，然後選取**Service Fabric 叢集**從 hello**計算**刀鋒視窗。
3. 填寫 hello Service Fabric**基本概念**表單。 如**作業系統**，選取為 Windows 或 Linux 想 hello 叢集節點 toorun hello 版本。 在此輸入 hello 使用者名稱和密碼是使用的 toolog toohello 虛擬機器中。 對於 [資源群組]，建立新的資源群組。 資源群組是在其中建立和共同管理 Azure 資源的邏輯容器。 完成時，按一下 [確定]。

    ![叢集設定輸出][cluster-setup-basics]

4. 填寫 hello**叢集設定**表單。  對於 [節點類型計數]，請輸入"1"。

5. 選取**節點類型 1 （主要）**然後填寫 hello**節點型別設定**表單。  輸入節點型別名稱，並設定 hello[持久性層](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster)太"銅。 」  選取 VM 大小。

    節點型別定義 hello VM 大小的 Vm，自訂的端點數目，和其他設定 hello 該類型的 Vm。 定義每個節點型別設定為不同的虛擬機器規模集，也就是使用的 toodeploy 和受管理的虛擬機器所設定。 每個節點類型可以獨立相應增加或相應減少，可以開啟不同組的連接埠，並可以有不同的容量計量。  hello 第一次，或主要節點類型是服務網狀架構系統服務會裝載和必須有五個或多個 Vm 的位置。

    對於任何生產部署而言，[容量規劃](service-fabric-cluster-capacity.md)都是一個很重要的步驟。  不過，在此快速入門中，您不會執行應用程式，因此選取 DS1_v2 Standard VM 大小。  選取 「 銀級 」 hello[可靠性層](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster)和初始虛擬機器規模集容量是 5。  

    自訂端點開啟 hello Azure 負載平衡器中的連接埠，以便您可以在 hello 叢集上執行的應用程式連接。  輸入連接埠 80 和 8172"80，8172"tooopen。

    不會檢查 hello**設定進階設定** 方塊中，用於自訂 TCP/HTTP 管理端點，應用程式連接埠範圍，[位置條件約束](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints)，和[容量屬性](service-fabric-cluster-resource-manager-metrics.md)。    

    選取 [確定] 。

6. 在 hello**叢集設定**表單中，設定**診斷**太**上**。  本快速入門中，您就不需要 tooenter 任何[網狀架構設定](service-fabric-cluster-fabric-settings.md)屬性。  在**Fabric 版本**，選取**自動**升級模式，以便讓 Microsoft 自動更新 hello hello 網狀架構程式碼執行 hello 叢集版本。  將 hello 模式設定為太**手動**如果您想太[選擇支援的版本](service-fabric-cluster-upgrade.md)tooupgrade 至。 

    ![節點類型組態][node-type-config]

    選取 [確定] 。

7. 填寫 hello**安全性**表單。  在此快速入門中選取 [不安全]。  它強烈建議使用 toocreate 安全的叢集，針對生產工作負載，不過，因為任何人都可以匿名連接 tooan 不安全的叢集，並執行管理作業。  

    憑證用於 Service Fabric tooprovide 驗證和加密 toosecure 叢集，而它的應用程式的各個層面。 如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例](service-fabric-cluster-security.md)。  tooenable 使用者驗證應用程式安全性為使用 Azure Active Directory 或憑證 tooset[從資源管理員範本建立叢集](service-fabric-cluster-creation-via-arm.md)。

    選取 [確定] 。

8. 檢閱 hello 摘要。  如果您想要 toodownload 輸入從 hello 設定所建立的資源管理員範本，請選取**下載範本和參數**。  選取**建立**toocreate hello 叢集。

    您可以看到在 hello 通知 hello 建立進度。 （按一下 hello 狀態列會在 hello 右上角螢幕附近的 hello"鈴鐺 」 圖示）。如果您按下**Pin tooStartboard**同時建立 hello 叢集，您會看到**部署 Service Fabric 叢集**釘選 toohello**啟動**面板。

### <a name="view-cluster-status"></a>檢視叢集狀態
一旦建立您的叢集，您可以檢查您的叢集在 hello**概觀**hello 入口網站中的刀鋒視窗。 您現在可以看到您的叢集 hello 儀表板，包括 hello 叢集的公用端點及連結 tooService Fabric 總管中的 hello 詳細資料。

![叢集狀態][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>使用 Service Fabric 總管 中的 hello 叢集以視覺化方式檢視
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 是一個理想的工具，可將叢集視覺化及管理應用程式。  Service Fabric 總管是 hello 叢集中執行的服務。  Hello，即可使用網頁瀏覽器存取**Service Fabric 總管**hello 叢集的連結**概觀**hello 入口網站頁面中的。  您也可以直接在 hello 瀏覽器輸入 hello 位址： [http://quickstartcluster.westus.cloudapp.azure.com:19080/總管](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

hello 叢集儀表板提供您的叢集，包括應用程式和節點健全狀況摘要的概觀。 hello 節點檢視會顯示 hello 實體 hello 叢集配置。 對於指定的節點，您可以檢查已經在該節點上部署程式碼的應用程式。

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Toohello 叢集使用 PowerShell 連線
請確認該 hello 叢集正在執行使用 PowerShell 連線。  hello ServiceFabric PowerShell 模組會隨 hello [Service Fabric SDK](service-fabric-get-started.md)。  hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet 建立連線 toohello 叢集。   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
請參閱[連接 tooa 安全叢集](service-fabric-connect-to-secure-cluster.md)連接 tooa 叢集的其他範例。 在連接 toohello 叢集中之後, 使用 hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello 叢集和狀態資訊的每個節點中的節點清單。 每個節點的 **HealthState** 應該為「正常」。

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>移除 hello 叢集
Service Fabric 叢集所組成的其他 Azure 資源此外 toohello 叢集資源本身。 因此 toocompletely 刪除 Service Fabric 叢集，您也需要的 toodelete 所有 hello 則由的資源。 hello 最簡單方式 toodelete hello 叢集及它會取用所有 hello 資源是 toodelete hello 資源群組。 如叢集或 toodelete 資源群組中的某些 （但並非所有） hello 資源，請參閱其他方式 toodelete[刪除叢集](service-fabric-cluster-delete.md)

刪除資源群組 hello Azure 入口網站中：
1. 瀏覽您想 toodelete toohello Service Fabric 叢集。
2. 按一下 hello**資源群組**hello 叢集 essentials 頁面上的名稱。
3. 在 hello**資源群組 Essentials**頁面上，按一下**刪除資源群組**依該頁面 toocomplete hello 刪除 hello 資源群組中的 hello 指示。
    ![刪除 hello 資源群組][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>使用 Azure Powershell toodeploy 安全叢集
1. 下載 hello [Azure Powershell 模組版本 4.0 或更新版本](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)您的電腦上。

2. 開啟 Windows PowerShell 視窗中，執行下列命令的 hello。 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    您應該會看到類似 toohello 下列輸出。

    ![ps-list][ps-list]

3. 登入 tooAzure 和選取 hello 訂用帳戶 toowhich 想 toocreate hello 叢集

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. 執行下列命令 toonow 的 hello 建立安全的叢集。 不要忘記 toocustomize hello 參數。 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    hello 命令可能需要 10 分鐘 too30 分鐘 toocomplete，hello 結尾處，您應該會收到類似 toohello 下列輸出。 hello hello 憑證，它已上傳，所以 KeyVault hello 的相關資訊及輸出 hello 複製 hello 憑證所在的本機資料夾。 

    ![ps-out][ps-out]

5. 複製 hello 整個輸出並儲存 tooa 文字檔案，因為我們需要 toorefer tooit。 記下 hello hello 輸出中的下列資訊。 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>在您的本機電腦上安裝 hello 憑證
  
tooconnect toohello 叢集中，您會需要 tooinstall hello 憑證到 hello hello 目前使用者的個人 (My) 存放區。 

執行下列 PowerShell hello

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

現在您已經準備就緒 tooconnect tooyour 安全叢集。

### <a name="connect-tooa-secure-cluster"></a>Tooa 安全叢集連線 

執行下列 PowerShell 命令 tooconnect tooa 安全叢集的 hello。 hello 憑證詳細資料必須符合已使用的 tooset hello 叢集的憑證。 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


下列範例顯示 hello hello completed 參數： 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

執行下列命令 toocheck 您所連接的 hello 且 hello 叢集狀況良好。

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>發行您從 Visual Studio 的應用程式 tooyour 叢集

既然您已設定 Azure 的叢集，您可以發佈您的應用程式 tooit 從 Visual Studio 的下列 hello[發行 tooan 叢集](service-fabric-publish-app-remote-cluster.md)文件。 

### <a name="remove-hello-cluster"></a>移除 hello 叢集
叢集所組成的其他 Azure 資源此外 toohello 叢集資源本身。 hello 最簡單方式 toodelete hello 叢集及它會取用所有 hello 資源是 toodelete hello 資源群組。 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>後續步驟
既然您已設定開發叢集，請嘗試下列 hello:
* [Hello 入口網站中建立安全的叢集](service-fabric-cluster-creation-via-portal.md)
* [從範本建立叢集](service-fabric-cluster-creation-via-arm.md) 
* [使用 PowerShell 部署應用程式](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
