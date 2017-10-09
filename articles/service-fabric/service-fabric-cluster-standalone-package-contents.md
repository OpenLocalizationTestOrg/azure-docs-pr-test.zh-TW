---
title: "適用於 Windows Server 的 Service Fabric 獨立封裝 aaaAzure |Microsoft 文件"
description: "描述與 Windows Server 的 hello Azure Service Fabric 獨立封裝的內容。"
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>適用於 Windows Server 的 Service Fabric 獨立封裝內容
在 hello[下載](http://go.microsoft.com/fwlink/?LinkId=730690)服務網狀架構的獨立套件，您會發現下列檔案的 hello:

| **檔案名稱** | **簡短說明** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |建立 hello 叢集使用 hello 設定，如此 PowerShell 指令碼。 |
| RemoveServiceFabricCluster.ps1 |PowerShell 指令碼移除使用如此 hello 設定的叢集。 |
| AddNode.ps1 |新增節點 tooan 現有的 PowerShell 指令碼部署的 hello 目前電腦上的叢集。 |
| RemoveNode.ps1 |移除節點，從現有的 PowerShell 指令碼部署 hello 目前電腦的叢集。 |
| CleanFabric.ps1 |清理獨立關閉 hello 目前機器 Service Fabric 安裝 PowerShell 指令碼。 先前的 MSI 安裝應該以本身相關聯的解除安裝程式來移除。 |
| TestConfiguration.ps1 |PowerShell 指令碼來分析 hello hello Cluster.json 中所指定的基礎結構。 |
| DownloadServiceFabricRuntimePackage.ps1 |PowerShell 指令碼以供下載 hello 最新版執行階段封裝超出訊號範圍，為的情況下部署機器 hello 不連線 toohello 網際網路。 |
| DeploymentComponentsAutoextractor.exe |自我解壓縮的封存包含部署元件使用 hello 獨立封裝的指令碼。 |
| EULA_ENU.txt |使用 Microsoft Azure Service Fabric 獨立 Windows Server 封裝 hello hello 授權條款。 您可以[下載一份 hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084)現在。 |
| Readme.txt |連結 toohello 版本資訊和基本安裝指示。 它是此文件中的 hello 指示的子集。 |
| ThirdPartyNotice.rtf |請注意一個 hello 套件中的協力廠商軟體。 |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |StandaloneLogCollector.exe 需求 toocollect 和上傳的追蹤上執行記錄 tooMicrosoft 支援用途。 |
| Tools\ServiceFabricUpdateService.zip |工具會將 tooenable 自動程式碼升級用於叢集且沒有網際網路存取權。 在 [這裡](service-fabric-cluster-upgrade-windows-server.md)|

**範本** 
| **檔案名稱** | **簡短說明** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |叢集組態範例檔包含不安全，三個節點，單一電腦 （或虛擬機器） 開發叢集，包括每個節點的 hello 資訊 hello 叢集中的 hello 設定。 |
| ClusterConfig.Unsecure.MultiMachine.json |叢集組態範例檔包含不安全、 多電腦 （或虛擬機器） 的叢集，包括 hello 叢集中的每個機器 hello 資訊 hello 設定。 |
| ClusterConfig.Windows.DevCluster.json |叢集組態範例檔，其中包含所有 hello 設定安全、 三個節點的單一電腦 （或虛擬機器） 開發叢集，包括 hello hello 叢集中的每個節點的資訊。 hello 叢集受到使用[Windows 識別](https://msdn.microsoft.com/library/ff649396.aspx)。 |
| ClusterConfig.Windows.MultiMachine.json |叢集組態範例檔，其中包含使用 Windows 安全性，包括 hello 資訊 hello 安全叢集中每一部電腦的安全、 多電腦 （或虛擬機器） 叢集的所有 hello 設定。 hello 叢集受到使用[Windows 識別](https://msdn.microsoft.com/library/ff649396.aspx)。 |
| ClusterConfig.x509.DevCluster.json |叢集組態範例檔，包含安全、 三個節點，單一電腦 （或虛擬機器） 開發叢集，包括每個節點的 hello 資訊 hello 叢集中的所有 hello 設定。 hello 叢集受到使用 x509 憑證。 |
| ClusterConfig.x509.MultiMachine.json |叢集組態範例檔包含所有 hello hello 設定安全、 多電腦 （或虛擬機器） 的叢集，包括 hello 安全叢集中的每個節點的 hello 資訊。 hello 叢集受到使用 x509 憑證。 |
| ClusterConfig.gMSA.Windows.MultiMachine.json |叢集組態範例檔包含所有 hello hello 設定安全、 多電腦 （或虛擬機器） 的叢集，包括 hello 安全叢集中的每個節點的 hello 資訊。 hello 叢集使用保護[群組受管理的服務帳戶](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx)。 |

## <a name="cluster-configuration-samples"></a>叢集組態範例
叢集組態範本最新版本，請參閱 hello GitHub 頁面：[獨立叢集組態範例](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)。

## <a name="independent-runtime-package"></a>獨立的執行階段套件
hello 最新的執行階段封裝可從叢集部署期間自動下載[下載連結的 Service Fabric 執行階段的 Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)。

## <a name="related"></a>相關參考
* [建立獨立 Azure Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)
* [Service Fabric 叢集安全性案例](service-fabric-windows-cluster-windows-security.md)
