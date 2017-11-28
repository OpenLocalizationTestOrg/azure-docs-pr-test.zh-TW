---
title: "aaaAzure Mobile Engagement 疑難排解指南-服務"
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
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="1e84e-103">服務問題的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="1e84e-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="1e84e-104">hello 以下是可能的問題，您可能會遇到與 Azure Mobile Engagement 的執行方式。</span><span class="sxs-lookup"><span data-stu-id="1e84e-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="1e84e-105">服務中斷</span><span class="sxs-lookup"><span data-stu-id="1e84e-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="1e84e-106">問題</span><span class="sxs-lookup"><span data-stu-id="1e84e-106">Issue</span></span>
* <span data-ttu-id="1e84e-107">出現 toobe Azure Mobile Engagement 服務中斷所造成的問題。</span><span class="sxs-lookup"><span data-stu-id="1e84e-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="1e84e-108">原因</span><span class="sxs-lookup"><span data-stu-id="1e84e-108">Causes</span></span>
* <span data-ttu-id="1e84e-109">出現 toobe Azure Mobile Engagement 服務中斷所造成的問題可能被因不同的幾個問題：</span><span class="sxs-lookup"><span data-stu-id="1e84e-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="1e84e-110">原本出現的 Azure Mobile Engagement 全面 tooall 隔離的問題</span><span class="sxs-lookup"><span data-stu-id="1e84e-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="1e84e-111">伺服器關閉所造成的已知問題 (不一定會顯示在伺服器狀態中)：</span><span class="sxs-lookup"><span data-stu-id="1e84e-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="1e84e-112">排程延遲、 目標錯誤、 徽章更新問題、 統計資料停止收集，推入停止運作，應用程式開發介面的停止作用、 新的應用程式或使用者無法建立，DNS 錯誤及逾時錯誤裝置 hello UI、 API 或應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1e84e-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="1e84e-113">雲端相依性中斷 [Azure 服務狀態](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="1e84e-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="1e84e-114">推送通知服務 (PNS) 相依性中斷</span><span class="sxs-lookup"><span data-stu-id="1e84e-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="1e84e-115">應用程式商店中斷</span><span class="sxs-lookup"><span data-stu-id="1e84e-115">App Store Outages</span></span>

1) <span data-ttu-id="1e84e-116">tootest toosee 全面 hello 問題時，您可以測試相同函式從不同的 hello</span><span class="sxs-lookup"><span data-stu-id="1e84e-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="1e84e-117">Azure Mobile Engagement 整合式應用程式</span><span class="sxs-lookup"><span data-stu-id="1e84e-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="1e84e-118">測試裝置</span><span class="sxs-lookup"><span data-stu-id="1e84e-118">Test device</span></span>
* <span data-ttu-id="1e84e-119">測試裝置作業系統版本</span><span class="sxs-lookup"><span data-stu-id="1e84e-119">Test device OS version</span></span>
* <span data-ttu-id="1e84e-120">活動</span><span class="sxs-lookup"><span data-stu-id="1e84e-120">Campaign</span></span>
* <span data-ttu-id="1e84e-121">系統管理員使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="1e84e-121">Administrator user account</span></span>
* <span data-ttu-id="1e84e-122">瀏覽器 (IE、Firefox、Chrome 等)</span><span class="sxs-lookup"><span data-stu-id="1e84e-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="1e84e-123">電腦</span><span class="sxs-lookup"><span data-stu-id="1e84e-123">Computer</span></span>

