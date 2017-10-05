---
title: "預設 TEMP 資料夾對角色而言太小 | Microsoft Docs"
description: "雲端服務角色的 TEMP 資料夾空間量有限。 本文提供關於如何避免用盡空間的一些建議。"
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
ms.openlocfilehash: 577d090a009eb2331b401273257c7cc7c1eea772
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="9c1b4-104">雲端服務 Web/背景工作角色的預設 TEMP 資料夾太小</span><span class="sxs-lookup"><span data-stu-id="9c1b4-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="9c1b4-105">雲端服務背景工作角色或 Web 角色的預設暫存目錄大小上限為 100 MB，可能會在某個時間點達到。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="9c1b4-106">本文說明如何避免用盡暫存目錄的空間。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="9c1b4-107">為何會用盡空間？</span><span class="sxs-lookup"><span data-stu-id="9c1b4-107">Why do I run out of space?</span></span>
<span data-ttu-id="9c1b4-108">您應用程式中執行的程式碼可以使用標準 Windows 環境變數 TEMP 和 TMP。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="9c1b4-109">TEMP 和 TMP 都會指向大小上限為 100 MB 的單一目錄。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="9c1b4-110">任何儲存在此目錄中的資料都不會跨雲端服務的生命週期而保存；如果雲端服務中的角色執行個體被回收，就會清除目錄。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="9c1b4-111">修正此問題的建議</span><span class="sxs-lookup"><span data-stu-id="9c1b4-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="9c1b4-112">實作下列其中一個替代方案：</span><span class="sxs-lookup"><span data-stu-id="9c1b4-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="9c1b4-113">設定本機儲存資源並直接加以存取，而不要使用 TEMP 或 TMP。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="9c1b4-114">若要從您應用程式內執行的程式碼存取本機儲存資源，請呼叫 [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="9c1b4-115">設定本機儲存資源，並將 TEMP 和 TMP 目錄指向本機儲存資源的路徑。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="9c1b4-116">此修改應在 [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) 方法內執行。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="9c1b4-117">下列程式碼範例說明如何在 OnStart 方法內修改 TEMP 和 TMP 的目標目錄：</span><span class="sxs-lookup"><span data-stu-id="9c1b4-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
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

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="9c1b4-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c1b4-118">Next steps</span></span>
<span data-ttu-id="9c1b4-119">請參閱說明 [如何增加 Azure Web 角色 ASP.NET 暫存資料夾大小](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx)的部落格。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="9c1b4-120">檢視更多雲端服務的 [疑難排解文章](/?tag=top-support-issue&product=cloud-services) 。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="9c1b4-121">若要了解如何利用 Azure PaaS 電腦診斷資料，對雲端服務角色的問題進行疑難排解，請檢視 [Kevin Williamson 的部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9c1b4-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
