---
title: "使用 Azure Log Analytics 監視 Surface Hub | Microsoft Docs"
description: "使用 Surface Hub 解決方案來追蹤您的 Surface Hub 健康狀態，並了解其使用狀況。"
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
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="0f706-103">使用 Log Analytics 監視 Surface Hub 來追蹤其健全狀況</span><span class="sxs-lookup"><span data-stu-id="0f706-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Surface Hub 符號](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="0f706-105">本文說明如何使用 Log Analytics 中的 Surface Hub 解決方案來監視 Microsoft Operations Management Suite (OMS) 搭配使用的 Microsoft Surface Hub 裝置。</span><span class="sxs-lookup"><span data-stu-id="0f706-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="0f706-106">Log Analytics 可幫助您追蹤您的 Surface Hub 健康狀態，以及了解其使用狀況。</span><span class="sxs-lookup"><span data-stu-id="0f706-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="0f706-107">每個 Surface Hub 都已安裝 Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="0f706-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="0f706-108">透過此代理程式，您可以將資料從您的 Surface Hub 傳送至 OMS。</span><span class="sxs-lookup"><span data-stu-id="0f706-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="0f706-109">系統會從您的 Surface Hub 讀取記錄檔，然後傳送給 OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="0f706-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="0f706-110">問題伺服器處於離線狀態、無法同步處理行事曆、裝置帳戶無法登入 Skype，諸如此類的問題會顯示在 OMS 的 Surface Hub 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="0f706-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="0f706-111">使用儀表板中的資料，您可以識別未執行或發生其他問題的裝置，然後可能會套用修正程式來處理偵測到的問題。</span><span class="sxs-lookup"><span data-stu-id="0f706-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="0f706-112">安裝和設定方案</span><span class="sxs-lookup"><span data-stu-id="0f706-112">Installing and configuring the solution</span></span>
<span data-ttu-id="0f706-113">請使用下列資訊來安裝和設定方案。</span><span class="sxs-lookup"><span data-stu-id="0f706-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="0f706-114">為了管理從 Microsoft Operations Management Suite (OMS) 管理您的 Surface Hub，您將需要下列各項︰</span><span class="sxs-lookup"><span data-stu-id="0f706-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="0f706-115">[OMS](http://www.microsoft.com/oms) 的有效訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f706-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="0f706-116">可支援您要監視之裝置數目的 [OMS 訂用帳戶](https://azure.microsoft.com/pricing/details/log-analytics/)層級。</span><span class="sxs-lookup"><span data-stu-id="0f706-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="0f706-117">OMS 的價格取決於已註冊多少裝置裝置以及要處理多少資料。</span><span class="sxs-lookup"><span data-stu-id="0f706-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="0f706-118">規劃使用 Surface Hub 時請將這一點列入考慮。</span><span class="sxs-lookup"><span data-stu-id="0f706-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="0f706-119">接下來，您要將 OMS 訂用帳戶新增至現有的 Microsoft Azure 訂用帳戶，或直接透過 OMS 入口網站建立新的工作區。</span><span class="sxs-lookup"><span data-stu-id="0f706-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="0f706-120">使用哪一種方法的詳細指示請參閱[開始使用 Log Analytics](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0f706-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="0f706-121">OMS 訂用帳戶設定完畢後，有兩種方式可以註冊您的 Surface Hub 裝置︰</span><span class="sxs-lookup"><span data-stu-id="0f706-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="0f706-122">自動透過 Intune 註冊</span><span class="sxs-lookup"><span data-stu-id="0f706-122">Automatically through Intune</span></span>
* <span data-ttu-id="0f706-123">在 Surface Hub 裝置上手動透過 [設定] 註冊</span><span class="sxs-lookup"><span data-stu-id="0f706-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="0f706-124">設定監視</span><span class="sxs-lookup"><span data-stu-id="0f706-124">Set up monitoring</span></span>
<span data-ttu-id="0f706-125">您可以使用 OMS 中的 Log Analytics 監視 Surface Hub 的健康狀態和活動。</span><span class="sxs-lookup"><span data-stu-id="0f706-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="0f706-126">您可以在 OMS 中使用 Intune 註冊 Surface Hub，或使用 Surface Hub 上的 [設定] 在本機註冊。</span><span class="sxs-lookup"><span data-stu-id="0f706-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="0f706-127">透過 Intune 將 Surface Hub 連接至 OMS</span><span class="sxs-lookup"><span data-stu-id="0f706-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="0f706-128">您會需要即將管理 Surface Hub 的 OMS 工作區的工作區識別碼和工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="0f706-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="0f706-129">您可以從 OMS 入口網站取得這些資訊。</span><span class="sxs-lookup"><span data-stu-id="0f706-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="0f706-130">Intune 是一項 Microsoft 產品，可讓您集中管理套用到一或多個裝置的 OMS 組態設定。</span><span class="sxs-lookup"><span data-stu-id="0f706-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="0f706-131">請依照下列步驟透過 Intune 設定您的裝置：</span><span class="sxs-lookup"><span data-stu-id="0f706-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="0f706-132">登入 Intune。</span><span class="sxs-lookup"><span data-stu-id="0f706-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="0f706-133">瀏覽至 [設定]  >  [連接的來源]。</span><span class="sxs-lookup"><span data-stu-id="0f706-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="0f706-134">以 Surface Hub 範本為基礎建立或編輯原則。</span><span class="sxs-lookup"><span data-stu-id="0f706-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="0f706-135">瀏覽至原則的 OMS (Azure Operational Insights) 區段，將 [工作區識別碼] 和 [工作區金鑰] 新增至原則。</span><span class="sxs-lookup"><span data-stu-id="0f706-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="0f706-136">儲存原則。</span><span class="sxs-lookup"><span data-stu-id="0f706-136">Save the policy.</span></span>
6. <span data-ttu-id="0f706-137">將原則與適當的裝置群組關聯。</span><span class="sxs-lookup"><span data-stu-id="0f706-137">Associate the policy with the appropriate group of devices.</span></span>

   ![Intune 原則](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="0f706-139">Intune 接著將 OMS 設定與目標群組中的裝置同步處理，將它們註冊到 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="0f706-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="0f706-140">使用設定應用程式將 Surface Hub 連接至 OMS</span><span class="sxs-lookup"><span data-stu-id="0f706-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="0f706-141">您會需要即將管理 Surface Hub 的 OMS 工作區的工作區識別碼和工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="0f706-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="0f706-142">您可以從 OMS 入口網站取得這些資訊。</span><span class="sxs-lookup"><span data-stu-id="0f706-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="0f706-143">如果您不使用 Intune 來管理您的環境，可以透過每個 Surface Hub 上的 [設定] 以手動方式註冊裝置︰</span><span class="sxs-lookup"><span data-stu-id="0f706-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="0f706-144">從您的 Surface Hub 開啟 [設定]。</span><span class="sxs-lookup"><span data-stu-id="0f706-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="0f706-145">出現提示時，輸入裝置的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="0f706-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="0f706-146">按一下 [這個裝置]，再按一下 [監視] 下的 [設定 OMS 設定]。</span><span class="sxs-lookup"><span data-stu-id="0f706-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="0f706-147">選取 [啟用監視]。</span><span class="sxs-lookup"><span data-stu-id="0f706-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="0f706-148">在 [OMS 設定] 對話方塊中，輸入**工作區識別碼**和**工作區金鑰**。</span><span class="sxs-lookup"><span data-stu-id="0f706-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="0f706-149">![設定](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="0f706-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="0f706-150">按一下 [確定] 完成設定。</span><span class="sxs-lookup"><span data-stu-id="0f706-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="0f706-151">會出現告訴您 OMS 設定已成功套用至裝置的確認訊息。</span><span class="sxs-lookup"><span data-stu-id="0f706-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="0f706-152">接下來會出現訊息指出代理程式已成功連接至 OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="0f706-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="0f706-153">裝置接著會開始將資料傳送至 OMS，您可以在其中檢視並處理它。</span><span class="sxs-lookup"><span data-stu-id="0f706-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="0f706-154">監視 Surface Hub</span><span class="sxs-lookup"><span data-stu-id="0f706-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="0f706-155">使用 OMS 監視 Surface Hub 和監視任何已註冊的裝置極為類似。</span><span class="sxs-lookup"><span data-stu-id="0f706-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="0f706-156">登入 OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0f706-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="0f706-157">瀏覽至 Surface Hub 解決方案組件的儀表板。</span><span class="sxs-lookup"><span data-stu-id="0f706-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="0f706-158">會顯示裝置的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="0f706-158">Your device's health is displayed.</span></span>

   ![Surface Hub 的儀表板](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="0f706-160">您可以根據現有或自訂的記錄檔搜尋來建立[警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="0f706-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="0f706-161">使用 OMS 從 existing or custom log searches 收集來的資料，您可以依您為裝置定義的條件搜尋問題和警示。</span><span class="sxs-lookup"><span data-stu-id="0f706-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f706-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f706-162">Next steps</span></span>
* <span data-ttu-id="0f706-163">使用 [Log Analytics 中的記錄檔搜尋](log-analytics-log-searches.md)來檢視詳細的 VMware 資料。</span><span class="sxs-lookup"><span data-stu-id="0f706-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="0f706-164">建立[警示](log-analytics-alerts.md)在 Surface Hub 發生問題時通知您。</span><span class="sxs-lookup"><span data-stu-id="0f706-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>
