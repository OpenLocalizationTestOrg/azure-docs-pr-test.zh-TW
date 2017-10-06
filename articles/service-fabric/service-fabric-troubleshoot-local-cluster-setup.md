---
title: "aaaTroubleshoot 您本機的 Service Fabric 叢集設定 |Microsoft 文件"
description: "本文涵蓋了一組疑難排解本機開發叢集的建議"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>疑難排解本機開發叢集設定
如果您的本機 Azure Service Fabric 開發叢集進行互動時遇到問題，請檢閱下列可能的解決方案的建議 hello。

## <a name="cluster-setup-failures"></a>叢集設定失敗
### <a name="cannot-clean-up-service-fabric-logs"></a>無法清除 Service Fabric 記錄檔
#### <a name="problem"></a>問題
在執行 hello DevClusterSetup 指令碼時，您會看到類似錯誤：

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>方案
關閉 hello 目前的 PowerShell 視窗，並開啟新的 PowerShell 視窗，以系統管理員。 您現在應該能夠 toosuccessfully 執行 hello 指令碼。

## <a name="cluster-connection-failures"></a>叢集連接失敗
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>在 Azure PowerShell 中無法辨識 Service Fabric PowerShell Cmdlet
#### <a name="problem"></a>問題
如果您嘗試 toorun 任何 hello Service Fabric PowerShell cmdlet，例如`Connect-ServiceFabricCluster`在 Azure PowerShell 視窗中，失敗，指出無法辨識該 hello 指令程式。 hello 這個錯誤的原因是，Azure PowerShell，將會使用 hello 32 位元版本的 Windows PowerShell （即使在 64 位元作業系統的版本），而 hello Service Fabric cmdlet 只能在 64 位元環境中運作。

#### <a name="solution"></a>方案
一律直接從 Windows PowerShell 執行 Service Fabric Cmdlet。

> [!NOTE]
> hello 最新版本的 Azure PowerShell 不會建立特殊的捷徑，因此這不會再出現。
> 
> 

### <a name="type-initialization-exception"></a>類型初始化例外狀況
#### <a name="problem"></a>問題
當您要連接 toohello 叢集在 PowerShell 中的時，您會看到如 System.Fabric.Common.AppTrace hello 錯誤 TypeInitializationException。

#### <a name="solution"></a>方案
在安裝期間未正確設定路徑變數。 登出 Windows，再重新登入。 這會重新整理您的路徑。

### <a name="cluster-connection-fails-with-object-is-closed"></a>叢集連接失敗，且出現「物件已關閉」
#### <a name="problem"></a>問題
呼叫 tooConnect ServiceFabricCluster 失敗，錯誤如下：

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>方案
關閉 hello 目前的 PowerShell 視窗，並開啟新的 PowerShell 視窗，以系統管理員。 您現在應該可以 toosuccessfully 連接。

### <a name="fabric-connection-denied-exception"></a>拒絕網狀架構連線例外狀況
#### <a name="problem"></a>問題
從 Visual Studio 進行偵錯時，看見 FabricConnectionDeniedException 錯誤。

#### <a name="solution"></a>方案
當您嘗試 toostart 服務主機處理序以手動方式，而不是允許 hello Service Fabric 執行階段 toostart，通常會發生此錯誤會針對您。

請確定您的解決方法中沒有任何設定為啟始專案的服務專案。 只有 Service Fabric 應用程式專案才可設為啟始專案。

> [!TIP]
> 如果安裝程式，您的本機叢集開始 toobehave 異常，您可以重設使用 hello 本機叢集管理員 」 系統匣應用程式。 此移除 hello 現有的叢集，並設定新的。 請注意，所有已部署的應用程式和相關聯的資料都會被移除。
> 
> 

## <a name="next-steps"></a>後續步驟
* [透過系統健康情況報告了解及疑難排解您的叢集](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [使用 Service Fabric 總管視覺化叢集](service-fabric-visualizing-your-cluster.md)

