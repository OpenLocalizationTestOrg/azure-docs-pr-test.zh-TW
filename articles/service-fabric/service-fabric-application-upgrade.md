---
title: "aaaService Fabric 應用程式升級 |Microsoft 文件"
description: "本文章提供簡介 tooupgrading Service Fabric 應用程式，包括選擇升級模式和執行健全狀況檢查。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>Service Fabric 應用程式升級
Azure Service Fabric 應用程式是服務集合。 在升級期間，Service Fabric 比較新的 hello[應用程式資訊清單](service-fabric-application-model.md#describe-an-application)的 hello 舊版本，並判斷哪些服務 hello 應用程式中的需要更新。 Service Fabric 比較 hello 版本 hello 服務中的數字資訊清單與 hello hello 前一版中的版本號碼。 如果服務未變更，則該服務不會升級。

## <a name="rolling-upgrades-overview"></a>輪流升級概觀
在循環的應用程式升級中，分階段執行 hello 升級。 在每個階段中，hello 升級已套用的 tooa hello 叢集中稱為更新網域的節點子集。 如此一來，hello 應用程式仍可在整個 hello 升級。 Hello 在升級期間，hello 叢集可能包含混合的 hello 舊的和新的版本。

基於這個原因，hello 兩個版本必須向前和向後相容。 如果不相容，hello 應用程式系統管理員是負責執行多個階段升級 toomaintain 可用性。 在多個階段升級中，hello 第一個步驟 tooan hello 與 hello 舊版本相容的應用程式的中繼版本升級。 hello 第二個步驟就是 tooupgrade hello 最終版本會中斷與 hello 更新前版本，相容性，但與 hello 中繼版本相容。

當您設定 hello 叢集 hello 叢集資訊清單中指定更新網域。 更新網域不會以特定順序收到更新。 更新網域是應用程式的部署邏輯單元。 更新網域允許 hello 服務 tooremain 高可用性時，在升級期間。

如果 hello 升級套用的 tooall hello 叢集中節點，也就是 hello 案例 hello 應用程式必須只有一個更新網域時，非輪流升級可能會。 不建議這種方法，因為 hello 服務中斷，且在升級 hello 時無法使用。 此外，當叢集僅以一個更新網域進行設定時，Azure 不提供任何保證。

## <a name="health-checks-during-upgrades"></a>升級期間的健康狀態檢查
進行升級時，健全狀況原則已設定的 toobe （或可能會使用預設值）。 升級稱為成功時將所有更新網域都升級 hello 內指定逾時、 且時所有更新網域會被視為狀況良好。  狀況良好的更新網域會表示該 hello 更新網域傳送 hello 健康原則中指定的所有 hello 健康情況檢查。 例如，健康狀態原則可能會要求應用程式執行個體中的所有服務都必須 *健康狀態良好*，如 Service Fabric 定義的健康狀況。

Service Fabric 在升級期間進行的健康狀態原則以及檢查不限於服務和應用程式。 也就是說，不會完成任何服務專屬的測試。  例如，您的服務可能會有的輸送量需求，但服務網狀架構並沒有 hello 資訊 toocheck 輸送量。 請參閱 toohello[健全狀況的發行項](service-fabric-health-introduction.md)的 hello 所執行的檢查。 hello 檢查是否已啟動 hello 執行個體，可能發生的 hello 應用程式套件是否正確，複製升級包含測試，依此類推。

hello 應用程式健全狀況是彙總的 hello 子實體的 hello 應用程式。 簡單地說，Service Fabric 評估 hello hello 透過 hello 健全狀況所報告的 hello 應用程式的應用程式的健全狀況。 它也會評估 hello hello 應用程式的所有 hello 服務的健全狀況這種方式。 Service Fabric 進一步評估 hello 應用程式服務的 hello 健全狀況及其子系，例如 hello 服務複本 hello 健全狀況彙總。 一旦符合 hello 應用程式健全狀況原則，hello 升級可以繼續。 如果違反 hello 健全狀況原則，hello 應用程式升級失敗。

## <a name="upgrade-modes"></a>升級模式
我們建議您針對應用程式升級的 hello 模式是 hello 監視模式，也就是 hello 常用的模式。 受監視的模式執行 hello 升級一個更新網域上，如果所有健康情況檢查通過 （每個指定 hello 原則），自動將移 toohello 下一個更新網域上。  如果健全狀況檢查失敗且/或達到逾時，hello 升級或是回復 hello 更新網域，或 hello 模式為 已變更的 toounmonitored 手動。 您可以設定 hello 升級 toochoose 失敗升級這些兩種模式之一。 

未受監視的手動模式會在每個更新網域上的升級、 tookick 關閉 hello hello 下一個更新網域升級之後需要手動介入。 系統不會執行任何 Service Fabric 健康狀態檢查。 hello 系統管理員會執行開始 hello 下一個更新網域中的 hello 升級之前的 hello 健全狀況或狀態檢查。

## <a name="upgrade-default-services"></a>升級預設服務
Hello 應用程式的升級程序期間，您可以升級 Service Fabric 應用程式中的預設服務。 預設的服務定義中 hello[應用程式資訊清單](service-fabric-application-model.md#describe-an-application)。 升級預設服務的 hello 標準規則如下：

1. 預設服務在新的 hello[應用程式資訊清單](service-fabric-application-model.md#describe-an-application)hello 叢集中不存在，會建立。
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) toobe 需要設定下列規則 tootrue tooenable hello。 從 v5.5 可支援此功能。

2. 會更新在上一個[應用程式資訊清單](service-fabric-application-model.md#describe-an-application)及新版本中的預設服務。 在 hello 新版本的服務描述會覆寫已經在 hello 叢集。 在更新預設服務失敗時，應用程式升級會自動回復。
3. 預設服務在上一個 hello[應用程式資訊清單](service-fabric-application-model.md#describe-an-application)但是會刪除不在 hello 新版本。 **請注意，無法還原此刪除預設服務。**

如果應用程式的升級回復，預設服務開始升級之前，就會是還原的 toohello 狀態。 但永遠無法建立已刪除的服務。

## <a name="application-upgrade-flowchart"></a>應用程式升級流程圖
遵循本段 hello 流程圖可協助您了解 hello Service Fabric 應用程式的升級程序。 Hello 流程特別的是，描述如何 hello 逾時、 包括*HealthCheckStableDuration*， *HealthCheckRetryTimeout*，和*UpgradeHealthCheckInterval*，當一個更新網域中的 hello 升級被視為成功或失敗時，協助控制。

![hello Service Fabric 應用程式的升級程序][image]

## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。

[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。

使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。

讓應用程式升級相容所學習如何 toouse[資料序列化](service-fabric-application-upgrade-data-serialization.md)。

了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。

藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
