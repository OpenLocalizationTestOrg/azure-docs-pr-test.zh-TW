---
title: "Azure App Service 中的 web 應用程式的 aaaEnable 診斷記錄"
description: "深入了解如何 tooenable 診斷記錄新增檢測 tooyour 應用程式，以及如何 tooaccess hello Azure 所記錄的資訊。"
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a><span data-ttu-id="99bb0-103">在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能。</span><span class="sxs-lookup"><span data-stu-id="99bb0-103">Enable diagnostics logging for web apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="99bb0-104">概觀</span><span class="sxs-lookup"><span data-stu-id="99bb0-104">Overview</span></span>
<span data-ttu-id="99bb0-105">Azure 提供內建的診斷與偵錯的 tooassist [App Service web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-105">Azure provides built-in diagnostics tooassist with debugging an [App Service web app](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="99bb0-106">在本文中，您將學習如何 tooenable 診斷記錄新增檢測 tooyour 應用程式，以及如何 tooaccess hello Azure 所記錄的資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-106">In this article you'll learn how tooenable diagnostic logging and add instrumentation tooyour application, as well as how tooaccess hello information logged by Azure.</span></span>

<span data-ttu-id="99bb0-107">本文使用 hello [Azure 入口網站](https://portal.azure.com)，Azure PowerShell 及 hello Azure 命令列介面 (Azure CLI) toowork 與診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="99bb0-107">This article uses hello [Azure Portal](https://portal.azure.com), Azure PowerShell, and hello Azure Command-Line Interface (Azure CLI) toowork with diagnostic logs.</span></span> <span data-ttu-id="99bb0-108">如需使用 Visual Studio 來處理診斷記錄的詳細資訊，請參閱 [在 Visual Studio 中疑難排解 Azure](web-sites-dotnet-troubleshoot-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-108">For information on working with diagnostic logs using Visual Studio, see [Troubleshooting Azure in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="99bb0-109"><a name="whatisdiag"></a>Web 伺服器診斷和應用程式診斷</span><span class="sxs-lookup"><span data-stu-id="99bb0-109"><a name="whatisdiag"></a>Web server diagnostics and application diagnostics</span></span>
<span data-ttu-id="99bb0-110">App Service web 應用程式提供記錄資訊從 hello web 伺服器和 hello web 應用程式的診斷的功能。</span><span class="sxs-lookup"><span data-stu-id="99bb0-110">App Service web apps provide diagnostic functionality for logging information from both hello web server and hello web application.</span></span> <span data-ttu-id="99bb0-111">這些資訊邏輯上可區分為 **Web 伺服器診斷**與**應用程式診斷**。</span><span class="sxs-lookup"><span data-stu-id="99bb0-111">These are logically separated into **web server diagnostics** and **application diagnostics**.</span></span>

### <a name="web-server-diagnostics"></a><span data-ttu-id="99bb0-112">Web 伺服器診斷</span><span class="sxs-lookup"><span data-stu-id="99bb0-112">Web server diagnostics</span></span>
<span data-ttu-id="99bb0-113">您可以啟用或停用下列種類的記錄檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="99bb0-113">You can enable or disable hello following kinds of logs:</span></span>

* <span data-ttu-id="99bb0-114">**詳細的錯誤記錄** - 對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-114">**Detailed Error Logging** - Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span> <span data-ttu-id="99bb0-115">這可能包含可協助您判斷為什麼 hello 伺服器傳回 hello 錯誤碼的資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-115">This may contain information that can help determine why hello server returned hello error code.</span></span>
* <span data-ttu-id="99bb0-116">**失敗要求追蹤**-詳細的失敗的要求，包括 hello IIS 使用的元件 tooprocess hello 要求和取得每個元件中的 hello 時間的追蹤資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-116">**Failed Request Tracing** - Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span> <span data-ttu-id="99bb0-117">如果您正嘗試 tooincrease 站台效能或隔離造成特定的 HTTP 錯誤 toobe 傳回時，這可能會很有用。</span><span class="sxs-lookup"><span data-stu-id="99bb0-117">This can be useful if you are attempting tooincrease site performance or isolate what is causing a specific HTTP error toobe returned.</span></span>
* <span data-ttu-id="99bb0-118">**Web 伺服器記錄**-HTTP 交易使用 hello 資訊[W3C 擴充的記錄檔格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-118">**Web Server Logging** - Information about HTTP transactions using hello [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> <span data-ttu-id="99bb0-119">判斷整體站台的度量資訊，例如 hello 處理要求的數目或多少要求來自特定 IP 位址時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="99bb0-119">This is useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="99bb0-120">應用程式診斷</span><span class="sxs-lookup"><span data-stu-id="99bb0-120">Application diagnostics</span></span>
<span data-ttu-id="99bb0-121">應用程式診斷可讓您的 web 應用程式所產生的 toocapture 資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-121">Application diagnostics allows you toocapture information produced by a web application.</span></span> <span data-ttu-id="99bb0-122">ASP.NET 應用程式可以使用 hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx)類別 toolog 資訊 toohello 應用程式診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="99bb0-122">ASP.NET applications can use hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) class toolog information toohello application diagnostics log.</span></span> <span data-ttu-id="99bb0-123">例如：</span><span class="sxs-lookup"><span data-stu-id="99bb0-123">For example:</span></span>

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

<span data-ttu-id="99bb0-124">在執行階段中，您可以擷取這些記錄檔 toohelp，進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="99bb0-124">At runtime you can retrieve these logs toohelp with troubleshooting.</span></span> <span data-ttu-id="99bb0-125">如需詳細資訊，請參閱 [在 Visual Studio 中疑難排解 Azure Web 應用程式](web-sites-dotnet-troubleshoot-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-125">For more information, see [Troubleshooting Azure web apps in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

<span data-ttu-id="99bb0-126">當您發佈內容 tooa web 應用程式時，app Service web 應用程式也記錄部署資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-126">App Service web apps also log deployment information when you publish content tooa web app.</span></span> <span data-ttu-id="99bb0-127">此動作會自動發生，因此無須任何組態設定即會記錄部署動作。</span><span class="sxs-lookup"><span data-stu-id="99bb0-127">This happens automatically and there are no configuration settings for deployment logging.</span></span> <span data-ttu-id="99bb0-128">部署記錄可讓您 toodetermine 部署失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="99bb0-128">Deployment logging allows you toodetermine why a deployment failed.</span></span> <span data-ttu-id="99bb0-129">例如，如果您使用的自訂部署指令碼，您可能會使用部署記錄 toodetermine hello 指令碼失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="99bb0-129">For example, if you are using a custom deployment script, you might use deployment logging toodetermine why hello script is failing.</span></span>

## <span data-ttu-id="99bb0-130"><a name="enablediag"></a>如何 tooenable 診斷</span><span class="sxs-lookup"><span data-stu-id="99bb0-130"><a name="enablediag"></a>How tooenable diagnostics</span></span>
<span data-ttu-id="99bb0-131">在 hello tooenable 診斷[Azure 入口網站](https://portal.azure.com)、 移 toohello 刀鋒視窗，web 應用程式，然後按一下**設定 > 診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="99bb0-131">tooenable diagnostics in hello [Azure Portal](https://portal.azure.com), go toohello blade for your web app and click **Settings > Diagnostics logs**.</span></span>

<!-- todo:cleanup dogfood addresses in screenshot -->
![記錄部分](./media/web-sites-enable-diagnostic-log/logspart.png)

<span data-ttu-id="99bb0-133">當您啟用**應用程式診斷**您也可以選擇 hello**層級**。</span><span class="sxs-lookup"><span data-stu-id="99bb0-133">When you enable **application diagnostics** you also choose hello **Level**.</span></span> <span data-ttu-id="99bb0-134">此設定可讓您擷取太 toofilter hello 資訊**資訊**，**警告**或**錯誤**資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-134">This setting allows you toofilter hello information captured too**informational**, **warning** or **error** information.</span></span> <span data-ttu-id="99bb0-135">將此設定太**verbose**會記錄 hello 應用程式所產生的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-135">Setting this too**verbose** will log all information produced by hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-136">不同於變更 hello web.config 檔，啟用應用程式診斷，或變更診斷記錄層級不會加以回收 hello hello 應用程式中執行的應用程式定義域。</span><span class="sxs-lookup"><span data-stu-id="99bb0-136">Unlike changing hello web.config file, enabling Application diagnostics or changing diagnostic log levels does not recycle hello app domain that hello application runs within.</span></span>
>
>

<span data-ttu-id="99bb0-137">在 hello[傳統入口網站](https://manage.windowsazure.com)Web 應用程式**設定**索引標籤上，您可以選取**儲存體**或**檔案系統**的**web 伺服器記錄**。</span><span class="sxs-lookup"><span data-stu-id="99bb0-137">In hello [classic portal](https://manage.windowsazure.com) Web app **Configure** tab, you can select **storage** or **file system** for **web server logging**.</span></span> <span data-ttu-id="99bb0-138">選取**儲存體**tooselect 儲存體帳戶，然後再 hello 記錄檔寫入的 blob 容器，可讓您。</span><span class="sxs-lookup"><span data-stu-id="99bb0-138">Selecting **storage** allows you tooselect a storage account, and then a blob container that hello logs will be written to.</span></span> <span data-ttu-id="99bb0-139">所有其他記錄**網站診斷**寫入只 toohello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="99bb0-139">All other logs for **site diagnostics** are written toohello file system only.</span></span>

<span data-ttu-id="99bb0-140">hello[傳統入口網站](https://manage.windowsazure.com)Web 應用程式**設定** 索引標籤也有其他應用程式診斷設定：</span><span class="sxs-lookup"><span data-stu-id="99bb0-140">hello [classic portal](https://manage.windowsazure.com) Web app **Configure** tab also has additional settings for application diagnostics:</span></span>

* <span data-ttu-id="99bb0-141">**檔案系統**-存放區 hello 應用程式診斷資訊 toohello web 應用程式檔案系統。</span><span class="sxs-lookup"><span data-stu-id="99bb0-141">**File system** - stores hello application diagnostics information toohello web app file system.</span></span> <span data-ttu-id="99bb0-142">這些檔案可以存取的 FTP，或使用 hello Azure PowerShell 或 Azure 命令列介面 (Azure CLI) 下載的 Zip 封存。</span><span class="sxs-lookup"><span data-stu-id="99bb0-142">These files can be accessed by FTP, or downloaded as a Zip archive by using hello Azure PowerShell or Azure Command-Line Interface (Azure CLI).</span></span>
* <span data-ttu-id="99bb0-143">**資料表儲存體**-存放區 hello hello 指定 Azure 儲存體帳戶和資料表名稱中的應用程式的診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-143">**Table storage** - stores hello application diagnostics information in hello specified Azure Storage Account and table name.</span></span>
* <span data-ttu-id="99bb0-144">**Blob 儲存體**-存放區 hello hello 指定的 Azure 儲存體帳戶和 blob 容器中的應用程式的診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-144">**Blob storage** - stores hello application diagnostics information in hello specified Azure Storage Account and blob container.</span></span>
* <span data-ttu-id="99bb0-145">**保留週期** - 依預設，所有記錄不會自動從 [Blob 儲存體] 中刪除。</span><span class="sxs-lookup"><span data-stu-id="99bb0-145">**Retention period** - by default, logs are not automatically deleted from **blob storage**.</span></span> <span data-ttu-id="99bb0-146">選取**設定保留**，然後輸入 hello 數天內，如果您想 tooautomatically tookeep 記錄刪除記錄檔。</span><span class="sxs-lookup"><span data-stu-id="99bb0-146">Select **set retention** and enter hello number of days tookeep logs if you wish tooautomatically delete logs.</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-147">如果您[重新產生儲存體帳戶的存取金鑰](../storage/common/storage-create-storage-account.md)，您必須重設 hello 各自的記錄組態 toouse hello 更新金鑰。</span><span class="sxs-lookup"><span data-stu-id="99bb0-147">If you [regenerate your storage account's access keys](../storage/common/storage-create-storage-account.md), you must reset hello respective logging configuration toouse hello updated keys.</span></span> <span data-ttu-id="99bb0-148">toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="99bb0-148">toodo this:</span></span>
>
> 1. <span data-ttu-id="99bb0-149">在 hello**設定**索引標籤上，設定得 hello 各自的記錄功能**關閉**。</span><span class="sxs-lookup"><span data-stu-id="99bb0-149">In hello **Configure** tab, set hello respective logging feature too**Off**.</span></span> <span data-ttu-id="99bb0-150">儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="99bb0-150">Save your setting.</span></span>
> 2. <span data-ttu-id="99bb0-151">重新啟用記錄 toohello 儲存體帳戶 blob 或資料表。</span><span class="sxs-lookup"><span data-stu-id="99bb0-151">Enable logging toohello storage account blob or table again.</span></span> <span data-ttu-id="99bb0-152">儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="99bb0-152">Save your setting.</span></span>
>
>

<span data-ttu-id="99bb0-153">檔案系統中，資料表儲存體或 blob 儲存體的任何組合，可以在 hello 相同的時間，並有個別的記錄層級組態啟用。</span><span class="sxs-lookup"><span data-stu-id="99bb0-153">Any combination of file system, table storage, or blob storage can be enabled at hello same time, and have individual log level configurations.</span></span> <span data-ttu-id="99bb0-154">比方說，您可能需要 toolog 錯誤和警告 tooblob 儲存體做為長期的記錄解決方案，同時也可讓檔案系統記錄的詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="99bb0-154">For example, you may wish toolog errors and warnings tooblob storage as a long-term logging solution, while enabling file system logging with a level of verbose.</span></span>

<span data-ttu-id="99bb0-155">當所有三個儲存體位置提供 hello 時記錄的事件相同的基本資訊**資料表儲存體**和**blob 儲存體**記錄例如 hello 執行個體識別碼、 執行緒識別碼和更多的其他資訊細微的時間戳記 （刻度格式） 於記錄太**檔案系統**。</span><span class="sxs-lookup"><span data-stu-id="99bb0-155">While all three storage locations provide hello same basic information for logged events, **table storage** and **blob storage** log additional information such as hello instance ID, thread ID, and a more granular timestamp (tick format) than logging too**file system**.</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-156">儲存在 [資料表儲存體] 或 [Blob 儲存體] 內的資訊只能透過儲存用戶端，或是能夠直接使用這些儲存系統的應用程式來存取。</span><span class="sxs-lookup"><span data-stu-id="99bb0-156">Information stored in **table storage** or **blob  storage** can only be accessed using a storage client or an application that can directly work with these storage systems.</span></span> <span data-ttu-id="99bb0-157">例如，Visual Studio 2013 包含可能是使用的 tooexplore 資料表或 blob 儲存體，儲存體總管，HDInsight 可以存取儲存在 blob 儲存體中的資料。</span><span class="sxs-lookup"><span data-stu-id="99bb0-157">For example, Visual Studio 2013 contains a Storage Explorer that can be used tooexplore table or blob storage, and HDInsight can access data stored in blob storage.</span></span> <span data-ttu-id="99bb0-158">您也可以撰寫應用程式存取 Azure 儲存體使用其中一種 hello [Azure Sdk](/downloads/#)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-158">You can also write an application that accesses Azure Storage by using one of hello [Azure SDKs](/downloads/#).</span></span>
>
> [!NOTE]
> <span data-ttu-id="99bb0-159">診斷也可以啟用從 Azure PowerShell 中使用 hello**組 AzureWebsite** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="99bb0-159">Diagnostics can also be enabled from Azure PowerShell using hello **Set-AzureWebsite** cmdlet.</span></span> <span data-ttu-id="99bb0-160">如果尚未安裝 Azure PowerShell，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-160">If you have not installed Azure PowerShell, or have not configured it toouse your Azure Subscription, see [How tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

## <span data-ttu-id="99bb0-161"><a name="download"></a> 作法：下載記錄</span><span class="sxs-lookup"><span data-stu-id="99bb0-161"><a name="download"></a> How to: Download logs</span></span>
<span data-ttu-id="99bb0-162">儲存診斷資訊 toohello web 應用程式檔案系統可以直接使用 FTP 存取。</span><span class="sxs-lookup"><span data-stu-id="99bb0-162">Diagnostic information stored toohello web app file system can be accessed directly using FTP.</span></span> <span data-ttu-id="99bb0-163">也可以使用 Azure PowerShell 或 hello Azure 命令列介面的 Zip 封存下載。</span><span class="sxs-lookup"><span data-stu-id="99bb0-163">It can also be downloaded as a Zip archive using Azure PowerShell or hello Azure Command-Line Interface.</span></span>

<span data-ttu-id="99bb0-164">hello hello 記錄會儲存於的目錄結構如下所示：</span><span class="sxs-lookup"><span data-stu-id="99bb0-164">hello directory structure that hello logs are stored in is as follows:</span></span>

* <span data-ttu-id="99bb0-165">**應用程式記錄** - /LogFiles/Application/。</span><span class="sxs-lookup"><span data-stu-id="99bb0-165">**Application logs** - /LogFiles/Application/.</span></span> <span data-ttu-id="99bb0-166">此資料夾內含有一或多個文字檔案，這些檔案涵蓋應用程式記錄所產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-166">This folder contains one or more text files containing information produced by application logging.</span></span>
* <span data-ttu-id="99bb0-167">**失敗要求追蹤** - /LogFiles/W3SVC#########/。</span><span class="sxs-lookup"><span data-stu-id="99bb0-167">**Failed Request Traces** - /LogFiles/W3SVC#########/.</span></span> <span data-ttu-id="99bb0-168">此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="99bb0-168">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="99bb0-169">請確定您 hello XSL 檔下載到 hello 與 hello XML 檔案，因為 hello XSL 檔案提供了用來格式化和篩選 hello hello XML 內容的功能相同的目錄檔案中 Internet Explorer 檢視時。</span><span class="sxs-lookup"><span data-stu-id="99bb0-169">Ensure that you download hello XSL file into hello same directory as hello XML file(s) because hello XSL file provides functionality for formatting and filtering hello contents of hello XML file(s) when viewed in Internet Explorer.</span></span>
* <span data-ttu-id="99bb0-170">**詳細錯誤記錄** - /LogFiles/DetailedErrors/。</span><span class="sxs-lookup"><span data-stu-id="99bb0-170">**Detailed Error Logs** - /LogFiles/DetailedErrors/.</span></span> <span data-ttu-id="99bb0-171">此資料夾包含一或多個 .htm 檔案，內含已經發生的任何 HTTP 錯誤之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-171">This folder contains one or more .htm files that provide extensive information for any HTTP errors that have occurred.</span></span>
* <span data-ttu-id="99bb0-172">**Web 伺服器記錄** - /LogFiles/http/RawLogs。</span><span class="sxs-lookup"><span data-stu-id="99bb0-172">**Web Server Logs** - /LogFiles/http/RawLogs.</span></span> <span data-ttu-id="99bb0-173">這個資料夾包含一個或多個文字檔案格式是 「 hello [W3C 擴充的記錄檔格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-173">This folder contains one or more text files formatted using hello [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
* <span data-ttu-id="99bb0-174">**部署記錄** - /LogFiles/Git。</span><span class="sxs-lookup"><span data-stu-id="99bb0-174">**Deployment logs** - /LogFiles/Git.</span></span> <span data-ttu-id="99bb0-175">此資料夾包含 hello Azure web 應用程式，所使用的內部部署處理序所產生的記錄檔，以及記錄檔中的 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="99bb0-175">This folder contains logs generated by hello internal deployment processes used by Azure web apps, as well as logs for Git deployments.</span></span>

### <a name="ftp"></a><span data-ttu-id="99bb0-176">FTP</span><span class="sxs-lookup"><span data-stu-id="99bb0-176">FTP</span></span>
<span data-ttu-id="99bb0-177">使用 FTP，請瀏覽 hello tooaccess 診斷資訊**儀表板**hello 在 web 應用程式的[傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-177">tooaccess diagnostic information using FTP, visit hello **Dashboard** of your web app in hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="99bb0-178">在 hello**快速概覽**區段中，使用 hello **FTP 診斷記錄**連結使用 FTP tooaccess hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="99bb0-178">In hello **quick glance** section, use hello **FTP Diagnostic Logs** link tooaccess hello log files using FTP.</span></span> <span data-ttu-id="99bb0-179">hello**部署/FTP 使用者**項目會列出 hello 應該使用的 tooaccess hello FTP 站台的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="99bb0-179">hello **Deployment/FTP User** entry lists hello user name that should be used tooaccess hello FTP site.</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-180">如果 hello**部署/FTP 使用者**未設定項目，或您忘了 hello 這個使用者的密碼，您可以建立新的使用者和密碼使用 hello**重設部署認證**hello中的連結**快速概覽**區段 hello**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="99bb0-180">If hello **Deployment/FTP User** entry is not set, or you have forgotten hello password for this user, you can create a new user and password by using hello **Reset deployment credentials** link in hello **quick glance** section of hello **Dashboard**.</span></span>
>
>

### <a name="download-with-azure-powershell"></a><span data-ttu-id="99bb0-181">使用 Azure PowerShell 來下載</span><span class="sxs-lookup"><span data-stu-id="99bb0-181">Download with Azure PowerShell</span></span>
<span data-ttu-id="99bb0-182">toodownload hello 記錄檔，啟動 Azure PowerShell 的新執行個體，並使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="99bb0-182">toodownload hello log files, start a new instance of Azure PowerShell and use hello following command:</span></span>

    Save-AzureWebSiteLog -Name webappname

<span data-ttu-id="99bb0-183">這會將 hello hello hello 所指定的 web 應用程式的記錄檔儲存**-名稱**參數 tooa 檔名為**logs.zip** hello 目前目錄中。</span><span class="sxs-lookup"><span data-stu-id="99bb0-183">This will save hello logs for hello web app specified by hello **-Name** parameter tooa file named **logs.zip** in hello current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-184">如果尚未安裝 Azure PowerShell，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-184">If you have not installed Azure PowerShell, or have not configured it toouse your Azure Subscription, see [How tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

### <a name="download-with-azure-command-line-interface"></a><span data-ttu-id="99bb0-185">使用 Azure 命列列介面來下載</span><span class="sxs-lookup"><span data-stu-id="99bb0-185">Download with Azure Command-Line Interface</span></span>
<span data-ttu-id="99bb0-186">toodownload hello 記錄檔使用 hello Azure 命令列介面，開啟新的命令提示字元、 PowerShell、 Bash 或終端機工作階段，並輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="99bb0-186">toodownload hello log files using hello Azure Command Line Interface, open a new command prompt, PowerShell, Bash, or Terminal session and enter hello following command:</span></span>

    azure site log download webappname

<span data-ttu-id="99bb0-187">這樣會將儲存 hello 記錄檔中的 hello web 應用程式名為 'webappname' tooa 檔名為**diagnostics.zip** hello 目前目錄中。</span><span class="sxs-lookup"><span data-stu-id="99bb0-187">This will save hello logs for hello web app named 'webappname' tooa file named **diagnostics.zip** in hello current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-188">如果您尚未安裝 hello Azure 命令列介面 (Azure CLI)，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-188">If you have not installed hello Azure Command-Line Interface (Azure CLI), or have not configured it toouse your Azure Subscription, see [How tooUse Azure CLI](../cli-install-nodejs.md).</span></span>
>
>

## <a name="how-to-view-logs-in-application-insights"></a><span data-ttu-id="99bb0-189">作法：在 Application Insights 中檢視記錄</span><span class="sxs-lookup"><span data-stu-id="99bb0-189">How to: View logs in Application Insights</span></span>
<span data-ttu-id="99bb0-190">Visual Studio Application Insights 提供工具來篩選和搜尋記錄檔和相關的 hello 記錄要求和其他事件。</span><span class="sxs-lookup"><span data-stu-id="99bb0-190">Visual Studio Application Insights provides tools for filtering and searching logs, and for correlating hello logs with requests and other events.</span></span>

1. <span data-ttu-id="99bb0-191">Visual Studio 中加入 hello Application Insights SDK tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="99bb0-191">Add hello Application Insights SDK tooyour project in Visual Studio.</span></span>
   * <span data-ttu-id="99bb0-192">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選擇 [加入 Application Insights]。</span><span class="sxs-lookup"><span data-stu-id="99bb0-192">In Solution Explorer, right click your project and choose Add Application Insights.</span></span> <span data-ttu-id="99bb0-193">系統將指導您完成包括建立 Application Insights 資源在內的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="99bb0-193">You'll be guided through steps that include creating an Application Insights resource.</span></span> [<span data-ttu-id="99bb0-194">深入了解</span><span class="sxs-lookup"><span data-stu-id="99bb0-194">Learn more</span></span>](../application-insights/app-insights-asp-net.md)
2. <span data-ttu-id="99bb0-195">加入 hello 追蹤接聽項封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="99bb0-195">Add hello Trace Listener package tooyour project.</span></span>
   * <span data-ttu-id="99bb0-196">以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="99bb0-196">Right click your project and choose Manage NuGet Packages.</span></span> <span data-ttu-id="99bb0-197">選取 `Microsoft.ApplicationInsights.TraceListener` [深入了解](../application-insights/app-insights-asp-net-trace-logs.md)</span><span class="sxs-lookup"><span data-stu-id="99bb0-197">Select `Microsoft.ApplicationInsights.TraceListener` [Learn more](../application-insights/app-insights-asp-net-trace-logs.md)</span></span>
3. <span data-ttu-id="99bb0-198">上傳您的專案，然後執行 toogenerate 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="99bb0-198">Upload your project and run it toogenerate log data.</span></span>
4. <span data-ttu-id="99bb0-199">在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 tooyour 新的 Application Insights 資源，並開啟**搜尋**。</span><span class="sxs-lookup"><span data-stu-id="99bb0-199">In hello [Azure Portal](https://portal.azure.com/), browse tooyour new Application Insights resource, and open **Search**.</span></span> <span data-ttu-id="99bb0-200">您將會看到您的記錄資料，以及要求、使用情況及其他遙測。</span><span class="sxs-lookup"><span data-stu-id="99bb0-200">You'll see your log data, along with request, usage and other telemetry.</span></span> <span data-ttu-id="99bb0-201">某些遙測可能需要幾分鐘的時間 tooarrive： 按一下 重新整理。</span><span class="sxs-lookup"><span data-stu-id="99bb0-201">Some telemetry might take a few minutes tooarrive: click Refresh.</span></span> [<span data-ttu-id="99bb0-202">深入了解</span><span class="sxs-lookup"><span data-stu-id="99bb0-202">Learn more</span></span>](../application-insights/app-insights-diagnostic-search.md)

[<span data-ttu-id="99bb0-203">深入了解使用 Application Insights 的效能追蹤</span><span class="sxs-lookup"><span data-stu-id="99bb0-203">Learn more about performance tracking with Application Insights</span></span>](../application-insights/app-insights-azure-web-apps.md)

## <span data-ttu-id="99bb0-204"><a name="streamlogs"></a> 作法：串流記錄</span><span class="sxs-lookup"><span data-stu-id="99bb0-204"><a name="streamlogs"></a> How to: Stream logs</span></span>
<span data-ttu-id="99bb0-205">在開發應用程式時，通常會很有用的 toosee 接近即時的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-205">While developing an application, it is often useful toosee logging information in near-real time.</span></span> <span data-ttu-id="99bb0-206">這可以透過串流處理將記錄資訊 tooyour 開發環境中使用 Azure PowerShell 或 hello Azure 命令列介面完成。</span><span class="sxs-lookup"><span data-stu-id="99bb0-206">This can be accomplished by streaming logging information tooyour development environment using either Azure PowerShell or hello Azure Command-Line Interface.</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-207">某些類型的記錄緩衝區寫入 toohello 記錄檔，可能會導致 hello 資料流中失序的事件。</span><span class="sxs-lookup"><span data-stu-id="99bb0-207">Some types of logging buffer write toohello log file, which can result in out of order events in hello stream.</span></span> <span data-ttu-id="99bb0-208">例如，當使用者造訪網頁時，就會發生的應用程式記錄檔項目可能顯示 hello hello 相對應 HTTP 記錄項目 hello 網頁要求之前的資料流中。</span><span class="sxs-lookup"><span data-stu-id="99bb0-208">For example, an application log entry that occurs when a user visits a page may be displayed in hello stream before hello corresponding HTTP log entry for hello page request.</span></span>
>
> [!NOTE]
> <span data-ttu-id="99bb0-209">記錄檔資料流也會串流資訊寫入 tooany 文字檔案儲存在 hello **d:\\家用\\LogFiles\\** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="99bb0-209">Log streaming will also stream information written tooany text file stored in hello **D:\\home\\LogFiles\\** folder.</span></span>
>
>

### <a name="streaming-with-azure-powershell"></a><span data-ttu-id="99bb0-210">使用 Azure PowerShell 來串流</span><span class="sxs-lookup"><span data-stu-id="99bb0-210">Streaming with Azure PowerShell</span></span>
<span data-ttu-id="99bb0-211">toostream 記錄資訊，請啟動 Azure PowerShell 的新執行個體，並使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="99bb0-211">toostream logging information, start a new instance of Azure PowerShell and use hello following command:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail

<span data-ttu-id="99bb0-212">這會連接 toohello hello 所指定的 web 應用程式**-名稱**參數並開始串流處理資訊 toohello PowerShell 視窗，記錄檔事件發生於 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99bb0-212">This will connect toohello web app specified by hello **-Name** parameter and begin streaming information toohello PowerShell window as log events occur on hello web app.</span></span> <span data-ttu-id="99bb0-213">將資料流寫入 toofiles 結尾.txt、.log 或.htm hello /LogFiles 目錄 （d: / 首頁/記錄檔） 中儲存的任何資訊 toohello 本機主控台。</span><span class="sxs-lookup"><span data-stu-id="99bb0-213">Any information written toofiles ending in .txt, .log, or .htm that are stored in hello /LogFiles directory (d:/home/logfiles) will be streamed toohello local console.</span></span>

<span data-ttu-id="99bb0-214">toofilter 特定事件，例如錯誤，使用 hello **-訊息**參數。</span><span class="sxs-lookup"><span data-stu-id="99bb0-214">toofilter specific events, such as errors, use hello **-Message** parameter.</span></span> <span data-ttu-id="99bb0-215">例如：</span><span class="sxs-lookup"><span data-stu-id="99bb0-215">For example:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

<span data-ttu-id="99bb0-216">toofilter 特定記錄類型，例如 HTTP、 使用 hello **-路徑**參數。</span><span class="sxs-lookup"><span data-stu-id="99bb0-216">toofilter specific log types, such as HTTP, use hello **-Path** parameter.</span></span> <span data-ttu-id="99bb0-217">例如：</span><span class="sxs-lookup"><span data-stu-id="99bb0-217">For example:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

<span data-ttu-id="99bb0-218">toosee 的可用路徑，使用 hello-ListPath 參數清單。</span><span class="sxs-lookup"><span data-stu-id="99bb0-218">toosee a list of available paths, use hello -ListPath parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-219">如果尚未安裝 Azure PowerShell，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-219">If you have not installed Azure PowerShell, or have not configured it toouse your Azure Subscription, see [How tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

### <a name="streaming-with-azure-command-line-interface"></a><span data-ttu-id="99bb0-220">使用 Azure 命令列介面來串流</span><span class="sxs-lookup"><span data-stu-id="99bb0-220">Streaming with Azure Command-Line Interface</span></span>
<span data-ttu-id="99bb0-221">toostream 記錄資訊，請開啟新的命令提示字元、 PowerShell、 Bash 或終端機工作階段，並輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="99bb0-221">toostream logging information, open a new command prompt, PowerShell, Bash, or Terminal session and enter hello following command:</span></span>

    azure site log tail webappname

<span data-ttu-id="99bb0-222">將名為 'webappname' toohello web 應用程式連接，並開始串流處理資訊 toohello 視窗記錄事件發生於 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99bb0-222">This will connect toohello web app named 'webappname' and begin streaming information toohello window as log events occur on hello web app.</span></span> <span data-ttu-id="99bb0-223">將資料流寫入 toofiles 結尾.txt、.log 或.htm hello /LogFiles 目錄 （d: / 首頁/記錄檔） 中儲存的任何資訊 toohello 本機主控台。</span><span class="sxs-lookup"><span data-stu-id="99bb0-223">Any information written toofiles ending in .txt, .log, or .htm that are stored in hello /LogFiles directory (d:/home/logfiles) will be streamed toohello local console.</span></span>

<span data-ttu-id="99bb0-224">toofilter 特定事件，例如錯誤，使用 hello **-篩選**參數。</span><span class="sxs-lookup"><span data-stu-id="99bb0-224">toofilter specific events, such as errors, use hello **--Filter** parameter.</span></span> <span data-ttu-id="99bb0-225">例如：</span><span class="sxs-lookup"><span data-stu-id="99bb0-225">For example:</span></span>

    azure site log tail webappname --filter Error

<span data-ttu-id="99bb0-226">toofilter 特定記錄類型，例如 HTTP、 使用 hello **-路徑**參數。</span><span class="sxs-lookup"><span data-stu-id="99bb0-226">toofilter specific log types, such as HTTP, use hello **--Path** parameter.</span></span> <span data-ttu-id="99bb0-227">例如：</span><span class="sxs-lookup"><span data-stu-id="99bb0-227">For example:</span></span>

    azure site log tail webappname --path http

> [!NOTE]
> <span data-ttu-id="99bb0-228">如果您尚未安裝 hello Azure 命令列介面，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure 命令列介面](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-228">If you have not installed hello Azure Command-Line Interface, or have not configured it toouse your Azure Subscription, see [How tooUse Azure Command-Line Interface](../cli-install-nodejs.md).</span></span>
>
>

## <span data-ttu-id="99bb0-229"><a name="understandlogs"></a> 作法：了解診斷記錄</span><span class="sxs-lookup"><span data-stu-id="99bb0-229"><a name="understandlogs"></a> How to: Understand diagnostics logs</span></span>
### <a name="application-diagnostics-logs"></a><span data-ttu-id="99bb0-230">應用程式診斷記錄</span><span class="sxs-lookup"><span data-stu-id="99bb0-230">Application diagnostics logs</span></span>
<span data-ttu-id="99bb0-231">應用程式診斷資訊是以特定格式儲存對於.NET 應用程式，根據您是否儲存記錄檔 toohello 檔案系統中，資料表儲存體，或 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="99bb0-231">Application diagnostics stores information in a specific format for .NET applications, depending on whether you store logs toohello file system, table storage, or blob storage.</span></span> <span data-ttu-id="99bb0-232">hello 組基本的資料儲存為相同 hello 到所有的三個儲存體類型-hello 日期和時間 hello、 發生事件 hello 產生 hello 事件、 hello 事件類型 （資訊、 警告、 錯誤） 和 hello 事件訊息的處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="99bb0-232">hello base set of data stored is hello same across all three storage types - hello date and time hello event occurred, hello process ID that produced hello event, hello event type (information, warning, error,) and hello event message.</span></span>

<span data-ttu-id="99bb0-233">**檔案系統**</span><span class="sxs-lookup"><span data-stu-id="99bb0-233">**File system**</span></span>

<span data-ttu-id="99bb0-234">記錄的 toohello 檔案系統，或使用資料流接收的每一行將處於下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="99bb0-234">Each line logged toohello file system or received using streaming will be in hello following format:</span></span>

    {Date}  PID[{process id}] {event type/level} {message}

<span data-ttu-id="99bb0-235">例如，錯誤事件會出現類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="99bb0-235">For example, an error event would appear similar toohello following:</span></span>

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

<span data-ttu-id="99bb0-236">記錄 toohello 檔案系統提供 hello 三個可用的方法，提供僅 hello 時間、 處理序識別碼、 事件層級，以及訊息的 hello 最基本的資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-236">Logging toohello file system provides hello most basic information of hello three available methods, providing only hello time, process id, event level, and message.</span></span>

<span data-ttu-id="99bb0-237">**資料表儲存體**</span><span class="sxs-lookup"><span data-stu-id="99bb0-237">**Table storage**</span></span>

<span data-ttu-id="99bb0-238">當記錄 tootable 儲存體，其他屬性會使用的 toofacilitate 搜尋 hello 資料儲存在 hello 資料表，以及更細微 hello 事件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-238">When logging tootable storage, additional properties are used toofacilitate searching hello data stored in hello table as well as more granular information on hello event.</span></span> <span data-ttu-id="99bb0-239">hello 下列屬性 （資料行） 會用於儲存在 hello 資料表中每個實體 （資料列）。</span><span class="sxs-lookup"><span data-stu-id="99bb0-239">hello following properties (columns) are used for each entity (row) stored in hello table.</span></span>

| <span data-ttu-id="99bb0-240">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="99bb0-240">Property name</span></span> | <span data-ttu-id="99bb0-241">值/格式</span><span class="sxs-lookup"><span data-stu-id="99bb0-241">Value/format</span></span> |
| --- | --- |
| <span data-ttu-id="99bb0-242">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="99bb0-242">PartitionKey</span></span> |<span data-ttu-id="99bb0-243">Hello 事件 yyyyMMddHH 格式的日期/時間。</span><span class="sxs-lookup"><span data-stu-id="99bb0-243">Date/time of hello event in yyyyMMddHH format</span></span> |
| <span data-ttu-id="99bb0-244">RowKey</span><span class="sxs-lookup"><span data-stu-id="99bb0-244">RowKey</span></span> |<span data-ttu-id="99bb0-245">可唯一識別此實體的 GUID 值</span><span class="sxs-lookup"><span data-stu-id="99bb0-245">A GUID value that uniquely identifies this entity</span></span> |
| <span data-ttu-id="99bb0-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="99bb0-246">Timestamp</span></span> |<span data-ttu-id="99bb0-247">發生 hello 日期和時間的 hello 事件</span><span class="sxs-lookup"><span data-stu-id="99bb0-247">hello date and time that hello event occurred</span></span> |
| <span data-ttu-id="99bb0-248">EventTickCount</span><span class="sxs-lookup"><span data-stu-id="99bb0-248">EventTickCount</span></span> |<span data-ttu-id="99bb0-249">hello 發生日期和時間的 hello 事件，以刻度格式 （大於有效位數）</span><span class="sxs-lookup"><span data-stu-id="99bb0-249">hello date and time that hello event occurred, in Tick format (greater precision)</span></span> |
| <span data-ttu-id="99bb0-250">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="99bb0-250">ApplicationName</span></span> |<span data-ttu-id="99bb0-251">hello web 應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="99bb0-251">hello web app name</span></span> |
| <span data-ttu-id="99bb0-252">Level</span><span class="sxs-lookup"><span data-stu-id="99bb0-252">Level</span></span> |<span data-ttu-id="99bb0-253">事件層級 (例如，錯誤、警告、資訊)</span><span class="sxs-lookup"><span data-stu-id="99bb0-253">Event level (e.g. error, warning, information)</span></span> |
| <span data-ttu-id="99bb0-254">EventId</span><span class="sxs-lookup"><span data-stu-id="99bb0-254">EventId</span></span> |<span data-ttu-id="99bb0-255">這個事件的 hello 事件識別碼</span><span class="sxs-lookup"><span data-stu-id="99bb0-255">hello event ID of this event</span></span><p><p><span data-ttu-id="99bb0-256">如果沒有指定，預設 too0</span><span class="sxs-lookup"><span data-stu-id="99bb0-256">Defaults too0 if none specified</span></span> |
| <span data-ttu-id="99bb0-257">InstanceId</span><span class="sxs-lookup"><span data-stu-id="99bb0-257">InstanceId</span></span> |<span data-ttu-id="99bb0-258">即使 hello hello web 應用程式的執行個體上發生</span><span class="sxs-lookup"><span data-stu-id="99bb0-258">Instance of hello web app that hello even occurred on</span></span> |
| <span data-ttu-id="99bb0-259">Pid</span><span class="sxs-lookup"><span data-stu-id="99bb0-259">Pid</span></span> |<span data-ttu-id="99bb0-260">處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="99bb0-260">Process ID</span></span> |
| <span data-ttu-id="99bb0-261">Tid</span><span class="sxs-lookup"><span data-stu-id="99bb0-261">Tid</span></span> |<span data-ttu-id="99bb0-262">產生 hello 事件 hello 執行緒 hello 執行緒 ID</span><span class="sxs-lookup"><span data-stu-id="99bb0-262">hello thread ID of hello thread that produced hello event</span></span> |
| <span data-ttu-id="99bb0-263">訊息</span><span class="sxs-lookup"><span data-stu-id="99bb0-263">Message</span></span> |<span data-ttu-id="99bb0-264">事件詳細資訊訊息</span><span class="sxs-lookup"><span data-stu-id="99bb0-264">Event detail message</span></span> |

<span data-ttu-id="99bb0-265">**Blob 儲存體**</span><span class="sxs-lookup"><span data-stu-id="99bb0-265">**Blob storage**</span></span>

<span data-ttu-id="99bb0-266">當記錄 tooblob 儲存體，資料會儲存在逗號分隔值 (CSV) 格式。</span><span class="sxs-lookup"><span data-stu-id="99bb0-266">When logging tooblob storage, data is stored in comma-separated values (CSV) format.</span></span> <span data-ttu-id="99bb0-267">類似的 tootable 儲存體的其他欄位會記錄的 tooprovide hello 事件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-267">Similar tootable storage, additional fields are logged tooprovide more granular information about hello event.</span></span> <span data-ttu-id="99bb0-268">hello 下列屬性適用於在 hello CSV 的每個資料列：</span><span class="sxs-lookup"><span data-stu-id="99bb0-268">hello following properties are used for each row in hello CSV:</span></span>

| <span data-ttu-id="99bb0-269">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="99bb0-269">Property name</span></span> | <span data-ttu-id="99bb0-270">值/格式</span><span class="sxs-lookup"><span data-stu-id="99bb0-270">Value/format</span></span> |
| --- | --- |
| <span data-ttu-id="99bb0-271">Date</span><span class="sxs-lookup"><span data-stu-id="99bb0-271">Date</span></span> |<span data-ttu-id="99bb0-272">發生 hello 日期和時間的 hello 事件</span><span class="sxs-lookup"><span data-stu-id="99bb0-272">hello date and time that hello event occurred</span></span> |
| <span data-ttu-id="99bb0-273">Level</span><span class="sxs-lookup"><span data-stu-id="99bb0-273">Level</span></span> |<span data-ttu-id="99bb0-274">事件層級 (例如，錯誤、警告、資訊)</span><span class="sxs-lookup"><span data-stu-id="99bb0-274">Event level (e.g. error, warning, information)</span></span> |
| <span data-ttu-id="99bb0-275">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="99bb0-275">ApplicationName</span></span> |<span data-ttu-id="99bb0-276">hello web 應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="99bb0-276">hello web app name</span></span> |
| <span data-ttu-id="99bb0-277">InstanceId</span><span class="sxs-lookup"><span data-stu-id="99bb0-277">InstanceId</span></span> |<span data-ttu-id="99bb0-278">Hello 事件 hello web 應用程式的執行個體上發生</span><span class="sxs-lookup"><span data-stu-id="99bb0-278">Instance of hello web app that hello event occurred on</span></span> |
| <span data-ttu-id="99bb0-279">EventTickCount</span><span class="sxs-lookup"><span data-stu-id="99bb0-279">EventTickCount</span></span> |<span data-ttu-id="99bb0-280">hello 發生日期和時間的 hello 事件，以刻度格式 （大於有效位數）</span><span class="sxs-lookup"><span data-stu-id="99bb0-280">hello date and time that hello event occurred, in Tick format (greater precision)</span></span> |
| <span data-ttu-id="99bb0-281">EventId</span><span class="sxs-lookup"><span data-stu-id="99bb0-281">EventId</span></span> |<span data-ttu-id="99bb0-282">這個事件的 hello 事件識別碼</span><span class="sxs-lookup"><span data-stu-id="99bb0-282">hello event ID of this event</span></span><p><p><span data-ttu-id="99bb0-283">如果沒有指定，預設 too0</span><span class="sxs-lookup"><span data-stu-id="99bb0-283">Defaults too0 if none specified</span></span> |
| <span data-ttu-id="99bb0-284">Pid</span><span class="sxs-lookup"><span data-stu-id="99bb0-284">Pid</span></span> |<span data-ttu-id="99bb0-285">處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="99bb0-285">Process ID</span></span> |
| <span data-ttu-id="99bb0-286">Tid</span><span class="sxs-lookup"><span data-stu-id="99bb0-286">Tid</span></span> |<span data-ttu-id="99bb0-287">產生 hello 事件 hello 執行緒 hello 執行緒 ID</span><span class="sxs-lookup"><span data-stu-id="99bb0-287">hello thread ID of hello thread that produced hello event</span></span> |
| <span data-ttu-id="99bb0-288">訊息</span><span class="sxs-lookup"><span data-stu-id="99bb0-288">Message</span></span> |<span data-ttu-id="99bb0-289">事件詳細資訊訊息</span><span class="sxs-lookup"><span data-stu-id="99bb0-289">Event detail message</span></span> |

<span data-ttu-id="99bb0-290">儲存在 blob 中的 hello 資料看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="99bb0-290">hello data stored in a blob would look similar toohello following:</span></span>

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> <span data-ttu-id="99bb0-291">hello hello 記錄檔的第一行會包含 hello 資料行標頭，此範例中所示。</span><span class="sxs-lookup"><span data-stu-id="99bb0-291">hello first line of hello log will contain hello column headers as represented in this example.</span></span>
>
>

### <a name="failed-request-traces"></a><span data-ttu-id="99bb0-292">失敗要求追蹤</span><span class="sxs-lookup"><span data-stu-id="99bb0-292">Failed request traces</span></span>
<span data-ttu-id="99bb0-293">失敗要求追蹤會儲存在名為 **fr######.xml**的 XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="99bb0-293">Failed request traces are stored in XML files named **fr######.xml**.</span></span> <span data-ttu-id="99bb0-294">toomake 它更容易 tooview hello 登入資訊、 名為的 XSL 樣式表**freb.xsl**所提供的 hello 相同目錄中如 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="99bb0-294">toomake it easier tooview hello logged information, an XSL stylesheet named **freb.xsl** is provided in hello same directory as hello XML files.</span></span> <span data-ttu-id="99bb0-295">在 Internet Explorer 中開啟其中一個 hello XML 檔案，將會使用 hello XSL 樣式表 tooprovide 格式化顯示 hello 追蹤資訊。</span><span class="sxs-lookup"><span data-stu-id="99bb0-295">Opening one of hello XML files in Internet Explorer will use hello XSL stylesheet tooprovide a formatted display of hello trace information.</span></span> <span data-ttu-id="99bb0-296">這會顯示類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="99bb0-296">This will appear similar toohello following:</span></span>

![hello 瀏覽器中檢視失敗的要求](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a><span data-ttu-id="99bb0-298">詳細錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="99bb0-298">Detailed error logs</span></span>
<span data-ttu-id="99bb0-299">詳細的錯誤記錄指的是可針對發生的 HTTP 錯誤提供更詳盡資訊的 HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="99bb0-299">Detailed error logs are HTML documents that provide more detailed information on HTTP errors that have occurred.</span></span> <span data-ttu-id="99bb0-300">由於它們都是單純的 HTML 文件，因此可以使用網頁瀏覽器來檢視。</span><span class="sxs-lookup"><span data-stu-id="99bb0-300">Since they are simply HTML documents, they can be viewed using a web browser.</span></span>

### <a name="web-server-logs"></a><span data-ttu-id="99bb0-301">Web 伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="99bb0-301">Web server logs</span></span>
<span data-ttu-id="99bb0-302">hello web 伺服器記錄檔的格式是 hello [W3C 擴充的記錄檔格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99bb0-302">hello web server logs are formatted using hello [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> <span data-ttu-id="99bb0-303">此項資訊可透過文字編輯器來讀取，或是運用 [記錄檔剖析器](http://go.microsoft.com/fwlink/?LinkId=246619)(英文) 之類的公用程式來剖析。</span><span class="sxs-lookup"><span data-stu-id="99bb0-303">This information can be read using a text editor or parsed using utilities such as [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619).</span></span>

> [!NOTE]
> <span data-ttu-id="99bb0-304">hello Azure web 應用程式所產生的記錄檔不支援 hello **s-computername**， **s ip**，或**cs 版本**欄位。</span><span class="sxs-lookup"><span data-stu-id="99bb0-304">hello logs produced by Azure web apps do not support hello **s-computername**, **s-ip**, or **cs-version** fields.</span></span>
>
>

## <span data-ttu-id="99bb0-305"><a name="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="99bb0-305"><a name="nextsteps"></a> Next steps</span></span>
* [<span data-ttu-id="99bb0-306">如何 tooMonitor Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="99bb0-306">How tooMonitor Web Apps</span></span>](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [<span data-ttu-id="99bb0-307">在 Visual Studio 中疑難排解 Azure Web App</span><span class="sxs-lookup"><span data-stu-id="99bb0-307">Troubleshooting Azure web apps in Visual Studio</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)
* [<span data-ttu-id="99bb0-308">在 HDInsight 中分析 Web 應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="99bb0-308">Analyze web app Logs in HDInsight</span></span>](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> <span data-ttu-id="99bb0-309">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="99bb0-309">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="99bb0-310">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="99bb0-310">No credit cards required; no commitments.</span></span>
>
>

## <a name="whats-changed"></a><span data-ttu-id="99bb0-311">變更的項目</span><span class="sxs-lookup"><span data-stu-id="99bb0-311">What's changed</span></span>
* <span data-ttu-id="99bb0-312">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="99bb0-312">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
* <span data-ttu-id="99bb0-313">Hello 舊入口網站 toohello 新入口網站的變更如指南 toohello:[巡覽參考 hello Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)</span><span class="sxs-lookup"><span data-stu-id="99bb0-313">For a guide toohello change of hello old portal toohello new portal see: [Reference for navigating hello Azure portal](http://go.microsoft.com/fwlink/?LinkId=529715)</span></span>
