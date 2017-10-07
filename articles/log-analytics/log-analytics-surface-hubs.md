---
title: "Azure 記錄分析 Surface Hub aaaMonitor |Microsoft 文件"
description: "使用 hello Surface Hub 方案 tootrack hello 的健全狀況 Surface Hub 和了解它們的使用方式。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a><span data-ttu-id="0f230-103">記錄分析 tootrack 與它們的健全狀況監視 Surface Hub</span><span class="sxs-lookup"><span data-stu-id="0f230-103">Monitor Surface Hubs with Log Analytics tootrack their health</span></span>

![Surface Hub 符號](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="0f230-105">本文說明如何使用 hello Surface Hub 方案以 hello Microsoft Operations Management Suite (OMS) 的記錄分析 toomonitor Microsoft Surface Hub 裝置中。</span><span class="sxs-lookup"><span data-stu-id="0f230-105">This article describes how you can use hello Surface Hub solution in Log Analytics toomonitor Microsoft Surface Hub devices with hello Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="0f230-106">記錄分析協助您，以及了解如何在使用追蹤 Surface Hub hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="0f230-106">Log Analytics helps you track hello health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="0f230-107">每個 Surface Hub 已安裝 Microsoft Monitoring Agent 的 hello。</span><span class="sxs-lookup"><span data-stu-id="0f230-107">Each Surface Hub has hello Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="0f230-108">它透過 hello 代理程式，您可以從 Surface Hub tooOMS 傳送資料。</span><span class="sxs-lookup"><span data-stu-id="0f230-108">Its through hello agent that you can send data from your Surface Hub tooOMS.</span></span> <span data-ttu-id="0f230-109">記錄檔從您到 Surface Hub 和都是讀取，則會傳送 toohello OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="0f230-109">Log files are read from your Surface Hubs and are then are sent toohello OMS service.</span></span> <span data-ttu-id="0f230-110">問題 like 伺服器處於離線狀態，hello 行事曆不同步，或無法至 Skype toolog hello 裝置帳戶是否會顯示在 OMS 中 hello Surface Hub 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="0f230-110">Issues like servers being offline, hello calendar not syncing, or if hello device account is unable toolog into Skype are shown in OMS in hello Surface Hub dashboard.</span></span> <span data-ttu-id="0f230-111">使用 hello 資料 hello 儀表板中，您可以識別未執行，或發生其他問題，並可能套用 hello 偵測到問題的修正程式的裝置。</span><span class="sxs-lookup"><span data-stu-id="0f230-111">By using hello data in hello dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for hello detected issues.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="0f230-112">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="0f230-112">Installing and configuring hello solution</span></span>
<span data-ttu-id="0f230-113">使用下列資訊 tooinstall hello 並設定 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="0f230-113">Use hello following information tooinstall and configure hello solution.</span></span> <span data-ttu-id="0f230-114">在順序 toomanage 您到 Surface Hub hello Microsoft Operations Management Suite (OMS)，從您將需要下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f230-114">In order toomanage your Surface Hubs from hello Microsoft Operations Management Suite (OMS), you'll need hello following:</span></span>

* <span data-ttu-id="0f230-115">有效的訂用帳戶太[OMS](http://www.microsoft.com/oms)。</span><span class="sxs-lookup"><span data-stu-id="0f230-115">A valid subscription too[OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="0f230-116">[OMS 訂用帳戶](https://azure.microsoft.com/pricing/details/log-analytics/)層級將支援 hello 數目要 toomonitor 的裝置。</span><span class="sxs-lookup"><span data-stu-id="0f230-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support hello number of devices you want toomonitor.</span></span> <span data-ttu-id="0f230-117">OMS 的價格取決於已註冊多少裝置裝置以及要處理多少資料。</span><span class="sxs-lookup"><span data-stu-id="0f230-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="0f230-118">您會想 tootake 這考量 Surface Hub 首度發行計劃時。</span><span class="sxs-lookup"><span data-stu-id="0f230-118">You'll want tootake this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="0f230-119">接下來，您會加入 OMS 訂用帳戶 tooyour 現有 Microsoft Azure 訂用帳戶，或建立新的工作區，以直接透過 hello OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0f230-119">Next, you will either add an OMS subscription tooyour existing Microsoft Azure subscription or create a new workspace directly through hello OMS portal.</span></span> <span data-ttu-id="0f230-120">使用哪一種方法的詳細指示請參閱[開始使用 Log Analytics](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0f230-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="0f230-121">一旦設定 hello OMS 訂用帳戶之後，有兩種方式 tooenroll Surface Hub 裝置：</span><span class="sxs-lookup"><span data-stu-id="0f230-121">Once hello OMS subscription is set up, there are two ways tooenroll your Surface Hub devices:</span></span>

* <span data-ttu-id="0f230-122">自動透過 Intune 註冊</span><span class="sxs-lookup"><span data-stu-id="0f230-122">Automatically through Intune</span></span>
* <span data-ttu-id="0f230-123">在 Surface Hub 裝置上手動透過 [設定] 註冊</span><span class="sxs-lookup"><span data-stu-id="0f230-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="0f230-124">設定監視</span><span class="sxs-lookup"><span data-stu-id="0f230-124">Set up monitoring</span></span>
<span data-ttu-id="0f230-125">您可以監視 hello 健全狀況和您在 OMS 中使用記錄分析的 Surface Hub 的活動。</span><span class="sxs-lookup"><span data-stu-id="0f230-125">You can monitor hello health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="0f230-126">您可以註冊 hello Surface Hub 在 OMS 中，使用 Intune，或在本機使用**設定**上 hello Surface Hub。</span><span class="sxs-lookup"><span data-stu-id="0f230-126">You can enroll hello Surface Hub in OMS by using Intune, or locally by using **Settings** on hello Surface Hub.</span></span>

## <a name="connect-surface-hubs-toooms-through-intune"></a><span data-ttu-id="0f230-127">透過 Intune 連線到 Surface Hub tooOMS</span><span class="sxs-lookup"><span data-stu-id="0f230-127">Connect Surface Hubs tooOMS through Intune</span></span>
<span data-ttu-id="0f230-128">您將需要 hello 工作區識別碼和管理 Surface Hub 的 hello OMS 工作區的工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="0f230-128">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="0f230-129">您可以取得 hello OMS 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="0f230-129">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="0f230-130">Intune 是一項 Microsoft 產品，可讓您 toocentrally 管理 hello OMS 組態設定會套用的 tooone 或多個裝置。</span><span class="sxs-lookup"><span data-stu-id="0f230-130">Intune is a Microsoft product that allows you toocentrally manage hello OMS configuration settings that are applied tooone or more of your devices.</span></span> <span data-ttu-id="0f230-131">請遵循這些步驟 tooconfigure 您透過 Intune 的裝置：</span><span class="sxs-lookup"><span data-stu-id="0f230-131">Follow these steps tooconfigure your devices through Intune:</span></span>

1. <span data-ttu-id="0f230-132">登入 tooIntune。</span><span class="sxs-lookup"><span data-stu-id="0f230-132">Sign in tooIntune.</span></span>
2. <span data-ttu-id="0f230-133">瀏覽過**設定** > **連線來源**。</span><span class="sxs-lookup"><span data-stu-id="0f230-133">Navigate too**Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="0f230-134">建立或編輯 hello Surface Hub 範本為基礎的原則。</span><span class="sxs-lookup"><span data-stu-id="0f230-134">Create or edit a policy based on hello Surface Hub template.</span></span>
4. <span data-ttu-id="0f230-135">瀏覽 toohello OMS (Azure Operational Insights) 區段的 hello 原則，並新增 hello*工作區識別碼*和*工作區金鑰*toohello 原則。</span><span class="sxs-lookup"><span data-stu-id="0f230-135">Navigate toohello OMS (Azure Operational Insights) section of hello policy, and add hello *Workspace ID* and *Workspace Key* toohello policy.</span></span>
5. <span data-ttu-id="0f230-136">儲存 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="0f230-136">Save hello policy.</span></span>
6. <span data-ttu-id="0f230-137">Hello 原則關聯的裝置 hello 適當的群組。</span><span class="sxs-lookup"><span data-stu-id="0f230-137">Associate hello policy with hello appropriate group of devices.</span></span>

   ![Intune 原則](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="0f230-139">然後，Intune 會同步 hello OMS 設定處理與 hello hello 目標群組中，您的 OMS 工作區中註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="0f230-139">Intune then syncs hello OMS settings with hello devices in hello target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a><span data-ttu-id="0f230-140">連接到 Surface Hub tooOMS 使用 hello 設定應用程式</span><span class="sxs-lookup"><span data-stu-id="0f230-140">Connect Surface Hubs tooOMS using hello Settings app</span></span>
<span data-ttu-id="0f230-141">您將需要 hello 工作區識別碼和管理 Surface Hub 的 hello OMS 工作區的工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="0f230-141">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="0f230-142">您可以取得 hello OMS 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="0f230-142">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="0f230-143">如果您不使用 Intune toomanage 您的環境，您可以註冊裝置以手動方式透過**設定**上每個 Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="0f230-143">If you don't use Intune toomanage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="0f230-144">從您的 Surface Hub 開啟 [設定]。</span><span class="sxs-lookup"><span data-stu-id="0f230-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="0f230-145">輸入當系統提示您 hello 裝置系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="0f230-145">Enter hello device admin credentials when prompted.</span></span>
3. <span data-ttu-id="0f230-146">按一下**此裝置**，和在 hello**監視**，按一下 **設定 OMS 設定**。</span><span class="sxs-lookup"><span data-stu-id="0f230-146">Click **This device**, and hello under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="0f230-147">選取 [啟用監視]。</span><span class="sxs-lookup"><span data-stu-id="0f230-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="0f230-148">在 hello OMS 設定對話方塊中，輸入 hello**工作區識別碼**和型別 hello**工作區金鑰**。</span><span class="sxs-lookup"><span data-stu-id="0f230-148">In hello OMS settings dialog, type hello **Workspace ID** and type hello **Workspace Key**.</span></span>  
   <span data-ttu-id="0f230-149">![設定](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="0f230-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="0f230-150">按一下**確定**toocomplete hello 組態。</span><span class="sxs-lookup"><span data-stu-id="0f230-150">Click **OK** toocomplete hello configuration.</span></span>

<span data-ttu-id="0f230-151">出現確認訊息會告訴您 hello OMS 組態已成功套用 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="0f230-151">A confirmation appears telling you whether or not hello OMS configuration was successfully applied toohello device.</span></span> <span data-ttu-id="0f230-152">如果資料，會出現訊息，指出該 hello 代理程式已成功連接 toohello OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="0f230-152">If it was, a message appears stating that hello agent successfully connected toohello OMS service.</span></span> <span data-ttu-id="0f230-153">hello 裝置接著會開始傳送資料 tooOMS，您可以在其中檢視和處理它。</span><span class="sxs-lookup"><span data-stu-id="0f230-153">hello device then starts sending data tooOMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="0f230-154">監視 Surface Hub</span><span class="sxs-lookup"><span data-stu-id="0f230-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="0f230-155">使用 OMS 監視 Surface Hub 和監視任何已註冊的裝置極為類似。</span><span class="sxs-lookup"><span data-stu-id="0f230-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="0f230-156">登入 toohello OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0f230-156">Sign in toohello OMS portal.</span></span>
2. <span data-ttu-id="0f230-157">瀏覽 toohello Surface Hub 方案套件儀表板。</span><span class="sxs-lookup"><span data-stu-id="0f230-157">Navigate toohello Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="0f230-158">會顯示裝置的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="0f230-158">Your device's health is displayed.</span></span>

   ![Surface Hub 的儀表板](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="0f230-160">您可以根據現有或自訂的記錄檔搜尋來建立[警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="0f230-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="0f230-161">使用 OMS 會收集從 Surface Hub hello 資料 hello，您可以搜尋問題和 hello 條件，您定義您的裝置上的警示。</span><span class="sxs-lookup"><span data-stu-id="0f230-161">Using hello data hello OMS collects from your Surface Hubs, you can search for issues and alert on hello conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f230-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f230-162">Next steps</span></span>
* <span data-ttu-id="0f230-163">使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 Surface Hub 資料。</span><span class="sxs-lookup"><span data-stu-id="0f230-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Surface Hub data.</span></span>
* <span data-ttu-id="0f230-164">建立[警示](log-analytics-alerts.md)toonotify 您 Surface Hub 發生問題時。</span><span class="sxs-lookup"><span data-stu-id="0f230-164">Create [alerts](log-analytics-alerts.md) toonotify you when issues occur with your Surface Hubs.</span></span>
