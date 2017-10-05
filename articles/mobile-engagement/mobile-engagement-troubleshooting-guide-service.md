---
title: "Azure Mobile Engagement 疑難排解指南 - 服務"
description: "Azure Mobile Engagement 疑難排解"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="46680-103">服務問題的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="46680-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="46680-104">以下是您可能會遇到，有關 Azure Mobile Engagement 執行的問題。</span><span class="sxs-lookup"><span data-stu-id="46680-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="46680-105">服務中斷</span><span class="sxs-lookup"><span data-stu-id="46680-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="46680-106">問題</span><span class="sxs-lookup"><span data-stu-id="46680-106">Issue</span></span>
* <span data-ttu-id="46680-107">似乎是因為 Azure Mobile Engagement 服務中斷所造成的問題。</span><span class="sxs-lookup"><span data-stu-id="46680-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="46680-108">原因</span><span class="sxs-lookup"><span data-stu-id="46680-108">Causes</span></span>
* <span data-ttu-id="46680-109">似乎是因為 Azure Mobile Engagement 服務中斷所造成的問題，可能由數種不同原因所造成：</span><span class="sxs-lookup"><span data-stu-id="46680-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="46680-110">原本顯示為 Azure Mobile Engagement 系統問題的隔離問題</span><span class="sxs-lookup"><span data-stu-id="46680-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="46680-111">伺服器關閉所造成的已知問題 (不一定會顯示在伺服器狀態中)：</span><span class="sxs-lookup"><span data-stu-id="46680-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="46680-112">排程延遲、目標錯誤、徽章更新問題、統計資料停止收集、推播停止運作、API 停止運作、無法建立新的應用程式或使用者、DNS 錯誤，以及 UI、API 或裝置上應用程式中的逾時錯誤。</span><span class="sxs-lookup"><span data-stu-id="46680-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="46680-113">雲端相依性中斷 [Azure 服務狀態](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="46680-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="46680-114">推送通知服務 (PNS) 相依性中斷</span><span class="sxs-lookup"><span data-stu-id="46680-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="46680-115">應用程式商店中斷</span><span class="sxs-lookup"><span data-stu-id="46680-115">App Store Outages</span></span>

1) <span data-ttu-id="46680-116">若要測試是否為系統性問題，您可以從下列不同的位置測試相同的函數</span><span class="sxs-lookup"><span data-stu-id="46680-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="46680-117">Azure Mobile Engagement 整合式應用程式</span><span class="sxs-lookup"><span data-stu-id="46680-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="46680-118">測試裝置</span><span class="sxs-lookup"><span data-stu-id="46680-118">Test device</span></span>
* <span data-ttu-id="46680-119">測試裝置作業系統版本</span><span class="sxs-lookup"><span data-stu-id="46680-119">Test device OS version</span></span>
* <span data-ttu-id="46680-120">活動</span><span class="sxs-lookup"><span data-stu-id="46680-120">Campaign</span></span>
* <span data-ttu-id="46680-121">系統管理員使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="46680-121">Administrator user account</span></span>
* <span data-ttu-id="46680-122">瀏覽器 (IE、Firefox、Chrome 等)</span><span class="sxs-lookup"><span data-stu-id="46680-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="46680-123">電腦</span><span class="sxs-lookup"><span data-stu-id="46680-123">Computer</span></span>

