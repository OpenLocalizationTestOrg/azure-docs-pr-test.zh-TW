---
title: "關於 Azure Service Fabric 支援選項 aaaLearn |Microsoft 文件"
description: "Azure Service Fabric 叢集版本支援，以及連結 toofile 支援票證"
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 42394e2cd9dad2040d37d3a2ff3600ee040d8720
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-support-options"></a>Azure Service Fabric 支援選項

上 toodeliver hello 適當叢集的支援您 Service Fabric 執行您的應用程式工作負載，我們已設定為您的各種選項。 根據 hello 的支援層級所需，且 hello hello 問題嚴重性，您 toopick hello 正確的選項。 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>報告實際執行或即時網站問題，或要求 Azure 的付費支援

對於報告 Azure 上部署的 Service Fabric 叢集的即時網站問題，在 [Azure 入口網站](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)或[Microsoft 支援網站](http://support.microsoft.com/oas/default.aspx?prid=16146)開啟專業支援的票證。

深入了解：
 
- [Microsoft 對於 Azure 的專業支援](https://azure.microsoft.com/en-us/support/plans/?b=16.44)。
- [Microsoft 頂級支援](https://support.microsoft.com/en-us/premier)。

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>報告實際執行或即時網站問題，或要求獨立 Service Fabric 叢集的付費支援

對於報告內部部署或其他雲端上部署的 Service Fabric 叢集的即時網站問題，在 [Microsoft 支援入口網站](http://support.microsoft.com/oas/default.aspx?prid=16146)開啟專業支援的票證。

深入了解：

- [Microsoft 對於內部部署的專業支援](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0)。
- [Microsoft 頂級支援](https://support.microsoft.com/en-us/premier)。


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>報告 Azure Service Fabric 問題 
我們已設定 GitHub 存放庫以報告 Service Fabric 問題。  我們也會主動監視 hello 遵循論壇。

### <a name="github-repo"></a>GitHub 存放庫 
在 [Service-Fabric-issues git 存放庫](https://github.com/Azure/service-fabric-issues)上報告 Azure Service Fabric 問題。 此存放庫適用於報告和追蹤 Azure Service Fabric 的問題，並進行小規模的功能要求。 **請勿的使用這個 tooreport 即時網站問題**。

### <a name="stackoverflow-and-msdn-forums"></a>StackOverflow 和 MSDN 論壇

hello [Service Fabric 標記在 StackOverflow 上的][ stackoverflow]和 hello [MSDN 上的 Service Fabric 論壇][ msdn-forum]是最佳使用詢問有關的問題hello 平台的運作方式以及如何您可能會完成它的某些工作。

### <a name="azure-feedback-forum"></a>Azure 意見反應論壇

hello [Azure 意見反應論壇，適用於 Service Fabric] [ uservoice-forum]是當我們檢閱 hello 最受歡迎的要求有 hello 產品的大功能構想是我們中型 toolong 詞彙的一部分送出 hello 最佳位置計劃。 我們建議您針對您的意見 hello 社群內 toorally 支援。


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>支援的 Service Fabric 版本。

請確定您的叢集一律執行支援的 Service Fabric 版本。 因為，當我們宣佈 hello 發行新版的 Service Fabric hello 舊版標示為的支援即將結束後的 60 天內從該日期的最小值。 hello 新的版本上經過宣布[hello Service Fabric 小組部落格上](https://blogs.msdn.microsoft.com/azureservicefabric/)。

請參閱下列文件上的方式的詳細資訊的 toohello tookeep 您執行受支援的 Service Fabric 版本的叢集。

- [在 Azure 叢集上升級 Service Fabric 版本](service-fabric-cluster-upgrade.md)
- [在獨立 Windows 伺服器叢集上升級 Service Fabric 版本](service-fabric-cluster-upgrade-windows-server.md)
 
以下是支援的 hello Service Fabric 版本 hello 清單以及其支援結束日期。

| **Service Fabric 執行階段叢集** | **相容的 SDK / NuGet 套件版本** | **結束支援日期** |
| --- | --- | --- |
| 所有叢集版本先前 too5.3.121 |小於或等於 tooversion 2.3 |2017 年 1 月 20 日 |
| 5.3.* |小於或等於 tooversion 2.3 |2017 年 2 月 24 日 |
| 5.4.* |小於或等於 tooversion 2.4 |2017 年 5 月 10 日     |
| 5.5.* |小於或等於 tooversion 2.5 |2017 年 8 月 10 日    |
| 5.6.* |小於或等於 tooversion 2.6 |2017 年 10 月 13 日    |
| 5.7.* |小於或等於 tooversion 2.7 |目前版本，沒有結束日期

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Service Fabric 預覽版本 - 不支援用於生產環境。
從時間 tootime 我們發行任何重要功能我們想意見反應，會以預覽發行的版本。 這些預覽版本只能用於測試目的。 您的生產叢集應一律執行支援的穩定 Service Fabric 版本。 預覽版本一律從 255 作為主要和次要版本號碼的開頭。 比方說，如果您看到 Service Fabric 版本 255.255.5703.949，該發行版本是唯一 toobe 用於測試叢集，而且目前處於預覽狀態。 這些發行前版本也會宣告於 hello [Service Fabric 團隊部落格](https://blogs.msdn.microsoft.com/azureservicefabric)來處理，而且對包含 hello 功能的詳細資料。

這些預覽版本沒有付費的支援選項。 使用其中一個下所列的 hello 選項[報表 Azure Service Fabric 發出](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues)tooask 問題或提供意見反應。

## <a name="next-steps"></a>後續步驟

- [在 Azure 叢集上升級 Service Fabric 版本](service-fabric-cluster-upgrade.md)
- [在獨立 Windows 伺服器叢集上升級 Service Fabric 版本](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
