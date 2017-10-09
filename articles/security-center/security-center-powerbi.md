---
title: "從 Power BI 的 Azure 資訊安全中心資料 aaaGet insights |Microsoft 文件"
description: "hello Azure 安全性中心 Power BI 內容套件可輕鬆 toofind 安全性警示，請建議、 攻擊資源和趨勢、 已為您的報表建立資料集為基礎。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a><span data-ttu-id="727c1-103">使用 Power BI 從 Azure 資訊安全中心的資料取得見解</span><span class="sxs-lookup"><span data-stu-id="727c1-103">Get insights from Azure Security Center data with Power BI</span></span>
<span data-ttu-id="727c1-104">hello [Power BI 儀表板](http://aka.ms/azure-security-center-power-bi)Azure 資訊安全中心可讓您 toovisualize，分析及篩選建議和從任何地方，包括您的行動裝置的安全性警示。</span><span class="sxs-lookup"><span data-stu-id="727c1-104">hello [Power BI Dashboard](http://aka.ms/azure-security-center-power-bi) for Azure Security Center enables you toovisualize, analyze, and filter recommendations and security alerts from anywhere, including your mobile device.</span></span> <span data-ttu-id="727c1-105">使用 hello Power BI 儀表板 tooreveal 趨勢，而攻擊的模式-檢視安全性警示的資源或來源 IP 位址，並依資源或年齡 unaddressed 安全性風險。</span><span class="sxs-lookup"><span data-stu-id="727c1-105">Use hello Power BI dashboard tooreveal trends and attack patterns - view security alerts by resource or source IP address and unaddressed security risks by resource or age.</span></span>

<span data-ttu-id="727c1-106">您也可以用相關方式結合資訊安全中心建議、安全性警示和其他資料，例如使用 [Azure 稽核記錄檔](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/)和 [Azure SQL Database 稽核](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)中的資料。</span><span class="sxs-lookup"><span data-stu-id="727c1-106">You can also mash up Security Center recommendations and security alerts with other data in interesting ways, for example using data from [Azure Audit Logs](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) and [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/).</span></span> <span data-ttu-id="727c1-107">同時提供 Power BI 儀表板，而您也可以匯出此資料 tooExcel，hello 安全性狀態，提供雲端資源的簡單報表。</span><span class="sxs-lookup"><span data-stu-id="727c1-107">Both offer Power BI Dashboards, and you can also export this data tooExcel for easy reporting on hello security state of your cloud resources.</span></span>

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a><span data-ttu-id="727c1-108">使用 Azure 資訊安全中心儀表板 tooaccess Power BI</span><span class="sxs-lookup"><span data-stu-id="727c1-108">Using Azure Security Center dashboard tooaccess Power BI</span></span>
<span data-ttu-id="727c1-109">您也可以使用 hello Azure 資訊安全中心儀表板 tooaccess Power BI 報表。</span><span class="sxs-lookup"><span data-stu-id="727c1-109">You can also use hello Azure Security Center dashboard tooaccess Power BI reports.</span></span> <span data-ttu-id="727c1-110">請依照下列 hello 步驟 tooperform 這項工作：</span><span class="sxs-lookup"><span data-stu-id="727c1-110">Follow hello steps tooperform this task:</span></span>

1. <span data-ttu-id="727c1-111">在 hello **Azure 資訊安全中心**儀表板，按一下  **Power BI**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="727c1-111">In hello **Azure Security Center** dashboard, click **Power BI** button.</span></span>

    ![連接使用 Power BI tooAzure 資訊安全中心](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. <span data-ttu-id="727c1-113">hello **Power BI** hello 右邊會開啟刀鋒視窗，hello 遵循畫面所示：</span><span class="sxs-lookup"><span data-stu-id="727c1-113">hello **Power BI** blade opens on hello right side as shown in hello following screen:</span></span>

    ![連接使用 Power BI tooAzure 資訊安全中心](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. <span data-ttu-id="727c1-115">如果您要建立 hello hello 的 Power BI 儀表板第一次，您可以選擇在 hello hello 下列其中一種選項**Power BI 中的瀏覽**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="727c1-115">If you are creating hello Power BI dashboard for hello first time, you can choose one of hello following options in hello **Explore in Power BI** blade:</span></span>

   * <span data-ttu-id="727c1-116">**安全性 insights 儀表板**： 如果您想 toocreate 儀表板，其中包含安全性狀態、 執行緒和偵測，請選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="727c1-116">**Security insights dashboard**: choose this option if you want toocreate a dashboard that includes security status, threads, and detections.</span></span> <span data-ttu-id="727c1-117">對於負責分析各訂用帳戶的防護狀態及偵測到之警示的 DevOps 角色而言，這是較常見的選項。</span><span class="sxs-lookup"><span data-stu-id="727c1-117">This option is a more common for DevOps role that is responsible for analyzing their protection status and detected alerts across subscriptions.</span></span>
   * <span data-ttu-id="727c1-118">**原則管理儀表板**： 選擇此選項，如果您要 tooexplore 管理和強制執行原則。</span><span class="sxs-lookup"><span data-stu-id="727c1-118">**Policy management dashboard**: choose this option if you want tooexplore management and enforcement policy.</span></span>  <span data-ttu-id="727c1-119">對於偏重控管的中心 IT 人員而言，這是較常見的選項。</span><span class="sxs-lookup"><span data-stu-id="727c1-119">This option is a more common for Central IT who are more focused on governance.</span></span> <span data-ttu-id="727c1-120">他們可以使用此儀表板 toogain 可見性和 insights 安全性原則一致性跨組織。</span><span class="sxs-lookup"><span data-stu-id="727c1-120">They can use this dashboard toogain visibility and insights on security policy adherence across their organization.</span></span>
   * <span data-ttu-id="727c1-121">如果您已經有了 Power BI 儀表板，按一下**Go tooyour 目前 Power BI 儀表板**。</span><span class="sxs-lookup"><span data-stu-id="727c1-121">If you already have a Power BI dashboard, click **Go tooyour current Power BI dashboard**.</span></span>
4. <span data-ttu-id="727c1-122">在這個範例中，請點選 [安全性深入解析儀表板]  選項。</span><span class="sxs-lookup"><span data-stu-id="727c1-122">For this example, click **Security insights dashboard** option.</span></span> <span data-ttu-id="727c1-123">如果這是 hello 第一次，您要建立 Power BI 儀表板，針對您的資訊安全中心提示 tooinstall hello 內容套件。</span><span class="sxs-lookup"><span data-stu-id="727c1-123">If this is hello first time, you are creating a Power BI dashboard for Security Center you are prompted tooinstall hello content pack.</span></span> <span data-ttu-id="727c1-124">按一下**取得**按鈕在 hello **Power bi 內容套件**視窗 hello 遵循畫面所示：</span><span class="sxs-lookup"><span data-stu-id="727c1-124">Click **Get** button in hello **Content packs for Power BI** window as shown in hello following screen:</span></span>

    ![Azure 資訊安全中心安全性深入解析儀表板](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. <span data-ttu-id="727c1-126">hello**連接 tooAzure 安全性中心的安全性深入解析**視窗會出現。</span><span class="sxs-lookup"><span data-stu-id="727c1-126">hello **Connect tooAzure Security Center Security Insights** window appear.</span></span> <span data-ttu-id="727c1-127">請確定 hello**驗證**方法**oAuth2**如下所示，按一下 [**登入**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="727c1-127">Make sure hello **Authentication** method is **oAuth2** as shown below and click **Sign in** button.</span></span>

    ![驗證](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. <span data-ttu-id="727c1-129">您可能會要求 tooauthenticate 再次與您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="727c1-129">You may be asked tooauthenticate again with your Azure credentials.</span></span> <span data-ttu-id="727c1-130">驗證之後，將會建立您的儀表板。</span><span class="sxs-lookup"><span data-stu-id="727c1-130">After authenticating your dashboard will be created.</span></span> <span data-ttu-id="727c1-131">一旦建立 hello 儀表板之後您會看到與 hello 類似結構報告 hello 遵循畫面所示：</span><span class="sxs-lookup"><span data-stu-id="727c1-131">Once hello dashboard is created you see a report with hello similar structure as shown in hello following screen:</span></span>

    ![Power BI 儀表板](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> <span data-ttu-id="727c1-133">Hello 報表重新整理是每日的排程的 tootake 位置。</span><span class="sxs-lookup"><span data-stu-id="727c1-133">A refresh of hello report is scheduled tootake place on a daily basis.</span></span> <span data-ttu-id="727c1-134">如果您遇到此重新整理失敗時，讀取[可能會發生重新整理問題 hello Azure 安全性中心 Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/)，如需有關如何 tootroubleshoot。</span><span class="sxs-lookup"><span data-stu-id="727c1-134">In case you experience a failure on this refresh, read [Potential Refresh Issues with hello Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), for more information on how tootroubleshoot.</span></span>
>
>

<span data-ttu-id="727c1-135">您可以查看 hello 編號安全性警示和建議，以及 hello Vm、 Azure SQL database 和 Azure 資訊安全中心受監視的網路資源數目。</span><span class="sxs-lookup"><span data-stu-id="727c1-135">Here you can see hello number of security alerts and recommendations, as well as hello number of VMs, Azure SQL databases, and network resources being monitored by Azure Security Center.</span></span>

<span data-ttu-id="727c1-136">連結 tooAzure 資訊安全中心重新導向 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="727c1-136">A link tooAzure Security Center redirects you toohello Azure portal.</span></span> <span data-ttu-id="727c1-137">hello 圖表讓安全性建議和警示，包括簡單 toovisualize 資訊：</span><span class="sxs-lookup"><span data-stu-id="727c1-137">hello charts make it easy toovisualize information about security recommendations and alerts, including:</span></span>

* <span data-ttu-id="727c1-138">資源安全性狀態</span><span class="sxs-lookup"><span data-stu-id="727c1-138">Resource Security State</span></span>
* <span data-ttu-id="727c1-139">擱置建議</span><span class="sxs-lookup"><span data-stu-id="727c1-139">Pending Recommendations</span></span>
* <span data-ttu-id="727c1-140">VM 建議</span><span class="sxs-lookup"><span data-stu-id="727c1-140">VM Recommendations</span></span>
* <span data-ttu-id="727c1-141">不同時間的警示</span><span class="sxs-lookup"><span data-stu-id="727c1-141">Alerts over Time</span></span>
* <span data-ttu-id="727c1-142">受到攻擊的資源</span><span class="sxs-lookup"><span data-stu-id="727c1-142">Attacked Resources</span></span>
* <span data-ttu-id="727c1-143">受到攻擊的 IP</span><span class="sxs-lookup"><span data-stu-id="727c1-143">Attacked IPs</span></span>

<span data-ttu-id="727c1-144">每個圖表背後都有額外的見解。</span><span class="sxs-lookup"><span data-stu-id="727c1-144">Behind each chart, there are additional insights.</span></span> <span data-ttu-id="727c1-145">選取磚 toosee 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="727c1-145">Select a tile toosee more information.</span></span> <span data-ttu-id="727c1-146">例如，hello**資源安全性狀態**磚會顯示您的其他詳細資料的相關暫止的建議資源 hello 遵循畫面所示：</span><span class="sxs-lookup"><span data-stu-id="727c1-146">For example, hello **Resource Security State** tile shows you additional details about pending recommendations by resources as shown in hello following screen:</span></span>

![建議](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

<span data-ttu-id="727c1-148">如果您按一下此圖表的任何一行，hello 其他人將 toogray 出與您的重點只在您選取的 hello。</span><span class="sxs-lookup"><span data-stu-id="727c1-148">If you click on any line of this graph, hello others are going toogray out and you focus only on hello one you selected.</span></span> <span data-ttu-id="727c1-149">tooreturn toohello 儀表板中，按一下  **Azure 資訊安全中心**下 hello**儀表板**hello 左窗格上的此頁面的選項。</span><span class="sxs-lookup"><span data-stu-id="727c1-149">tooreturn toohello dashboard, click **Azure Security Center** under hello **Dashboards** option on hello left pane of this page.</span></span>

> [!NOTE]
> <span data-ttu-id="727c1-150">如果您想要 toocustomize 報表藉由新增其他欄位，或變更現有的視覺效果，您可以編輯 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="727c1-150">If you’d like toocustomize your reports by adding additional fields or changing existing visuals, you can edit hello report.</span></span> <span data-ttu-id="727c1-151">如需詳細資訊，請閱讀 [在 Power BI 中與編輯檢視的報告互動](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) 。</span><span class="sxs-lookup"><span data-stu-id="727c1-151">Read [Interact with a report in Editing View in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) for more information.</span></span>
>
>

<span data-ttu-id="727c1-152">hello**經過一段時間，攻擊資源警示**和**攻擊者的 Ip**當您按一下每個磚會有 hello 相似的輸出。</span><span class="sxs-lookup"><span data-stu-id="727c1-152">hello **Alerts over Time, Attacked Resources** and **Attacker IPs** tiles will have hello similar output when you click on each one of it.</span></span> <span data-ttu-id="727c1-153">這是因為 hello 報表彙總所有的三個變數的相關資訊，並呼叫它**遭受攻擊的資源**hello 遵循畫面所示：</span><span class="sxs-lookup"><span data-stu-id="727c1-153">This happens because hello report aggregates information regarding all those three variables and calls it **Resources under Attack** as shown in hello following screen:</span></span>

![遭受攻擊的資源](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

<span data-ttu-id="727c1-155">此時您也可以儲存此報表的複本、 列印或 hello 網站上發佈使用 hello 中可用的 hello 選項**檔案**功能表。</span><span class="sxs-lookup"><span data-stu-id="727c1-155">At this point you can also save a copy of this report, print it or publish it on hello web by using hello options available in hello **File** menu.</span></span>

![[檔案] 功能表](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a><span data-ttu-id="727c1-157">使用 Power BI 服務探索 Azure 資訊安全中心的資料</span><span class="sxs-lookup"><span data-stu-id="727c1-157">Exploring your Azure Security Center data with Power BI services</span></span>
<span data-ttu-id="727c1-158">連接 toohello [Power BI 內容套件服務](https://msit.powerbi.com/groups/me/getdata/services)Power BI 中，然後執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="727c1-158">Connect toohello [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) in Power BI and execute hello following steps:</span></span>

1. <span data-ttu-id="727c1-159">在 hello**適用於 Power BI 內容套件**視窗將會看到兩個選項，如下所示。</span><span class="sxs-lookup"><span data-stu-id="727c1-159">In hello **Content Pack for Power BI** window you will see two options as shown below.</span></span>

    ![Power BI 內容套件](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > <span data-ttu-id="727c1-161">如果已經執行本文章的 hello 第一個部分，您會看到一個選項，這是 Azure 安全性中心的 原則管理。</span><span class="sxs-lookup"><span data-stu-id="727c1-161">If already executed hello first part of this article you will see only one option, which is Azure Security Center Policy Management.</span></span>
   >
   >
2. <span data-ttu-id="727c1-162">為了 hello 此範例中，按一下 **取得**在 hello **Azure 安全性中心的 原則管理**磚。</span><span class="sxs-lookup"><span data-stu-id="727c1-162">For hello purpose of this example, click **Get** in hello **Azure Security Center Policy Management** tile.</span></span>
3. <span data-ttu-id="727c1-163">在 hello**連接 tooAzure 安全性 Center 原則管理**視窗中，請確定 tooselect **oAuth2**下**驗證方法**卸除下如下所示，然後按一下**登入** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="727c1-163">In hello **Connect tooAzure Security Center Policy Management** window, make sure tooselect **oAuth2** under **Authentication Method** drop down as shown below and click **Sign in** button.</span></span>

    ![原則管理視窗](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. <span data-ttu-id="727c1-165">您將會重新導向的 tooan 驗證頁面上，您應該在其中輸入 hello 認證使用 tooconnect tooAzure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="727c1-165">You will be redirected tooan authentication page where you should type hello credentials that you are using tooconnect tooAzure Security Center.</span></span> <span data-ttu-id="727c1-166">Hello 驗證程序完成之後，Power BI 會開始匯入資料 toobuild 您的報表。</span><span class="sxs-lookup"><span data-stu-id="727c1-166">After hello authentication process is complete, Power BI will start importing data toobuild your reports.</span></span> <span data-ttu-id="727c1-167">在這段期間可能會看到下列訊息上的瀏覽器的 hello 右上角的 hello:</span><span class="sxs-lookup"><span data-stu-id="727c1-167">During this time you may see hello following message on hello right corner of your browser:</span></span>

    ![連接使用 Power BI tooAzure 資訊安全中心](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > <span data-ttu-id="727c1-169">hello 儀表板建立時的 hello 第一次它可以比平常長，主要用於情況下，您需要多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="727c1-169">when hello dashboard is being created for hello first time it can take longer than usual, mainly for scenarios where you have multiple subscriptions.</span></span>
   >
   >
5. <span data-ttu-id="727c1-170">Azure 安全性中心 Power BI 儀表板在 hello 程序完成時，便會載入 hello**原則管理**報告類似 toohello 一個如下所示：</span><span class="sxs-lookup"><span data-stu-id="727c1-170">Once hello process is finished, your Azure Security Center Power BI dashboard will load with hello **Policy Management** report similar toohello one shown below:</span></span>

    ![原則管理儀表板](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a><span data-ttu-id="727c1-172">另請參閱</span><span class="sxs-lookup"><span data-stu-id="727c1-172">See also</span></span>
<span data-ttu-id="727c1-173">在本文件中，您學到如何 toouse Azure 資訊安全中心中的 Power BI。</span><span class="sxs-lookup"><span data-stu-id="727c1-173">In this document, you learned how toouse Power BI in Azure Security Center.</span></span> <span data-ttu-id="727c1-174">toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="727c1-174">toolearn more about Azure Security Center, see hello following:</span></span>

* <span data-ttu-id="727c1-175">[Azure 資訊安全中心計劃與作業指南](security-center-planning-and-operations-guide.md)— 了解如何 tooplan Azure 資訊安全中心採用。</span><span class="sxs-lookup"><span data-stu-id="727c1-175">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how tooplan Azure Security Center adoption.</span></span>
* <span data-ttu-id="727c1-176">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)— 了解如何 tooconfigure Azure 資訊安全中心中的安全性設定</span><span class="sxs-lookup"><span data-stu-id="727c1-176">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security settings in Azure Security Center</span></span>
* <span data-ttu-id="727c1-177">[Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示</span><span class="sxs-lookup"><span data-stu-id="727c1-177">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts</span></span>
* <span data-ttu-id="727c1-178">[Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集</span><span class="sxs-lookup"><span data-stu-id="727c1-178">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service</span></span>
* <span data-ttu-id="727c1-179">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="727c1-179">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span></span>