2) <span data-ttu-id="46680-124">若要測試問題是否只影響 UI 或 API：</span><span class="sxs-lookup"><span data-stu-id="46680-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="46680-125">在 Azure Mobile Engagement UI 和 Azure Mobile Engagement API 中測試相同的函數。</span><span class="sxs-lookup"><span data-stu-id="46680-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="46680-126">若要測試是否是您的行動電話網路的問題：</span><span class="sxs-lookup"><span data-stu-id="46680-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="46680-127">測試時透過 WIFI 和 3G 行動電話網路連線到網際網路。</span><span class="sxs-lookup"><span data-stu-id="46680-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="46680-128">確認您的防火牆不會封鎖任何 Azure Mobile Engagement 的 IP 位址或連接埠。</span><span class="sxs-lookup"><span data-stu-id="46680-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="46680-129">若要測試是否是您的裝置的問題：</span><span class="sxs-lookup"><span data-stu-id="46680-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="46680-130">測試您的裝置是否能透過另一個 Azure Mobile Engagement 整合式應用程式連接到 Azure Mobile Engagement。</span><span class="sxs-lookup"><span data-stu-id="46680-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="46680-131">測試您是否可以從手機產生可在 Azure Mobile Engagement UI 中看到的事件、工作和當機情況。</span><span class="sxs-lookup"><span data-stu-id="46680-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="46680-132">測試是否能夠從 Azure Mobile Engagement UI，根據裝置識別碼傳送推播通知給您的裝置。</span><span class="sxs-lookup"><span data-stu-id="46680-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="46680-133">若要測試是否是您的應用程式的問題：</span><span class="sxs-lookup"><span data-stu-id="46680-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="46680-134">從模擬器 (而不是實體裝置)，安裝並測試您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="46680-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="46680-135">若要測試是否是使用者裝置的作業系統升級的問題 (需要升級 SDK 才能解決)：</span><span class="sxs-lookup"><span data-stu-id="46680-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="46680-136">在使用不同作業系統版本的不同裝置上測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="46680-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="46680-137">確認您使用最新版的 SDK。</span><span class="sxs-lookup"><span data-stu-id="46680-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="46680-138">連線和資訊不正確的問題</span><span class="sxs-lookup"><span data-stu-id="46680-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="46680-139">問題</span><span class="sxs-lookup"><span data-stu-id="46680-139">Issue</span></span>
* <span data-ttu-id="46680-140">登入 Azure Mobile Engagement UI 時發生問題。</span><span class="sxs-lookup"><span data-stu-id="46680-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="46680-141">使用 Azure Mobile Engagement API 時發生連線錯誤。</span><span class="sxs-lookup"><span data-stu-id="46680-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="46680-142">透過裝置 API 上傳應用程式資訊標記時發生問題。</span><span class="sxs-lookup"><span data-stu-id="46680-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="46680-143">從 Azure Mobile Engagement 下載記錄檔或匯出資料時發生問題。</span><span class="sxs-lookup"><span data-stu-id="46680-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="46680-144">Azure Mobile Engagement UI 中顯示的資訊不正確。</span><span class="sxs-lookup"><span data-stu-id="46680-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="46680-145">Azure Mobile Engagement 記錄檔中顯示的資訊不正確。</span><span class="sxs-lookup"><span data-stu-id="46680-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="46680-146">原因</span><span class="sxs-lookup"><span data-stu-id="46680-146">Causes</span></span>
* <span data-ttu-id="46680-147">確認您的使用者帳戶具備執行該作業所需的權限。</span><span class="sxs-lookup"><span data-stu-id="46680-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="46680-148">確認問題不是因為一部電腦或是因為您的區域網路而產生。</span><span class="sxs-lookup"><span data-stu-id="46680-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="46680-149">確認 Azure Mobile Engagement 服務沒有報告中斷。</span><span class="sxs-lookup"><span data-stu-id="46680-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="46680-150">確認您的應用程式資訊標記遵循以下所有規則：</span><span class="sxs-lookup"><span data-stu-id="46680-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="46680-151">僅使用 UTF8 字元集 (不支援 ANSI 字元集)。</span><span class="sxs-lookup"><span data-stu-id="46680-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="46680-152">使用逗號 "," 做為分隔字元 (您可以開啟服務要求，來要求將 .csv 分隔字元從逗號變更為另一個字元，例如分號 ";")。</span><span class="sxs-lookup"><span data-stu-id="46680-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="46680-153">使用全部小寫的布林值 "true" 和 "false"。</span><span class="sxs-lookup"><span data-stu-id="46680-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="46680-154">使用小於 35MB 檔案大小上限的檔案。</span><span class="sxs-lookup"><span data-stu-id="46680-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

