---
title: "aaaDefault TEMP 資料夾大小會太小角色 |Microsoft 文件"
description: "雲端服務角色具有有限的 hello TEMP 資料夾的空間。 本文提供一些建議如何 tooavoid 空間用盡。"
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="c59e1-104">雲端服務 Web/背景工作角色的預設 TEMP 資料夾太小</span><span class="sxs-lookup"><span data-stu-id="c59e1-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="c59e1-105">hello 的雲端服務工作者或 web 角色的暫存目錄大小上限為 100 MB，可能會變成完整在某個時間點的預設值。</span><span class="sxs-lookup"><span data-stu-id="c59e1-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="c59e1-106">本文說明如何 tooavoid hello 暫存目錄空間用盡。</span><span class="sxs-lookup"><span data-stu-id="c59e1-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="c59e1-107">為何會用盡空間？</span><span class="sxs-lookup"><span data-stu-id="c59e1-107">Why do I run out of space?</span></span>
<span data-ttu-id="c59e1-108">hello 標準 Windows 環境變數 TEMP 和 TMP 可執行應用程式中的可用 toocode。</span><span class="sxs-lookup"><span data-stu-id="c59e1-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="c59e1-109">TEMP 和 TMP 都會指向大小上限為 100 MB tooa 單一目錄。</span><span class="sxs-lookup"><span data-stu-id="c59e1-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="c59e1-110">儲存此目錄中所有資料都不會保存 hello 雲端服務; hello 生命週期裡如果雲端服務中的 hello 角色執行個體被回收時，會清除 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="c59e1-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="c59e1-111">建議 toofix hello 問題</span><span class="sxs-lookup"><span data-stu-id="c59e1-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="c59e1-112">實作其中一個 hello 下列替代項目：</span><span class="sxs-lookup"><span data-stu-id="c59e1-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="c59e1-113">設定本機儲存資源並直接加以存取，而不要使用 TEMP 或 TMP。</span><span class="sxs-lookup"><span data-stu-id="c59e1-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="c59e1-114">執行您的應用程式呼叫 hello 內的程式碼中的本機儲存體資源 tooaccess [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="c59e1-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="c59e1-115">設定一個本機儲存體資源，並指向 hello TEMP 和 TMP 目錄 toopoint toohello hello 本機儲存體資源路徑。</span><span class="sxs-lookup"><span data-stu-id="c59e1-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="c59e1-116">應該執行這項修改內 hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="c59e1-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="c59e1-117">hello 下列程式碼範例示範如何 toomodify hello TEMP 和 TMP 從 hello OnStart 方法內目標目錄：</span><span class="sxs-lookup"><span data-stu-id="c59e1-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c59e1-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c59e1-118">Next steps</span></span>
<span data-ttu-id="c59e1-119">閱讀部落格說明[tooincrease 如何 hello hello Azure Web 角色 ASP.NET 暫存資料夾的大小](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c59e1-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="c59e1-120">檢視更多雲端服務的 [疑難排解文章](/?tag=top-support-issue&product=cloud-services) 。</span><span class="sxs-lookup"><span data-stu-id="c59e1-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="c59e1-121">toolearn 如何使用 Azure PaaS 電腦診斷資料，會發出 tootroubleshoot 雲端服務角色檢視[Kevin Williamson 部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c59e1-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
