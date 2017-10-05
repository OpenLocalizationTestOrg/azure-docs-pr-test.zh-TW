---
title: "在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能。"
description: "了解如何啟用診斷記錄，並在您的應用程式中加入診斷工具，以及如何存取 Azure 所記錄的資訊。"
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
ms.openlocfilehash: 7b125aeb9c0ee1dcbb199da98b0ce079820ea85c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a><span data-ttu-id="b9b5c-103">在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-103">Enable diagnostics logging for web apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="b9b5c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b9b5c-104">Overview</span></span>
<span data-ttu-id="b9b5c-105">Azure 提供內建診斷功能，可協助對 [App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-105">Azure provides built-in diagnostics to assist with debugging an [App Service web app](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="b9b5c-106">本文將說明如何啟用診斷記錄，並在您的應用程式中加入檢測，以及如何存取 Azure 所記錄的資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-106">In this article you'll learn how to enable diagnostic logging and add instrumentation to your application, as well as how to access the information logged by Azure.</span></span>

<span data-ttu-id="b9b5c-107">本文使用 [Azure 入口網站](https://portal.azure.com)、Azure PowerShell 及 Azure 命令列介面 (Azure CLI) 來處理診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-107">This article uses the [Azure Portal](https://portal.azure.com), Azure PowerShell, and the Azure Command-Line Interface (Azure CLI) to work with diagnostic logs.</span></span> <span data-ttu-id="b9b5c-108">如需使用 Visual Studio 來處理診斷記錄的詳細資訊，請參閱 [在 Visual Studio 中疑難排解 Azure](web-sites-dotnet-troubleshoot-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-108">For information on working with diagnostic logs using Visual Studio, see [Troubleshooting Azure in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="b9b5c-109"><a name="whatisdiag"></a>Web 伺服器診斷和應用程式診斷</span><span class="sxs-lookup"><span data-stu-id="b9b5c-109"><a name="whatisdiag"></a>Web server diagnostics and application diagnostics</span></span>
<span data-ttu-id="b9b5c-110">App Service Web 應用程式會針對來自 Web 伺服器和 Web 應用程式的記錄資訊提供診斷功能。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-110">App Service web apps provide diagnostic functionality for logging information from both the web server and the web application.</span></span> <span data-ttu-id="b9b5c-111">這些資訊邏輯上可區分為 [Web 伺服器診斷] 與 [應用程式診斷]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-111">These are logically separated into **web server diagnostics** and **application diagnostics**.</span></span>

### <a name="web-server-diagnostics"></a><span data-ttu-id="b9b5c-112">Web 伺服器診斷</span><span class="sxs-lookup"><span data-stu-id="b9b5c-112">Web server diagnostics</span></span>
<span data-ttu-id="b9b5c-113">您可以啟用或停用下列各種記錄：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-113">You can enable or disable the following kinds of logs:</span></span>

* <span data-ttu-id="b9b5c-114">**詳細的錯誤記錄** - 對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-114">**Detailed Error Logging** - Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span> <span data-ttu-id="b9b5c-115">這當中包含的資訊可協助您判斷為何伺服器傳回錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-115">This may contain information that can help determine why the server returned the error code.</span></span>
* <span data-ttu-id="b9b5c-116">**失敗的要求追蹤** - 關於失敗要求的詳細資訊，包括用於處理要求的 IIS 元件追蹤，以及每個元件所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-116">**Failed Request Tracing** - Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span> <span data-ttu-id="b9b5c-117">如果您嘗試提升網站效能或是想要從傳回的特定 HTTP 錯誤中找到發生原因，這個方法非常實用。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-117">This can be useful if you are attempting to increase site performance or isolate what is causing a specific HTTP error to be returned.</span></span>
* <span data-ttu-id="b9b5c-118">**Web 伺服器記錄** - 使用 [W3C 擴充記錄檔格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)的 HTTP 交易相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-118">**Web Server Logging** - Information about HTTP transactions using the [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> <span data-ttu-id="b9b5c-119">當您需要判斷整體網站指標 (例如，處理的要求數量，或者有多少要求來自特定的 IP 位址) 時，這非常實用。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-119">This is useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="b9b5c-120">應用程式診斷</span><span class="sxs-lookup"><span data-stu-id="b9b5c-120">Application diagnostics</span></span>
<span data-ttu-id="b9b5c-121">應用程式診斷功能可讓您擷取 Web 應用程式所產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-121">Application diagnostics allows you to capture information produced by a web application.</span></span> <span data-ttu-id="b9b5c-122">ASP.NET 應用程式會使用 [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) 類別將資訊記錄到應用程式診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-122">ASP.NET applications can use the [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) class to log information to the application diagnostics log.</span></span> <span data-ttu-id="b9b5c-123">例如：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-123">For example:</span></span>

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

<span data-ttu-id="b9b5c-124">您可以在執行階段擷取這些記錄檔，以協助疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-124">At runtime you can retrieve these logs to help with troubleshooting.</span></span> <span data-ttu-id="b9b5c-125">如需詳細資訊，請參閱 [在 Visual Studio 中疑難排解 Azure Web 應用程式](web-sites-dotnet-troubleshoot-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-125">For more information, see [Troubleshooting Azure web apps in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

<span data-ttu-id="b9b5c-126">當您將內容發行至 Web 應用程式時，App Service Web 應用程式也會記錄部署資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-126">App Service web apps also log deployment information when you publish content to a web app.</span></span> <span data-ttu-id="b9b5c-127">此動作會自動發生，因此無須任何組態設定即會記錄部署動作。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-127">This happens automatically and there are no configuration settings for deployment logging.</span></span> <span data-ttu-id="b9b5c-128">部署記錄功能可讓您判斷部署失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-128">Deployment logging allows you to determine why a deployment failed.</span></span> <span data-ttu-id="b9b5c-129">例如，如果您是使用自訂的部署指令碼，則您可以使用部署記錄功能來判斷指令碼失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-129">For example, if you are using a custom deployment script, you might use deployment logging to determine why the script is failing.</span></span>

## <span data-ttu-id="b9b5c-130"><a name="enablediag"></a>如何啟用診斷</span><span class="sxs-lookup"><span data-stu-id="b9b5c-130"><a name="enablediag"></a>How to enable diagnostics</span></span>
<span data-ttu-id="b9b5c-131">若要在 [Azure 入口網站](https://portal.azure.com)中啟用診斷，請移至 Web 應用程式的刀鋒視窗，然後依序按一下 [設定] > [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-131">To enable diagnostics in the [Azure Portal](https://portal.azure.com), go to the blade for your web app and click **Settings > Diagnostics logs**.</span></span>

<!-- todo:cleanup dogfood addresses in screenshot -->
![記錄部分](./media/web-sites-enable-diagnostic-log/logspart.png)

<span data-ttu-id="b9b5c-133">啟用 [應用程式診斷] 時，也會選擇 [層級]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-133">When you enable **application diagnostics** you also choose the **Level**.</span></span> <span data-ttu-id="b9b5c-134">此設定可讓您篩選擷取至**資訊**、**警告**或**錯誤**資訊中的資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-134">This setting allows you to filter the information captured to **informational**, **warning** or **error** information.</span></span> <span data-ttu-id="b9b5c-135">將此功能設為 [詳細資訊] 會記錄所有由該應用程式所產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-135">Setting this to **verbose** will log all information produced by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-136">與變更 web.config 檔案不同，啟用應用程式診斷或是變更診斷記錄層級並不會回收用來執行應用程式的應用程式網域。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-136">Unlike changing the web.config file, enabling Application diagnostics or changing diagnostic log levels does not recycle the app domain that the application runs within.</span></span>
>
>

<span data-ttu-id="b9b5c-137">在[傳統入口網站](https://manage.windowsazure.com) Web 應用程式的 [設定] 索引標籤中，您可以針對 [Web 伺服器記錄] 選取 [儲存體] 或 [檔案系統]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-137">In the [classic portal](https://manage.windowsazure.com) Web app **Configure** tab, you can select **storage** or **file system** for **web server logging**.</span></span> <span data-ttu-id="b9b5c-138">選取 [儲存]  可讓您選取儲存體帳戶，並接著選取可供寫入記錄的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-138">Selecting **storage** allows you to select a storage account, and then a blob container that the logs will be written to.</span></span> <span data-ttu-id="b9b5c-139">[網站診斷] 的其他所有記錄  都只會寫入檔案系統。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-139">All other logs for **site diagnostics** are written to the file system only.</span></span>

<span data-ttu-id="b9b5c-140">[傳統入口網站](https://manage.windowsazure.com) Web 應用程式的 [設定] 索引標籤也有其他應用程式診斷的設定：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-140">The [classic portal](https://manage.windowsazure.com) Web app **Configure** tab also has additional settings for application diagnostics:</span></span>

* <span data-ttu-id="b9b5c-141">**檔案系統** - 將應用程式診斷資訊儲存至 Web 應用程式檔案系統。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-141">**File system** - stores the application diagnostics information to the web app file system.</span></span> <span data-ttu-id="b9b5c-142">這些檔案可透過 FTP 存取，或是使用 Azure PowerShell 或 Azure 命令列介面 (Azure CLI) 下載為 Zip 封存。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-142">These files can be accessed by FTP, or downloaded as a Zip archive by using the Azure PowerShell or Azure Command-Line Interface (Azure CLI).</span></span>
* <span data-ttu-id="b9b5c-143">**資料表儲存體** - 會將應用程式診斷資訊儲存至指定的 Azure 儲存體帳戶與資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-143">**Table storage** - stores the application diagnostics information in the specified Azure Storage Account and table name.</span></span>
* <span data-ttu-id="b9b5c-144">**Blob 儲存體** - 會將應用程式診斷資訊儲存至指定的 Azure 儲存體帳戶與 Blob 容器中。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-144">**Blob storage** - stores the application diagnostics information in the specified Azure Storage Account and blob container.</span></span>
* <span data-ttu-id="b9b5c-145">**保留週期** - 依預設，所有記錄不會自動從 [Blob 儲存體] 中刪除。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-145">**Retention period** - by default, logs are not automatically deleted from **blob storage**.</span></span> <span data-ttu-id="b9b5c-146">如果您想要讓系統自動刪除記錄的話，請選取 [set retention]  並輸入記錄保留天數。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-146">Select **set retention** and enter the number of days to keep logs if you wish to automatically delete logs.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-147">如果您 [重新產生儲存體帳戶的存取金鑰](../storage/common/storage-create-storage-account.md)，您必須重設個別的記錄組態，才能使用更新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-147">If you [regenerate your storage account's access keys](../storage/common/storage-create-storage-account.md), you must reset the respective logging configuration to use the updated keys.</span></span> <span data-ttu-id="b9b5c-148">作法：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-148">To do this:</span></span>
>
> 1. <span data-ttu-id="b9b5c-149">在 [設定] 索引標籤上，將個別的記錄功能設定為 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-149">In the **Configure** tab, set the respective logging feature to **Off**.</span></span> <span data-ttu-id="b9b5c-150">儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-150">Save your setting.</span></span>
> 2. <span data-ttu-id="b9b5c-151">重新啟用記錄至儲存體帳戶 Blob 或資料表。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-151">Enable logging to the storage account blob or table again.</span></span> <span data-ttu-id="b9b5c-152">儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-152">Save your setting.</span></span>
>
>

<span data-ttu-id="b9b5c-153">包括檔案系統、資料表儲存體或是 Blob 儲存體都可以任意組合並同時啟用，並個別具有記錄層級組態。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-153">Any combination of file system, table storage, or blob storage can be enabled at the same time, and have individual log level configurations.</span></span> <span data-ttu-id="b9b5c-154">例如，您也許想要將各種錯誤與警告資訊記錄到 Blob 儲存體做為長期的記錄解決方案，同時啟用詳細資訊層級的檔案系統記錄功能。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-154">For example, you may wish to log errors and warnings to blob storage as a long-term logging solution, while enabling file system logging with a level of verbose.</span></span>

<span data-ttu-id="b9b5c-155">雖然以上三個儲存位置全都提供相同的基本資訊供您記錄事件，[資料表儲存體] 與 [Blob 儲存體] 會比 [檔案系統] 記錄更多的資訊，例如執行個體識別碼、執行緒識別碼以及更細緻的時間戳記 (刻度格式)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-155">While all three storage locations provide the same basic information for logged events, **table storage** and **blob storage** log additional information such as the instance ID, thread ID, and a more granular timestamp (tick format) than logging to **file system**.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-156">儲存在 [資料表儲存體] 或 [Blob 儲存體] 內的資訊只能透過儲存用戶端，或是能夠直接使用這些儲存系統的應用程式來存取。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-156">Information stored in **table storage** or **blob  storage** can only be accessed using a storage client or an application that can directly work with these storage systems.</span></span> <span data-ttu-id="b9b5c-157">例如，Visual Studio 2013 內含的 [儲存體總管] 可用來探索資料表或 Blob 儲存體，而 HDInsight 則可存取儲存在 Blob 儲存體內的資料。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-157">For example, Visual Studio 2013 contains a Storage Explorer that can be used to explore table or blob storage, and HDInsight can access data stored in blob storage.</span></span> <span data-ttu-id="b9b5c-158">您也可以使用任何一項 [Azure SDK](/downloads/#)，撰寫可存取 Azure 儲存體的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-158">You can also write an application that accesses Azure Storage by using one of the [Azure SDKs](/downloads/#).</span></span>
>
> [!NOTE]
> <span data-ttu-id="b9b5c-159">您也可以在 Azure PowerShell 中使用 **Set-AzureWebsite** Cmdlet 來啟用診斷功能。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-159">Diagnostics can also be enabled from Azure PowerShell using the **Set-AzureWebsite** cmdlet.</span></span> <span data-ttu-id="b9b5c-160">如果您尚未安裝 Azure PowerShell，或尚未將其設定為使用 Azure 訂閱，請參閱 [如何使用 Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-160">If you have not installed Azure PowerShell, or have not configured it to use your Azure Subscription, see [How to Use Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

## <span data-ttu-id="b9b5c-161"><a name="download"></a> 作法：下載記錄</span><span class="sxs-lookup"><span data-stu-id="b9b5c-161"><a name="download"></a> How to: Download logs</span></span>
<span data-ttu-id="b9b5c-162">儲存在 Web 應用程式檔案系統中的診斷資訊，可透過 FTP 直接存取。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-162">Diagnostic information stored to the web app file system can be accessed directly using FTP.</span></span> <span data-ttu-id="b9b5c-163">或是使用 Azure PowerShell 或 Azure 命令列介面下載為 Zip 封存。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-163">It can also be downloaded as a Zip archive using Azure PowerShell or the Azure Command-Line Interface.</span></span>

<span data-ttu-id="b9b5c-164">儲存這些記錄的目錄結構如下所示：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-164">The directory structure that the logs are stored in is as follows:</span></span>

* <span data-ttu-id="b9b5c-165">**應用程式記錄** - /LogFiles/Application/。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-165">**Application logs** - /LogFiles/Application/.</span></span> <span data-ttu-id="b9b5c-166">此資料夾內含有一或多個文字檔案，這些檔案涵蓋應用程式記錄所產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-166">This folder contains one or more text files containing information produced by application logging.</span></span>
* <span data-ttu-id="b9b5c-167">**失敗要求追蹤** - /LogFiles/W3SVC#########/。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-167">**Failed Request Traces** - /LogFiles/W3SVC#########/.</span></span> <span data-ttu-id="b9b5c-168">此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-168">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="b9b5c-169">請確保將 XSL 檔案下載至 XML 檔案所在的相同目錄，因為 XSL 檔案可提供格式化功能，讓您在 Internet Explorer 中檢視時能夠篩選 XML 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-169">Ensure that you download the XSL file into the same directory as the XML file(s) because the XSL file provides functionality for formatting and filtering the contents of the XML file(s) when viewed in Internet Explorer.</span></span>
* <span data-ttu-id="b9b5c-170">**詳細錯誤記錄** - /LogFiles/DetailedErrors/。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-170">**Detailed Error Logs** - /LogFiles/DetailedErrors/.</span></span> <span data-ttu-id="b9b5c-171">此資料夾包含一或多個 .htm 檔案，內含已經發生的任何 HTTP 錯誤之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-171">This folder contains one or more .htm files that provide extensive information for any HTTP errors that have occurred.</span></span>
* <span data-ttu-id="b9b5c-172">**Web 伺服器記錄** - /LogFiles/http/RawLogs。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-172">**Web Server Logs** - /LogFiles/http/RawLogs.</span></span> <span data-ttu-id="b9b5c-173">此資料夾包含一或多個運用 [W3C 擴充記錄檔格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)來格式化的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-173">This folder contains one or more text files formatted using the [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
* <span data-ttu-id="b9b5c-174">**部署記錄** - /LogFiles/Git。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-174">**Deployment logs** - /LogFiles/Git.</span></span> <span data-ttu-id="b9b5c-175">此資料夾包含由內部部署處理序所產生，且可供 Azure Web 應用程式運用的記錄，以及適用於 Git 部署的記錄。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-175">This folder contains logs generated by the internal deployment processes used by Azure web apps, as well as logs for Git deployments.</span></span>

### <a name="ftp"></a><span data-ttu-id="b9b5c-176">FTP</span><span class="sxs-lookup"><span data-stu-id="b9b5c-176">FTP</span></span>
<span data-ttu-id="b9b5c-177">若要使用 FTP 存取診斷資訊，請在[傳統入口網站](https://manage.windowsazure.com)中造訪您 Web 應用程式的 [儀表板]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-177">To access diagnostic information using FTP, visit the **Dashboard** of your web app in the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="b9b5c-178">在 [Quick Glance] 區段中，使用 **FTP Diagnostic Logs** 連結以便透過 FTP 存取記錄檔案。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-178">In the **quick glance** section, use the **FTP Diagnostic Logs** link to access the log files using FTP.</span></span> <span data-ttu-id="b9b5c-179">[Deployment/FTP User] 項目會列出應該用來存取 FTP 網站的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-179">The **Deployment/FTP User** entry lists the user name that should be used to access the FTP site.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-180">如果未設定的 [部署/FTP 使用者] 項目，或是您忘記此使用者的密碼，您可以使用 [儀表板] 的 [快速概覽] 區段中**重設部署認證**連結來建立新的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-180">If the **Deployment/FTP User** entry is not set, or you have forgotten the password for this user, you can create a new user and password by using the **Reset deployment credentials** link in the **quick glance** section of the **Dashboard**.</span></span>
>
>

### <a name="download-with-azure-powershell"></a><span data-ttu-id="b9b5c-181">使用 Azure PowerShell 來下載</span><span class="sxs-lookup"><span data-stu-id="b9b5c-181">Download with Azure PowerShell</span></span>
<span data-ttu-id="b9b5c-182">若要下載記錄檔，請啟動新的 Azure PowerShell 執行個體並使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-182">To download the log files, start a new instance of Azure PowerShell and use the following command:</span></span>

    Save-AzureWebSiteLog -Name webappname

<span data-ttu-id="b9b5c-183">此舉會將 **-Name** 參數所指定的 Web 應用程式記錄儲存到目前目錄中名為 **logs.zip** 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-183">This will save the logs for the web app specified by the **-Name** parameter to a file named **logs.zip** in the current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-184">如果您尚未安裝 Azure PowerShell，或尚未將其設定為使用 Azure 訂閱，請參閱 [如何使用 Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-184">If you have not installed Azure PowerShell, or have not configured it to use your Azure Subscription, see [How to Use Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

### <a name="download-with-azure-command-line-interface"></a><span data-ttu-id="b9b5c-185">使用 Azure 命列列介面來下載</span><span class="sxs-lookup"><span data-stu-id="b9b5c-185">Download with Azure Command-Line Interface</span></span>
<span data-ttu-id="b9b5c-186">若要使用 Azure 命令列介面來下載記錄檔案，請開啟新的命令列提示字元、PowerShell、Bash 或終端機工作階段，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-186">To download the log files using the Azure Command Line Interface, open a new command prompt, PowerShell, Bash, or Terminal session and enter the following command:</span></span>

    azure site log download webappname

<span data-ttu-id="b9b5c-187">此舉會將名為 'webappname' 的 Web 應用程式記錄儲存至目前目錄中名為 **diagnostics.zip** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-187">This will save the logs for the web app named 'webappname' to a file named **diagnostics.zip** in the current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-188">如果您尚未安裝 Azure 命令列介面 (Azure CLI)，或是尚未將其設定為使用您的 Azure 訂用帳戶，請參閱 [如何使用 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-188">If you have not installed the Azure Command-Line Interface (Azure CLI), or have not configured it to use your Azure Subscription, see [How to Use Azure CLI](../cli-install-nodejs.md).</span></span>
>
>

## <a name="how-to-view-logs-in-application-insights"></a><span data-ttu-id="b9b5c-189">作法：在 Application Insights 中檢視記錄</span><span class="sxs-lookup"><span data-stu-id="b9b5c-189">How to: View logs in Application Insights</span></span>
<span data-ttu-id="b9b5c-190">Visual Studio Application Insights 提供篩選與搜尋記錄的工具，以及將記錄與要求及其他事件建立相互關聯的工具。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-190">Visual Studio Application Insights provides tools for filtering and searching logs, and for correlating the logs with requests and other events.</span></span>

1. <span data-ttu-id="b9b5c-191">在 Visual Studio 中將 Application Insights SDK 加入至專案。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-191">Add the Application Insights SDK to your project in Visual Studio.</span></span>
   * <span data-ttu-id="b9b5c-192">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選擇 [加入 Application Insights]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-192">In Solution Explorer, right click your project and choose Add Application Insights.</span></span> <span data-ttu-id="b9b5c-193">系統將指導您完成包括建立 Application Insights 資源在內的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-193">You'll be guided through steps that include creating an Application Insights resource.</span></span> [<span data-ttu-id="b9b5c-194">深入了解</span><span class="sxs-lookup"><span data-stu-id="b9b5c-194">Learn more</span></span>](../application-insights/app-insights-asp-net.md)
2. <span data-ttu-id="b9b5c-195">將追蹤接聽套件新增至專案。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-195">Add the Trace Listener package to your project.</span></span>
   * <span data-ttu-id="b9b5c-196">以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-196">Right click your project and choose Manage NuGet Packages.</span></span> <span data-ttu-id="b9b5c-197">選取 `Microsoft.ApplicationInsights.TraceListener` [深入了解](../application-insights/app-insights-asp-net-trace-logs.md)</span><span class="sxs-lookup"><span data-stu-id="b9b5c-197">Select `Microsoft.ApplicationInsights.TraceListener` [Learn more](../application-insights/app-insights-asp-net-trace-logs.md)</span></span>
3. <span data-ttu-id="b9b5c-198">上傳您的專案並執行，以產生記錄資料。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-198">Upload your project and run it to generate log data.</span></span>
4. <span data-ttu-id="b9b5c-199">在 [Azure 入口網站](https://portal.azure.com/)中，瀏覽至您新的 Application Insights 資源，然後開啟 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-199">In the [Azure Portal](https://portal.azure.com/), browse to your new Application Insights resource, and open **Search**.</span></span> <span data-ttu-id="b9b5c-200">您將會看到您的記錄資料，以及要求、使用情況及其他遙測。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-200">You'll see your log data, along with request, usage and other telemetry.</span></span> <span data-ttu-id="b9b5c-201">有些遙測可能需要數分鐘才能抵達：按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-201">Some telemetry might take a few minutes to arrive: click Refresh.</span></span> [<span data-ttu-id="b9b5c-202">深入了解</span><span class="sxs-lookup"><span data-stu-id="b9b5c-202">Learn more</span></span>](../application-insights/app-insights-diagnostic-search.md)

[<span data-ttu-id="b9b5c-203">深入了解使用 Application Insights 的效能追蹤</span><span class="sxs-lookup"><span data-stu-id="b9b5c-203">Learn more about performance tracking with Application Insights</span></span>](../application-insights/app-insights-azure-web-apps.md)

## <span data-ttu-id="b9b5c-204"><a name="streamlogs"></a> 作法：串流記錄</span><span class="sxs-lookup"><span data-stu-id="b9b5c-204"><a name="streamlogs"></a> How to: Stream logs</span></span>
<span data-ttu-id="b9b5c-205">開發應用程式時，如果能夠幾近即時地檢視記錄資訊，通常會很實用。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-205">While developing an application, it is often useful to see logging information in near-real time.</span></span> <span data-ttu-id="b9b5c-206">您可以使用 Azure PowerShell 或 Azure 命令列介面，將記錄資訊串流至開發環境來達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-206">This can be accomplished by streaming logging information to your development environment using either Azure PowerShell or the Azure Command-Line Interface.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-207">某些記錄緩衝區類型會寫入記錄檔中，進而造成串流中的事件順序錯亂。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-207">Some types of logging buffer write to the log file, which can result in out of order events in the stream.</span></span> <span data-ttu-id="b9b5c-208">例如，使用者造訪某個網頁所產生的應用程式記錄項目，可能會比頁面要求的對應 HTTP 記錄項目優先顯示在串流中。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-208">For example, an application log entry that occurs when a user visits a page may be displayed in the stream before the corresponding HTTP log entry for the page request.</span></span>
>
> [!NOTE]
> <span data-ttu-id="b9b5c-209">記錄串流也會將串流資訊寫入儲存於 **D:\\home\\LogFiles\\** 資料夾中的任何文字檔。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-209">Log streaming will also stream information written to any text file stored in the **D:\\home\\LogFiles\\** folder.</span></span>
>
>

### <a name="streaming-with-azure-powershell"></a><span data-ttu-id="b9b5c-210">使用 Azure PowerShell 來串流</span><span class="sxs-lookup"><span data-stu-id="b9b5c-210">Streaming with Azure PowerShell</span></span>
<span data-ttu-id="b9b5c-211">若要串流記錄資訊，請啟動新的 Azure PowerShell 執行個體並使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-211">To stream logging information, start a new instance of Azure PowerShell and use the following command:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail

<span data-ttu-id="b9b5c-212">此舉會連線 **-Name** 參數所指定的 Web 應用程式，並在該 Web 應用程式產生記錄事件時，開始將資訊串流至 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-212">This will connect to the web app specified by the **-Name** parameter and begin streaming information to the PowerShell window as log events occur on the web app.</span></span> <span data-ttu-id="b9b5c-213">任何寫入副檔名為 .txt、.log 或 .htm 的檔案中並存放在 /LogFiles 目錄 (d:/home/logfiles) 的資訊，都會串流至本機主控台。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-213">Any information written to files ending in .txt, .log, or .htm that are stored in the /LogFiles directory (d:/home/logfiles) will be streamed to the local console.</span></span>

<span data-ttu-id="b9b5c-214">若要篩選特定事件，例如錯誤，請使用 **-Message** 參數。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-214">To filter specific events, such as errors, use the **-Message** parameter.</span></span> <span data-ttu-id="b9b5c-215">例如：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-215">For example:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

<span data-ttu-id="b9b5c-216">若要篩選特定記錄類型，例如 HTTP，請使用 **-Path** 參數。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-216">To filter specific log types, such as HTTP, use the **-Path** parameter.</span></span> <span data-ttu-id="b9b5c-217">例如：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-217">For example:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

<span data-ttu-id="b9b5c-218">若要檢視可用的路徑清單，請使用 -ListPath 參數。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-218">To see a list of available paths, use the -ListPath parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-219">如果您尚未安裝 Azure PowerShell，或尚未將其設定為使用 Azure 訂閱，請參閱 [如何使用 Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-219">If you have not installed Azure PowerShell, or have not configured it to use your Azure Subscription, see [How to Use Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

### <a name="streaming-with-azure-command-line-interface"></a><span data-ttu-id="b9b5c-220">使用 Azure 命令列介面來串流</span><span class="sxs-lookup"><span data-stu-id="b9b5c-220">Streaming with Azure Command-Line Interface</span></span>
<span data-ttu-id="b9b5c-221">若要串流記錄資訊，請開啟新的命列列提示字元、PowerShell、Bash 或終端機工作階段，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-221">To stream logging information, open a new command prompt, PowerShell, Bash, or Terminal session and enter the following command:</span></span>

    azure site log tail webappname

<span data-ttu-id="b9b5c-222">這會連接至名為 'webappname' 的 Web 應用程式，並在該 Web 應用程式產生記錄事件時，開始將資訊串流至視窗。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-222">This will connect to the web app named 'webappname' and begin streaming information to the window as log events occur on the web app.</span></span> <span data-ttu-id="b9b5c-223">任何寫入副檔名為 .txt、.log 或 .htm 的檔案中並存放在 /LogFiles 目錄 (d:/home/logfiles) 的資訊，都會串流至本機主控台。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-223">Any information written to files ending in .txt, .log, or .htm that are stored in the /LogFiles directory (d:/home/logfiles) will be streamed to the local console.</span></span>

<span data-ttu-id="b9b5c-224">若要篩選特定事件，例如錯誤，請使用 **--Filter** 參數。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-224">To filter specific events, such as errors, use the **--Filter** parameter.</span></span> <span data-ttu-id="b9b5c-225">例如：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-225">For example:</span></span>

    azure site log tail webappname --filter Error

<span data-ttu-id="b9b5c-226">若要篩選特定記錄類型，例如 HTTP，請使用 **--Path** 參數。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-226">To filter specific log types, such as HTTP, use the **--Path** parameter.</span></span> <span data-ttu-id="b9b5c-227">例如：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-227">For example:</span></span>

    azure site log tail webappname --path http

> [!NOTE]
> <span data-ttu-id="b9b5c-228">如果您尚未安裝 Azure 命令列介面，或是尚未將其設定為使用您的 Azure 訂用帳戶，請參閱 [如何使用 Azure 命令列介面](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-228">If you have not installed the Azure Command-Line Interface, or have not configured it to use your Azure Subscription, see [How to Use Azure Command-Line Interface](../cli-install-nodejs.md).</span></span>
>
>

## <span data-ttu-id="b9b5c-229"><a name="understandlogs"></a> 作法：了解診斷記錄</span><span class="sxs-lookup"><span data-stu-id="b9b5c-229"><a name="understandlogs"></a> How to: Understand diagnostics logs</span></span>
### <a name="application-diagnostics-logs"></a><span data-ttu-id="b9b5c-230">應用程式診斷記錄</span><span class="sxs-lookup"><span data-stu-id="b9b5c-230">Application diagnostics logs</span></span>
<span data-ttu-id="b9b5c-231">應用程式診斷功能會根據您將記錄儲存至檔案系統、資料表儲存體或 Blob 儲存體的不同，將 .NET 應用程式的資訊儲存為特定格式。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-231">Application diagnostics stores information in a specific format for .NET applications, depending on whether you store logs to the file system, table storage, or blob storage.</span></span> <span data-ttu-id="b9b5c-232">這三種儲存類型所儲存的資料基底集合全都相同，包括事件發生的日期與時間、產生事件的處理序識別碼、事件類型 (資訊、警告與錯誤)，以及事件訊息。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-232">The base set of data stored is the same across all three storage types - the date and time the event occurred, the process ID that produced the event, the event type (information, warning, error,) and the event message.</span></span>

<span data-ttu-id="b9b5c-233">**檔案系統**</span><span class="sxs-lookup"><span data-stu-id="b9b5c-233">**File system**</span></span>

<span data-ttu-id="b9b5c-234">每一行記錄到檔案系統的訊息，或是透過串流方式收到的訊息，都將採下列格式：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-234">Each line logged to the file system or received using streaming will be in the following format:</span></span>

    {Date}  PID[{process id}] {event type/level} {message}

<span data-ttu-id="b9b5c-235">例如，錯誤事件可能會類似下列訊息：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-235">For example, an error event would appear similar to the following:</span></span>

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on the page!

<span data-ttu-id="b9b5c-236">記錄到檔案系統可針對三種可用的方法提供最基本的資訊，亦即僅提供時間、處理序識別碼、事件層級與訊息。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-236">Logging to the file system provides the most basic information of the three available methods, providing only the time, process id, event level, and message.</span></span>

<span data-ttu-id="b9b5c-237">**資料表儲存體**</span><span class="sxs-lookup"><span data-stu-id="b9b5c-237">**Table storage**</span></span>

<span data-ttu-id="b9b5c-238">記錄至資料表儲存體時，會使用其他屬性來協助搜尋儲存在資料表裡的資料，以及更精細的事件資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-238">When logging to table storage, additional properties are used to facilitate searching the data stored in the table as well as more granular information on the event.</span></span> <span data-ttu-id="b9b5c-239">以下內容 (資料行) 會用於資料表中儲存的每個實體 (列)。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-239">The following properties (columns) are used for each entity (row) stored in the table.</span></span>

| <span data-ttu-id="b9b5c-240">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="b9b5c-240">Property name</span></span> | <span data-ttu-id="b9b5c-241">值/格式</span><span class="sxs-lookup"><span data-stu-id="b9b5c-241">Value/format</span></span> |
| --- | --- |
| <span data-ttu-id="b9b5c-242">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="b9b5c-242">PartitionKey</span></span> |<span data-ttu-id="b9b5c-243">格式為 yyyyMMddHH 的事件日期/時間</span><span class="sxs-lookup"><span data-stu-id="b9b5c-243">Date/time of the event in yyyyMMddHH format</span></span> |
| <span data-ttu-id="b9b5c-244">RowKey</span><span class="sxs-lookup"><span data-stu-id="b9b5c-244">RowKey</span></span> |<span data-ttu-id="b9b5c-245">可唯一識別此實體的 GUID 值</span><span class="sxs-lookup"><span data-stu-id="b9b5c-245">A GUID value that uniquely identifies this entity</span></span> |
| <span data-ttu-id="b9b5c-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="b9b5c-246">Timestamp</span></span> |<span data-ttu-id="b9b5c-247">事件發生的日期與時間</span><span class="sxs-lookup"><span data-stu-id="b9b5c-247">The date and time that the event occurred</span></span> |
| <span data-ttu-id="b9b5c-248">EventTickCount</span><span class="sxs-lookup"><span data-stu-id="b9b5c-248">EventTickCount</span></span> |<span data-ttu-id="b9b5c-249">事件發生的日期與時間 (刻度格式，精準度更高)</span><span class="sxs-lookup"><span data-stu-id="b9b5c-249">The date and time that the event occurred, in Tick format (greater precision)</span></span> |
| <span data-ttu-id="b9b5c-250">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="b9b5c-250">ApplicationName</span></span> |<span data-ttu-id="b9b5c-251">Web 應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="b9b5c-251">The web app name</span></span> |
| <span data-ttu-id="b9b5c-252">等級</span><span class="sxs-lookup"><span data-stu-id="b9b5c-252">Level</span></span> |<span data-ttu-id="b9b5c-253">事件層級 (例如，錯誤、警告、資訊)</span><span class="sxs-lookup"><span data-stu-id="b9b5c-253">Event level (e.g. error, warning, information)</span></span> |
| <span data-ttu-id="b9b5c-254">EventId</span><span class="sxs-lookup"><span data-stu-id="b9b5c-254">EventId</span></span> |<span data-ttu-id="b9b5c-255">如果沒有指定</span><span class="sxs-lookup"><span data-stu-id="b9b5c-255">The event ID of this event</span></span><p><p><span data-ttu-id="b9b5c-256">這個事件的事件識別碼，則預設為 0</span><span class="sxs-lookup"><span data-stu-id="b9b5c-256">Defaults to 0 if none specified</span></span> |
| <span data-ttu-id="b9b5c-257">InstanceId</span><span class="sxs-lookup"><span data-stu-id="b9b5c-257">InstanceId</span></span> |<span data-ttu-id="b9b5c-258">發生事件的 Web 應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="b9b5c-258">Instance of the web app that the even occurred on</span></span> |
| <span data-ttu-id="b9b5c-259">Pid</span><span class="sxs-lookup"><span data-stu-id="b9b5c-259">Pid</span></span> |<span data-ttu-id="b9b5c-260">處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="b9b5c-260">Process ID</span></span> |
| <span data-ttu-id="b9b5c-261">Tid</span><span class="sxs-lookup"><span data-stu-id="b9b5c-261">Tid</span></span> |<span data-ttu-id="b9b5c-262">產生事件的執行緒之執行緒識別碼</span><span class="sxs-lookup"><span data-stu-id="b9b5c-262">The thread ID of the thread that produced the event</span></span> |
| <span data-ttu-id="b9b5c-263">訊息</span><span class="sxs-lookup"><span data-stu-id="b9b5c-263">Message</span></span> |<span data-ttu-id="b9b5c-264">事件詳細資訊訊息</span><span class="sxs-lookup"><span data-stu-id="b9b5c-264">Event detail message</span></span> |

<span data-ttu-id="b9b5c-265">**Blob 儲存體**</span><span class="sxs-lookup"><span data-stu-id="b9b5c-265">**Blob storage**</span></span>

<span data-ttu-id="b9b5c-266">登入 Blob 儲存體時，資料會儲存為逗號分隔值 (CSV) 的格式。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-266">When logging to blob storage, data is stored in comma-separated values (CSV) format.</span></span> <span data-ttu-id="b9b5c-267">其他欄位則會以類似資料表儲存體的作法記錄起來，以提供更精細的事件相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-267">Similar to table storage, additional fields are logged to provide more granular information about the event.</span></span> <span data-ttu-id="b9b5c-268">CSV 中的每一列會使用以下屬性：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-268">The following properties are used for each row in the CSV:</span></span>

| <span data-ttu-id="b9b5c-269">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="b9b5c-269">Property name</span></span> | <span data-ttu-id="b9b5c-270">值/格式</span><span class="sxs-lookup"><span data-stu-id="b9b5c-270">Value/format</span></span> |
| --- | --- |
| <span data-ttu-id="b9b5c-271">日期</span><span class="sxs-lookup"><span data-stu-id="b9b5c-271">Date</span></span> |<span data-ttu-id="b9b5c-272">事件發生的日期與時間</span><span class="sxs-lookup"><span data-stu-id="b9b5c-272">The date and time that the event occurred</span></span> |
| <span data-ttu-id="b9b5c-273">等級</span><span class="sxs-lookup"><span data-stu-id="b9b5c-273">Level</span></span> |<span data-ttu-id="b9b5c-274">事件層級 (例如，錯誤、警告、資訊)</span><span class="sxs-lookup"><span data-stu-id="b9b5c-274">Event level (e.g. error, warning, information)</span></span> |
| <span data-ttu-id="b9b5c-275">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="b9b5c-275">ApplicationName</span></span> |<span data-ttu-id="b9b5c-276">Web 應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="b9b5c-276">The web app name</span></span> |
| <span data-ttu-id="b9b5c-277">InstanceId</span><span class="sxs-lookup"><span data-stu-id="b9b5c-277">InstanceId</span></span> |<span data-ttu-id="b9b5c-278">發生事件的 Web 應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="b9b5c-278">Instance of the web app that the event occurred on</span></span> |
| <span data-ttu-id="b9b5c-279">EventTickCount</span><span class="sxs-lookup"><span data-stu-id="b9b5c-279">EventTickCount</span></span> |<span data-ttu-id="b9b5c-280">事件發生的日期與時間 (刻度格式，精準度更高)</span><span class="sxs-lookup"><span data-stu-id="b9b5c-280">The date and time that the event occurred, in Tick format (greater precision)</span></span> |
| <span data-ttu-id="b9b5c-281">EventId</span><span class="sxs-lookup"><span data-stu-id="b9b5c-281">EventId</span></span> |<span data-ttu-id="b9b5c-282">如果沒有指定</span><span class="sxs-lookup"><span data-stu-id="b9b5c-282">The event ID of this event</span></span><p><p><span data-ttu-id="b9b5c-283">這個事件的事件識別碼，則預設為 0</span><span class="sxs-lookup"><span data-stu-id="b9b5c-283">Defaults to 0 if none specified</span></span> |
| <span data-ttu-id="b9b5c-284">Pid</span><span class="sxs-lookup"><span data-stu-id="b9b5c-284">Pid</span></span> |<span data-ttu-id="b9b5c-285">處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="b9b5c-285">Process ID</span></span> |
| <span data-ttu-id="b9b5c-286">Tid</span><span class="sxs-lookup"><span data-stu-id="b9b5c-286">Tid</span></span> |<span data-ttu-id="b9b5c-287">產生事件的執行緒之執行緒識別碼</span><span class="sxs-lookup"><span data-stu-id="b9b5c-287">The thread ID of the thread that produced the event</span></span> |
| <span data-ttu-id="b9b5c-288">訊息</span><span class="sxs-lookup"><span data-stu-id="b9b5c-288">Message</span></span> |<span data-ttu-id="b9b5c-289">事件詳細資訊訊息</span><span class="sxs-lookup"><span data-stu-id="b9b5c-289">Event detail message</span></span> |

<span data-ttu-id="b9b5c-290">儲存在 Blob 中的資料類似以下內容：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-290">The data stored in a blob would look similar to the following:</span></span>

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> <span data-ttu-id="b9b5c-291">記錄的第一行會包含如此範例所示的資料行標題。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-291">The first line of the log will contain the column headers as represented in this example.</span></span>
>
>

### <a name="failed-request-traces"></a><span data-ttu-id="b9b5c-292">失敗要求追蹤</span><span class="sxs-lookup"><span data-stu-id="b9b5c-292">Failed request traces</span></span>
<span data-ttu-id="b9b5c-293">失敗要求追蹤會儲存在名為 **fr######.xml**的 XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-293">Failed request traces are stored in XML files named **fr######.xml**.</span></span> <span data-ttu-id="b9b5c-294">為了讓您輕鬆地檢視記錄資訊，系統會在 XML 檔案所屬的相同目錄中，提供名為 **freb.xsl** 的 XSL 樣式表。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-294">To make it easier to view the logged information, an XSL stylesheet named **freb.xsl** is provided in the same directory as the XML files.</span></span> <span data-ttu-id="b9b5c-295">在 Internet Explorer 中開啟其中一個 XML 檔案會使用 XSL 樣式表，提供格式化的追蹤資訊顯示。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-295">Opening one of the XML files in Internet Explorer will use the XSL stylesheet to provide a formatted display of the trace information.</span></span> <span data-ttu-id="b9b5c-296">此資訊類似以下內容：</span><span class="sxs-lookup"><span data-stu-id="b9b5c-296">This will appear similar to the following:</span></span>

![在瀏覽器中檢視的失敗要求](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a><span data-ttu-id="b9b5c-298">詳細錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="b9b5c-298">Detailed error logs</span></span>
<span data-ttu-id="b9b5c-299">詳細的錯誤記錄指的是可針對發生的 HTTP 錯誤提供更詳盡資訊的 HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-299">Detailed error logs are HTML documents that provide more detailed information on HTTP errors that have occurred.</span></span> <span data-ttu-id="b9b5c-300">由於它們都是單純的 HTML 文件，因此可以使用網頁瀏覽器來檢視。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-300">Since they are simply HTML documents, they can be viewed using a web browser.</span></span>

### <a name="web-server-logs"></a><span data-ttu-id="b9b5c-301">Web 伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="b9b5c-301">Web server logs</span></span>
<span data-ttu-id="b9b5c-302">Web 伺服器記錄使用 [W3C 擴充記錄檔案格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)來格式化。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-302">The web server logs are formatted using the [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> <span data-ttu-id="b9b5c-303">此項資訊可透過文字編輯器來讀取，或是運用 [記錄檔剖析器](http://go.microsoft.com/fwlink/?LinkId=246619)(英文) 之類的公用程式來剖析。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-303">This information can be read using a text editor or parsed using utilities such as [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619).</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5c-304">Azure Web 應用程式所產生的記錄並不支援 **s-computername**、**s-ip** 或 **cs-version** 欄位。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-304">The logs produced by Azure web apps do not support the **s-computername**, **s-ip**, or **cs-version** fields.</span></span>
>
>

## <span data-ttu-id="b9b5c-305"><a name="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9b5c-305"><a name="nextsteps"></a> Next steps</span></span>
* [<span data-ttu-id="b9b5c-306">如何監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b9b5c-306">How to Monitor Web Apps</span></span>](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [<span data-ttu-id="b9b5c-307">在 Visual Studio 中疑難排解 Azure Web App</span><span class="sxs-lookup"><span data-stu-id="b9b5c-307">Troubleshooting Azure web apps in Visual Studio</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)
* [<span data-ttu-id="b9b5c-308">在 HDInsight 中分析 Web 應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="b9b5c-308">Analyze web app Logs in HDInsight</span></span>](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> <span data-ttu-id="b9b5c-309">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-309">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b9b5c-310">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="b9b5c-310">No credit cards required; no commitments.</span></span>
>
>

## <a name="whats-changed"></a><span data-ttu-id="b9b5c-311">變更的項目</span><span class="sxs-lookup"><span data-stu-id="b9b5c-311">What's changed</span></span>
* <span data-ttu-id="b9b5c-312">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b9b5c-312">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
* <span data-ttu-id="b9b5c-313">如需從舊的入口網站變更為新入口網站的指南，請參閱： [瀏覽 Azure 入口網站的參考](http://go.microsoft.com/fwlink/?LinkId=529715)</span><span class="sxs-lookup"><span data-stu-id="b9b5c-313">For a guide to the change of the old portal to the new portal see: [Reference for navigating the Azure portal](http://go.microsoft.com/fwlink/?LinkId=529715)</span></span>
