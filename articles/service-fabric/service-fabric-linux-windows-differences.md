---
title: "Linux 和 Windows 之間的差異 aaaAzure Service Fabric |Microsoft 文件"
description: "在 Windows Azure Service Fabric hello on Linux 的 Azure 服務網狀架構預覽之間的差異。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a>Linux (預覽) 和 Windows (正式推出) 上 Service Fabric 之間的差異

由於 Linux 上的 Service Fabric 是預覽，有一些 Windows 上支援的功能在 Linux 上尚未支援。 最後，hello 功能集，會在同位在 Linux 上的 Service Fabric 正式推出時。 在即將推出的版本中，兩者間的功能差異會減少。 hello 下列之間存在差異 hello 最新可用版本 (也就是在 Windows 和 Linux 上的 5.5 版上 5.6 版本之間): 

* 可靠的集合 (和可靠的具狀態服務) 
* ReverseProxy 
* 獨立安裝程式 
* 資訊清單檔案的 XML 結構描述驗證 
* 主控台重新導向 
* hello 錯誤 Analysis Service (FAS)
* 容器的 Docker Compose 和磁碟區與記錄驅動程式 
* 容器和服務的資源管理 
* DNS 服務
* Azure Active Directory 支援
* 某些 Powershell 命令的對等 CLI 命令 
* 針對 Linux 叢集 （如展開 hello 下一節），可以執行 Powershell 命令的子集。

>[!NOTE]
>在生產環境叢集中不支援主控台重新導向，即使是在 Windows 上亦然。

Windows 與 Linux 上的開發工具也不同。 在 Windows 上使用 VisualStudio、Powershell、VSTS 和 ETW，而在 Linux 上使用 Yeoman、Eclipse、Jenkins 和 LTTng。

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a>無法針對 Linux Service Fabric 叢集運作的 Powershell Cmdlet

* Invoke-ServiceFabricChaosTestScenario
* Invoke-ServiceFabricFailoverTestScenario
* Invoke-ServiceFabricPartitionDataLoss
* Invoke-ServiceFabricPartitionQuorumLoss
* Restart-ServiceFabricPartition
* Start-ServiceFabricNode
* Stop-ServiceFabricNode
* Get-ServiceFabricImageStoreContent
* Get-ServiceFabricChaosReport
* Get-ServiceFabricNodeTransitionProgress
* Get-ServiceFabricPartitionDataLossProgress
* Get-ServiceFabricPartitionQuorumLossProgress
* Get-ServiceFabricPartitionRestartProgress
* Get-ServiceFabricTestCommandStatusList
* Remove-ServiceFabricTestState
* Start-ServiceFabricChaos
* Start-ServiceFabricNodeTransition
* Start-ServiceFabricPartitionDataLoss
* Start-ServiceFabricPartitionQuorumLoss
* Start-ServiceFabricPartitionRestart
* Stop-ServiceFabricChaos
* Stop-ServiceFabricTestCommand
* Cmd
* Get-ServiceFabricNodeConfiguration
* Get-ServiceFabricClusterConfiguration
* Get-ServiceFabricClusterConfigurationUpgradeStatus
* Get-ServiceFabricPackageDebugParameters
* New-ServiceFabricPackageDebugParameter
* New-ServiceFabricPackageSharingPolicy
* Add-ServiceFabricNode
* Copy-ServiceFabricClusterPackage
* Get-ServiceFabricRuntimeSupportedVersion
* Get-ServiceFabricRuntimeUpgradeVersion
* New-ServiceFabricCluster
* New-ServiceFabricNodeConfiguration
* Remove-ServiceFabricCluster
* Remove-ServiceFabricClusterPackage
* Remove-ServiceFabricNodeConfiguration
* Test-ServiceFabricClusterManifest
* Test-ServiceFabricConfiguration
* Update-ServiceFabricNodeConfiguration
* Approve-ServiceFabricRepairTask
* Complete-ServiceFabricRepairTask
* Get-ServiceFabricRepairTask
* Invoke-ServiceFabricDecryptText
* Invoke-ServiceFabricEncryptSecret
* Invoke-ServiceFabricEncryptText
* Invoke-ServiceFabricInfrastructureCommand
* Invoke-ServiceFabricInfrastructureQuery
* Remove-ServiceFabricRepairTask
* Start-ServiceFabricRepairTask
* Stop-ServiceFabricRepairTask
* Update-ServiceFabricRepairTaskHealthPolicy



## <a name="next-steps"></a>後續步驟
* [在 Linux 上準備您的開發環境](service-fabric-get-started-linux.md)
* [在 OSX 上準備您的開發環境](service-fabric-get-started-mac.md)
* [使用 Yeoman 在 Linux 上建立和部署第一個 Service Fabric Java 應用程式](service-fabric-create-your-first-linux-application-with-java.md)
* [在 Linux 上使用適用於 Eclipse 的 Service Fabric 外掛程式建立和部署第一個 Service Fabric Java 應用程式](service-fabric-get-started-eclipse.md)
* [在 Linux 上建立第一個 CSharp 應用程式](service-fabric-create-your-first-linux-application-with-csharp.md)
* [使用 hello 服務網狀架構 CLI toomanage 您應用程式](service-fabric-application-lifecycle-sfctl.md)