2) <span data-ttu-id="1e84e-124">如果 hello 問題只會影響 hello UI 或 hello API，tootest:</span><span class="sxs-lookup"><span data-stu-id="1e84e-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="1e84e-125">測試相同的函式從這兩個 hello Azure Mobile Engagement UI 和 hello Azure Mobile Engagement 應用程式開發介面的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e84e-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="1e84e-126">tootest hello 問題是否與您的行動電話網路：</span><span class="sxs-lookup"><span data-stu-id="1e84e-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="1e84e-127">測試連接 toohello 網際網路透過 WIFI 和時透過行動電話 3g 網路連線時。</span><span class="sxs-lookup"><span data-stu-id="1e84e-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="1e84e-128">確認您的防火牆不會封鎖任何 hello Azure Mobile Engagement IP 位址或連接埠。</span><span class="sxs-lookup"><span data-stu-id="1e84e-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="1e84e-129">tootest hello 問題是否與您的裝置：</span><span class="sxs-lookup"><span data-stu-id="1e84e-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="1e84e-130">測試您的裝置可以 tooconnect tooAzure Mobile Engagement 與另一個 Azure Mobile Engagement 整合式應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e84e-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="1e84e-131">您可以從手機 hello Azure Mobile Engagement UI 中，可以看到產生的事件、 工作和當機的測試。</span><span class="sxs-lookup"><span data-stu-id="1e84e-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="1e84e-132">測試您可以傳送推播通知從 hello Azure Mobile Engagement UI tooyour 裝置根據其裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="1e84e-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="1e84e-133">tootest hello 問題是否與您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="1e84e-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="1e84e-134">從模擬器 (而不是實體裝置)，安裝並測試您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="1e84e-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="1e84e-135">tootest hello 問題是否與裝置，需要 SDK 升級 tooresolve OS 升級 tooend 使用者：</span><span class="sxs-lookup"><span data-stu-id="1e84e-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="1e84e-136">測試不同的裝置，具有不同版本的 hello OS 上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e84e-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="1e84e-137">確認您使用的 hello hello SDK 最新版本。</span><span class="sxs-lookup"><span data-stu-id="1e84e-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="1e84e-138">連線和資訊不正確的問題</span><span class="sxs-lookup"><span data-stu-id="1e84e-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="1e84e-139">問題</span><span class="sxs-lookup"><span data-stu-id="1e84e-139">Issue</span></span>
* <span data-ttu-id="1e84e-140">登入問題 hello Azure Mobile Engagement UI。</span><span class="sxs-lookup"><span data-stu-id="1e84e-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="1e84e-141">Hello Azure Mobile Engagement 應用程式開發介面的連接錯誤。</span><span class="sxs-lookup"><span data-stu-id="1e84e-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="1e84e-142">透過 hello 裝置 API 上傳應用程式資訊標記的問題。</span><span class="sxs-lookup"><span data-stu-id="1e84e-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="1e84e-143">從 Azure Mobile Engagement 下載記錄檔或匯出資料時發生問題。</span><span class="sxs-lookup"><span data-stu-id="1e84e-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="1e84e-144">Hello Azure Mobile Engagement UI 中顯示的資訊不正確。</span><span class="sxs-lookup"><span data-stu-id="1e84e-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="1e84e-145">Azure Mobile Engagement 記錄檔中顯示的資訊不正確。</span><span class="sxs-lookup"><span data-stu-id="1e84e-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="1e84e-146">原因</span><span class="sxs-lookup"><span data-stu-id="1e84e-146">Causes</span></span>
* <span data-ttu-id="1e84e-147">請確認您的使用者帳戶有足夠的權限 tooperform hello 工作。</span><span class="sxs-lookup"><span data-stu-id="1e84e-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="1e84e-148">請確認該 hello 問題不是隔離的 tooone 電腦或區域網路。</span><span class="sxs-lookup"><span data-stu-id="1e84e-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="1e84e-149">請確認該 hello Azure Mobile Engagement 服務有任何回報的中斷。</span><span class="sxs-lookup"><span data-stu-id="1e84e-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="1e84e-150">確認您的應用程式資訊標記遵循以下所有規則：</span><span class="sxs-lookup"><span data-stu-id="1e84e-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="1e84e-151">使用僅 hello UTF8 字元集 （不支援 hello ANSI 字元集）。</span><span class="sxs-lookup"><span data-stu-id="1e84e-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="1e84e-152">使用逗號"，"hello 分隔符號字元 (您可以開啟 服務要求 toorequest toochange hello.csv 分隔符號字元逗號"，"tooanother 字元，例如分號";")。</span><span class="sxs-lookup"><span data-stu-id="1e84e-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="1e84e-153">使用全部小寫的布林值 "true" 和 "false"。</span><span class="sxs-lookup"><span data-stu-id="1e84e-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="1e84e-154">使用小於 hello 檔案大小上限為 35 MB 的檔案。</span><span class="sxs-lookup"><span data-stu-id="1e84e-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

