---
title: "雲端服務角色回收的常見原因 | Microsoft Docs"
description: "突然回收的雲端服務角色可能會造成顯著的停機時間。 以下是導致角色回收的一些常見問題，或許有助於縮短停機時間。"
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e55009c72b977ee4a30f6c71043bde483849f78f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="common-issues-that-cause-roles-to-recycle"></a><span data-ttu-id="2fdb8-104">導致角色回收的常見問題</span><span class="sxs-lookup"><span data-stu-id="2fdb8-104">Common issues that cause roles to recycle</span></span>
<span data-ttu-id="2fdb8-105">本文討論部署問題的常見原因，和可協助您解決這些問題的疑難排解秘訣。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-105">This article discusses some of the common causes of deployment problems and provides troubleshooting tips to help you resolve these problems.</span></span> <span data-ttu-id="2fdb8-106">應用程式出現問題的徵候之一，是角色執行個體無法啟動，或是在初始化中、忙碌和停止中狀態之間循環。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-106">An indication that a problem exists with an application is when the role instance fails to start, or it cycles between the initializing, busy, and stopping states.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a><span data-ttu-id="2fdb8-107">遺失執行階段相依性</span><span class="sxs-lookup"><span data-stu-id="2fdb8-107">Missing runtime dependencies</span></span>
<span data-ttu-id="2fdb8-108">如果應用程式中的角色依賴任何不屬於 .NET Framework 或 Azure Managed 程式庫的組件，您必須明確地在應用程式封裝中包含該組件。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-108">If a role in your application relies on any assembly that is not part of the .NET Framework or the Azure managed library, you must explicitly include that assembly in the application package.</span></span> <span data-ttu-id="2fdb8-109">請記住，其他 Microsoft 架構依預設並未在 Azure 上提供。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-109">Keep in mind that other Microsoft frameworks are not available on Azure by default.</span></span> <span data-ttu-id="2fdb8-110">如果您的角色依賴這類架構，您必須將這些組件新增至應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-110">If your role relies on such a framework, you must add those assemblies to the application package.</span></span>

<span data-ttu-id="2fdb8-111">在您建置及封裝應用程式之前，請確認下列項目：</span><span class="sxs-lookup"><span data-stu-id="2fdb8-111">Before you build and package your application, verify the following:</span></span>

* <span data-ttu-id="2fdb8-112">如果使用 Visual studio，請確定您不屬於 Azure SDK 或 .NET Framework 的專案中每個參考的組件，[複製到本機] 屬性都設定為 [True]。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-112">If using Visual studio, make sure the **Copy Local** property is set to **True** for each referenced assembly in your project that is not part of the Azure SDK or the .NET Framework.</span></span>
* <span data-ttu-id="2fdb8-113">確定 web.config 檔案未參考 compilation 元素中任何未使用的組件。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-113">Make sure the web.config file does not reference any unused assemblies in the compilation element.</span></span>
* <span data-ttu-id="2fdb8-114">每個 .cshtml 檔案的 [建置動作] 都設為 [內容]。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-114">The **Build Action** of every .cshtml file is set to **Content**.</span></span> <span data-ttu-id="2fdb8-115">這可確保檔案會正確出現在封裝中，並且讓其他參考的檔案出現在封裝中。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-115">This ensures that the files will appear correctly in the package and enables other referenced files to appear in the package.</span></span>

## <a name="assembly-targets-wrong-platform"></a><span data-ttu-id="2fdb8-116">組件以錯誤的平台作為目標</span><span class="sxs-lookup"><span data-stu-id="2fdb8-116">Assembly targets wrong platform</span></span>
<span data-ttu-id="2fdb8-117">Azure 是 64 位元環境。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-117">Azure is a 64-bit environment.</span></span> <span data-ttu-id="2fdb8-118">因此，針對 32 位元目標編譯的 .NET 組件無法在 Azure 上運作。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-118">Therefore, .NET assemblies compiled for a 32-bit target won't work on Azure.</span></span>

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a><span data-ttu-id="2fdb8-119">角色在初始化或停止時會擲回未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="2fdb8-119">Role throws unhandled exceptions while initializing or stopping</span></span>
<span data-ttu-id="2fdb8-120">[RoleEntryPoint] 類別的方法 (包括 [OnStart]、[OnStop] 和 [Run]) 方法所擲回的任何例外狀況，都是未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-120">Any exceptions that are thrown by the methods of the [RoleEntryPoint] class, which includes the [OnStart], [OnStop], and [Run] methods, are unhandled exceptions.</span></span> <span data-ttu-id="2fdb8-121">如果其中有一個方法發生未處理的例外狀況，角色就會進行回收。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-121">If an unhandled exception occurs in one of these methods, the role will recycle.</span></span> <span data-ttu-id="2fdb8-122">如果角色重複回收，它可能會在每次嘗試啟動時擲回未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-122">If the role is recycling repeatedly, it may be throwing an unhandled exception each time it tries to start.</span></span>

