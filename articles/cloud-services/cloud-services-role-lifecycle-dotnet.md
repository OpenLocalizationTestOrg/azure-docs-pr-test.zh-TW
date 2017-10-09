---
title: "aaaHandle 雲端服務生命週期事件 |Microsoft 文件"
description: "了解如何使用雲端服務角色的 hello 存留週期方法，在.NET 中"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>自訂 hello.NET 中的 Web 或背景工作角色的生命週期
當您建立背景工作角色時，您必須擴充 hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx)類別可提供方法讓您可讓您的 toooverride 回應 toolifecycle 事件。 Web 角色的這個類別是選擇性的因此您必須使用它 toorespond toolifecycle 事件。

## <a name="extend-hello-roleentrypoint-class"></a>擴充 hello RoleEntryPoint 類別
hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx)類別包括 Azure 所呼叫的方法時它**啟動**，**執行**，或**停止**web 或背景工作角色。 您選擇可以覆寫這些方法 toomanage 角色初始化、 角色關機順序或 hello hello 角色的執行緒。 

在擴充**RoleEntryPoint**，您應留意下列 hello 方法的行為的 hello:

* hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx)和[OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)方法會傳回布林值，因此您很可能 tooreturn **false**這些方法。
  
   如果您的程式碼傳回**false**hello 角色程序會突然終止，但不執行任何關閉程序中，您可能必須在位置。 一般情況下，您應該避免傳回**false**從 hello **OnStart**方法。
* **RoleEntryPoint** 方法多載中未能攔截的任何例外狀況，都會被視為未處理的例外狀況。
  
   其中一個 hello 存留週期方法內發生的例外狀況，Azure 會引發 hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx)事件，然後終止 hello 程序。 您的角色離線之後，Azure 將重新啟動該角色。 當未處理的例外狀況發生時，hello[停止](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx)事件就不會引發，和 hello **OnStop**不會呼叫方法。

如果您的角色未啟動，或 hello 初始化、 忙碌和停止狀態之間循環您的程式碼可能會擲回未處理的例外狀況，其中每個時間 hello 角色重新啟動的 hello 生命週期事件內。 在此情況下，使用 hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx)事件 toodetermine hello hello 例外狀況的原因並加以適當地處理。 您的角色也可能會傳回從 hello[執行](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法，導致 hello 角色 toorestart。 如需部署狀態的詳細資訊，請參閱[一般問題的原因角色 tooRecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)。

> [!NOTE]
> 如果您使用 hello **Azure Tools for Microsoft Visual Studio** toodevelop 應用程式 hello 角色專案範本會自動擴充 hello **RoleEntryPoint**類別，在 hello *WebRole.cs*和*WorkerRole.cs*檔案。
> 
> 

## <a name="onstart-method"></a>OnStart 方法
hello **OnStart**角色執行個體在 Azure 中有不同的回到線上時，呼叫方法。 Hello 角色執行個體 hello OnStart 程式碼執行時，會標示為**忙碌**任何外部流量將會導向的 tooit hello 負載平衡器。 您可以覆寫此方法 tooperform 初始化工作，例如實作事件處理常式及啟動[Azure 診斷](cloud-services-how-to-monitor.md)。

如果**OnStart**傳回**true**、 hello 執行個體已成功初始化，且 Azure 會呼叫 hello **RoleEntryPoint.Run**方法。 如果**OnStart**傳回**false**，hello 角色，立即結束，而不執行任何計劃的關機順序。

hello 下列程式碼範例顯示如何 toooverride hello **OnStart**方法。 這個方法會設定並啟動診斷監視器時 hello 角色執行個體啟動，並且設定傳輸記錄資料 tooa 儲存體帳戶：

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>OnStop 方法
hello **OnStop**離線之後，角色執行個體已由 Azure 和 hello 處理序結束之前，呼叫方法。 您可以覆寫此方法的 toocall 程式碼所需的關閉您角色執行個體 toocleanly。

> [!IMPORTANT]
> 在 hello 中執行的程式碼**OnStop**方法具有有限的時間 toofinish 以外的使用者起始關機的原因而呼叫時。 這段時間之後，hello 程序即會終止，因此您必須確定該程式碼中 hello **OnStop**方法可快速地執行或容許中斷 toocompletion 未執行。 hello **OnStop**方法呼叫之後 hello**停止**就會引發事件。
> 
> 

## <a name="run-method"></a>Run 方法
您可以覆寫 hello**執行**方法 tooimplement 角色執行個體長時間執行的執行緒。

覆寫 hello**執行**方法並非必要; hello 的預設實作會啟動永久處於睡眠狀態的執行緒。 如果您不要覆寫 hello**執行**方法，您的程式碼應無限期地封鎖。 如果 hello**執行**方法傳回時，會自動地正常回收 hello 角色; 換句話說，Azure 會引發 hello**停止**事件並呼叫 hello **OnStop**方法讓hello 角色離線之前，會先執行關機順序。

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Web 角色的實作 hello ASP.NET 存留週期方法
您可以使用 hello ASP.NET 存留週期方法，除了 toothose 提供 hello **RoleEntryPoint**類別，為 web 角色的 toomanage 初始化及關機順序。 如果您要移植現有的 ASP.NET 應用程式 tooAzure，這可能是適用於相容性用途。 hello ASP.NET 存留週期方法從呼叫 hello 內**RoleEntryPoint**方法。 hello**應用程式\_啟動**方法呼叫之後 hello **RoleEntryPoint.OnStart**方法完成。 hello**應用程式\_結束**方法 hello 之前呼叫**Application_end**方法呼叫。

## <a name="next-steps"></a>後續步驟
了解如何太[建立雲端服務封裝](cloud-services-model-and-package.md)。

