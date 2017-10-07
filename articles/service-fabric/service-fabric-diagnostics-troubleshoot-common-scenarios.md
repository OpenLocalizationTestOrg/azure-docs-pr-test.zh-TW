---
title: "與事件追蹤 aaaTroubleshooting |Microsoft 文件"
description: "hello 在 Microsoft Azure Service Fabric 上部署服務時遇到最常見的問題。"
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>針對您在 Azure Service Fabric 上部署服務時的常見問題進行疑難排解
如果您開發人員電腦上執行服務，它是簡單 toouse [Visual Studio 的偵錯工具](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。 對於遠端叢集，[健康情況報告](service-fabric-view-entities-aggregated-health.md)永遠是很好的起點 toostart。 hello 這些報表是透過 PowerShell 的最簡單方式 tooaccess 或[SFX](service-fabric-visualizing-your-cluster.md)。 本文假設您正在偵錯遠端叢集，且有基本的了解如何 toouse 任一種工具。

## <a name="application-crash"></a>應用程式損毀
hello"分割低於目標複本或執行個體計數 」 報表會清楚指出您的服務所引起。 toofind 出在損毀您的服務會進行一些更多調查。 當大規模執行服務時，最好有一套詳實的追蹤資料。  我們建議您嘗試[Azure 診斷](service-fabric-diagnostics-how-to-setup-wad.md)來收集這些追蹤，並使用像是方案[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)來檢視和搜尋 hello 追蹤。

![SFX 資料分割健康情況](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>在服務或動作項目初始化期間
初始化 hello 服務類型之前的任何例外狀況會導致 hello 程序 toocrash。 這些類型的損毀，hello 應用程式事件記錄檔會顯示 hello 錯誤從您的服務。
初始化 hello 服務之前，這些是最常見的例外狀況 toosee hello。

System.IO.FileNotFoundException

此錯誤通常是因為 toomissing 組件相依性。 請檢查 hello CopyLocal 屬性在 Visual Studio 或 hello 全域組件快取中的 hello 節點。

***System.Runtime.InteropServices.COMException*** *在 System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory （IntPtr、 IFabricStatefulServiceFactory）*

 這表示該 hello 註冊的服務型別名稱與 hello 服務資訊清單不相符。

[Azure 診斷](service-fabric-diagnostics-how-to-setup-wad.md)可以自動為您的所有節點設定的 tooupload hello 應用程式事件日誌。

### <a name="runasync-or-onactivateasync"></a>RunAsync() 或 OnActivateAsync()
如果在 hello 初始化期間發生 hello 當機或執行您已註冊的服務型別或動作項目，hello 攔截的例外狀況將被 Azure Service Fabric。 您可以檢視這些提供者 hello EventSource hello 「 後續步驟 」 一節所述。

## <a name="next-steps"></a>後續步驟
深入了解 Service Fabric 所提供的現有診斷：

* [Reliable Actors 項目診斷](service-fabric-reliable-actors-diagnostics.md)
* [Reliable Services 診斷](service-fabric-reliable-services-diagnostics.md)

