---
title: "設定獨立 Azure Service Fabric 叢集 aaaSet |Microsoft 文件"
description: "以 hello 上執行的三個節點建立開發獨立叢集相同的電腦。 完成此安裝之後，您將準備 toocreate 多電腦的叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>建立您的第一個 Service Fabric 獨立叢集
在任何虛擬機器或執行 Windows Server 2012 R2 或 Windows Server 2016 中，在內部部署電腦上或 hello 雲端中，您可以建立獨立 Service Fabric 叢集。 本快速入門可協助您開發獨立叢集 toocreate 只在幾分鐘內。  當您完成時，您會具備有一個包含三個節點的叢集，其在您可部署應用程式的單一電腦上執行。

## <a name="before-you-begin"></a>開始之前
Service Fabric 會提供安裝套件 toocreate Service Fabric 獨立叢集。  [下載 hello 安裝套件](http://go.microsoft.com/fwlink/?LinkId=730690)。  將解壓縮 hello 安裝 tooa 上的套件資料夾 hello 電腦或虛擬機器您要在其中設定 hello 開發叢集。  hello 內容 hello 安裝套件的詳細說明[這裡](service-fabric-cluster-standalone-package-contents.md)。

hello 叢集系統管理員部署和設定 hello 叢集必須 hello 電腦上具有系統管理員權限。 您無法在網域控制站上安裝 Service Fabric。

## <a name="validate-hello-environment"></a>驗證 hello 環境
hello *TestConfiguration.ps1* hello 獨立封裝中的指令碼作為最佳做法分析程式 toovalidate，是否可供指定的環境上部署叢集。 [部署準備](service-fabric-cluster-standalone-deployment-preparation.md)清單 hello 必要元件與環境需求。 如果您可以建立 hello 開發叢集，請執行 hello 指令碼 tooverify:

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>建立 hello 叢集
數個範例叢集組態檔案會安裝 hello 的安裝封裝。 *ClusterConfig.Unsecure.DevCluster.json*是 hello 最簡單的叢集設定： 在單一電腦上執行的不安全，三個節點叢集。  其他組態檔說明使用 X.509 憑證或 Windows 安全性保護之單一或多重電腦的叢集。  中不需要 toomodify hello 預設組態設定的任何此教學課程中，但透過 hello 組態檔看起來並熟悉 hello 設定。  hello**節點**章節描述 hello hello 叢集中的三個節點： 名稱、 IP 位址，[節點型別、 容錯網域和升級網域](service-fabric-cluster-manifest.md#nodes-on-the-cluster)。  hello**屬性**區段會定義 hello[安全性、 可靠性層級、 收集診斷資訊，以及節點類型的](service-fabric-cluster-manifest.md#cluster-properties)hello 叢集。

此叢集並不安全。  任何人都可以匿名方式連線並執行管理作業，所以一律要使用 X.509 憑證或 Windows 安全性來保護生產叢集。  在叢集建立期間只能設定安全性而且不可能 tooenable 安全性之後建立 hello 叢集。  讀取[安全叢集](service-fabric-cluster-security.md)toolearn 更多關於 Service Fabric 叢集安全性。  

toocreate hello 開發三個節點叢集，請執行 hello *CreateServiceFabricCluster.ps1*從系統管理員 PowerShell 工作階段的指令碼：

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

hello Service Fabric 執行階段封裝會自動下載並安裝在叢集建立的時間。

## <a name="connect-toohello-cluster"></a>Toohello 叢集連線
包含三個節點的開發叢集現在正在執行中。 hello ServiceFabric PowerShell 模組會隨 hello 執行階段。  您可以確認該 hello 叢集正在執行 hello 從同一部電腦或從 hello Service Fabric 執行階段的遠端電腦。  hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet 建立連線 toohello 叢集。   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
請參閱[連接 tooa 安全叢集](service-fabric-connect-to-secure-cluster.md)連接 tooa 叢集的其他範例。 在連接 toohello 叢集中之後, 使用 hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello 叢集和狀態資訊的每個節點中的節點清單。 每個節點的 **HealthState** 應該為「正常」。

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>使用 Service Fabric 總管 中的 hello 叢集以視覺化方式檢視
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 是一個理想的工具，可將叢集視覺化及管理應用程式。  Service Fabric 總管是一項服務執行於 hello 叢集中，您使用瀏覽器瀏覽過存取[http://localhost:19080/總管](http://localhost:19080/Explorer)。 

hello 叢集儀表板提供您的叢集，包括應用程式和節點健全狀況摘要的概觀。 hello 節點檢視會顯示 hello 實體 hello 叢集配置。 對於指定的節點，您可以檢查已經在該節點上部署程式碼的應用程式。

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>移除 hello 叢集
tooremove 叢集中，執行 hello *RemoveServiceFabricCluster.ps1* hello 套件資料夾並傳入 hello 路徑 toohello JSON 組態檔中的 PowerShell 指令碼。 您可以選擇性地指定 hello 刪除 hello 記錄檔的位置。

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

tooremove hello Service Fabric 執行階段從 hello 電腦，執行 hello hello 套件資料夾中的下列 PowerShell 指令碼。

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>後續步驟
既然您已設定開發獨立叢集，請嘗試下列發行項的 hello:
* [設定包含多部電腦的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)並啟用安全性。
* [使用 PowerShell 部署應用程式](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