## <a name="role-returns-from-run-method"></a><span data-ttu-id="2fdb8-123">角色因 Run 方法而回收</span><span class="sxs-lookup"><span data-stu-id="2fdb8-123">Role returns from Run method</span></span>
<span data-ttu-id="2fdb8-124">[Run] 方法應該無限期地執行。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-124">The [Run] method is intended to run indefinitely.</span></span> <span data-ttu-id="2fdb8-125">如果您的程式碼覆寫 [Run] 方法，此方法應無限期地停用。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-125">If your code overrides the [Run] method, it should sleep indefinitely.</span></span> <span data-ttu-id="2fdb8-126">如果 [Run] 方法回復，角色即會回收。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-126">If the [Run] method returns, the role recycles.</span></span>

## <a name="incorrect-diagnosticsconnectionstring-setting"></a><span data-ttu-id="2fdb8-127">不正確的 DiagnosticsConnectionString 設定</span><span class="sxs-lookup"><span data-stu-id="2fdb8-127">Incorrect DiagnosticsConnectionString setting</span></span>
<span data-ttu-id="2fdb8-128">如果應用程式使用 Azure 診斷，則您的服務組態檔必須指定 `DiagnosticsConnectionString` 組態設定。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-128">If application uses Azure Diagnostics, your service configuration file must specify the `DiagnosticsConnectionString` configuration setting.</span></span> <span data-ttu-id="2fdb8-129">此設定應指定您在 Azure 中的儲存體帳戶的 HTTPS 連線。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-129">This setting should specify an HTTPS connection to your storage account in Azure.</span></span>

<span data-ttu-id="2fdb8-130">為了在您將應用程式封裝部署至 Azure 之前確保 `DiagnosticsConnectionString` 設定正確無誤，請確認下列事項：</span><span class="sxs-lookup"><span data-stu-id="2fdb8-130">To ensure that your `DiagnosticsConnectionString` setting is correct before you deploy your application package to Azure, verify the following:</span></span>  

* <span data-ttu-id="2fdb8-131">`DiagnosticsConnectionString` 設定指向 Azure 中的有效儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-131">The `DiagnosticsConnectionString` setting points to a valid storage account in Azure.</span></span>  
  <span data-ttu-id="2fdb8-132">根據預設，此設定會指向模擬儲存體帳戶，因此您必須在部署應用程式封裝之前明確變更這項設定。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-132">By default, this setting points to the emulated storage account, so you must explicitly change this setting before you deploy your application package.</span></span> <span data-ttu-id="2fdb8-133">若未變更此設定，當角色執行個體嘗試啟動診斷監視器時，將會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-133">If you do not change this setting, an exception is thrown when the role instance attempts to start the diagnostic monitor.</span></span> <span data-ttu-id="2fdb8-134">這可能會導致角色執行個體無限期地回收。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-134">This may cause the role instance to recycle indefinitely.</span></span>
* <span data-ttu-id="2fdb8-135">連接字串是以下列 [格式](../storage/common/storage-configure-connection-string.md)指定。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-135">The connection string is specified in the following [format](../storage/common/storage-configure-connection-string.md).</span></span> <span data-ttu-id="2fdb8-136">(通訊協定必須指定為 HTTPS。)以您的儲存體帳戶名稱取代 MyAccountName，並以您的存取金鑰取代 MyAccountKey：</span><span class="sxs-lookup"><span data-stu-id="2fdb8-136">(The protocol must be specified as HTTPS.) Replace *MyAccountName* with the name of your storage account, and *MyAccountKey* with your access key:</span></span>    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  <span data-ttu-id="2fdb8-137">如果您使用 Azure Tools for Microsoft Visual Studio 開發應用程式，您可以使用屬性頁面來設定此值。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-137">If you are developing your application by using Azure Tools for Microsoft Visual Studio, you can use the property pages to set this value.</span></span>

## <a name="exported-certificate-does-not-include-private-key"></a><span data-ttu-id="2fdb8-138">匯出的憑證未包含私密金鑰</span><span class="sxs-lookup"><span data-stu-id="2fdb8-138">Exported certificate does not include private key</span></span>
<span data-ttu-id="2fdb8-139">若要在 SSL 下執行 Web 角色，您必須確保匯出的管理憑證包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-139">To run a web role under SSL, you must ensure that your exported management certificate includes the private key.</span></span> <span data-ttu-id="2fdb8-140">如果您使用「Windows 憑證管理員」匯出憑證，請務必針對 [匯出私密金鑰] 選項選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-140">If you use the *Windows Certificate Manager* to export the certificate, be sure to select **Yes** for the **Export the private key** option.</span></span> <span data-ttu-id="2fdb8-141">憑證必須匯出為 PFX 格式，這是目前唯一支援的格式。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-141">The certificate must be exported in the PFX format, which is the only format currently supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fdb8-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2fdb8-142">Next steps</span></span>
<span data-ttu-id="2fdb8-143">檢視更多雲端服務的 [疑難排解文章](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-143">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="2fdb8-144">在以下位置檢視多個角色回收案例： [Kevin Williamson 的部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2fdb8-144">View more role recycling scenarios at [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[Run]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
