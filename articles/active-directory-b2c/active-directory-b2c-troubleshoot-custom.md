---
title: "應用程式 Insights tootroubleshoot 自訂原則的 Azure AD B2C |Microsoft 文件"
description: "如何 toosetup Application Insights tootrace hello 執行的自訂原則"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="068a1-103">Azure Active Directory B2C︰收集記錄</span><span class="sxs-lookup"><span data-stu-id="068a1-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="068a1-104">本文提供從 Azure AD B2C 收集記錄的步驟，讓您可以診斷自訂原則的問題。</span><span class="sxs-lookup"><span data-stu-id="068a1-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="068a1-105">目前，hello 此處所述的詳細的活動記錄檔設計**只**tooaid 中開發的自訂原則。</span><span class="sxs-lookup"><span data-stu-id="068a1-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="068a1-106">請勿在生產環境中使用開發模式。</span><span class="sxs-lookup"><span data-stu-id="068a1-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="068a1-107">記錄檔收集 tooand 寄 hello 身分識別提供者，在開發期間的所有宣告。</span><span class="sxs-lookup"><span data-stu-id="068a1-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="068a1-108">如果在生產環境中使用，hello 開發人員負責 PII （私下識別資訊） 他們自己的 hello App Insights 記錄中收集。</span><span class="sxs-lookup"><span data-stu-id="068a1-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="068a1-109">這些詳細的記錄檔只會收集當 hello 原則放置在**開發模式**。</span><span class="sxs-lookup"><span data-stu-id="068a1-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="068a1-110">使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="068a1-110">Use Application Insights</span></span>

<span data-ttu-id="068a1-111">Azure AD B2C 傳送資料 tooApplication Insights 支援的功能。</span><span class="sxs-lookup"><span data-stu-id="068a1-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="068a1-112">Application Insights 提供方式 toodiagnose 例外狀況，並以視覺化方式檢視應用程式效能問題。</span><span class="sxs-lookup"><span data-stu-id="068a1-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="068a1-113">設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="068a1-113">Setup Application Insights</span></span>

1. <span data-ttu-id="068a1-114">移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="068a1-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="068a1-115">請確定您是在 hello 租用戶與 Azure 訂用帳戶 （不您 Azure AD B2C 租用戶）。</span><span class="sxs-lookup"><span data-stu-id="068a1-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="068a1-116">按一下**+ 新增**hello 左側瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="068a1-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="068a1-117">搜尋並選取 [Application Insights]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="068a1-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="068a1-118">完成 hello 表單，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="068a1-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="068a1-119">選取**一般**hello**應用程式類型**。</span><span class="sxs-lookup"><span data-stu-id="068a1-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="068a1-120">一旦建立 hello 資源之後，開啟 hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="068a1-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="068a1-121">尋找**屬性**在 hello 左邊功能表上，並加以點選。</span><span class="sxs-lookup"><span data-stu-id="068a1-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="068a1-122">複製 hello**檢測金鑰**並儲存起來供 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="068a1-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="068a1-123">Hello 自訂原則設定</span><span class="sxs-lookup"><span data-stu-id="068a1-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="068a1-124">開啟 hello RP 檔案 (例如，SignUpOrSignin.xml)。</span><span class="sxs-lookup"><span data-stu-id="068a1-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="068a1-125">新增下列屬性 toohello hello`<TrustFrameworkPolicy>`項目：</span><span class="sxs-lookup"><span data-stu-id="068a1-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="068a1-126">如果它已不存在，將子節點加入`<UserJourneyBehaviors>`toohello`<RelyingParty>`節點。</span><span class="sxs-lookup"><span data-stu-id="068a1-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="068a1-127">它必須位於後面 hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="068a1-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="068a1-128">新增做為 hello 的子節點的後 hello`<UserJourneyBehaviors>`項目。</span><span class="sxs-lookup"><span data-stu-id="068a1-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="068a1-129">請確定 tooreplace`{Your Application Insights Key}`以 hello**檢測金鑰**您從 hello 前一節中的 Application Insights 取得。</span><span class="sxs-lookup"><span data-stu-id="068a1-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="068a1-130">`DeveloperMode="true"`良好告知 ApplicationInsights tooexpedite hello 遙測經由 hello 處理管線，開發項目，但在高的磁碟區的 受條件約束。</span><span class="sxs-lookup"><span data-stu-id="068a1-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="068a1-131">`ClientEnabled="true"`會傳送 hello ApplicationInsights 用戶端指令碼追蹤頁面檢視和用戶端錯誤 （不需要）。</span><span class="sxs-lookup"><span data-stu-id="068a1-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="068a1-132">`ServerEnabled="true"`傳送 hello 現有 UserJourneyRecorder JSON 做為自訂事件 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="068a1-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="068a1-133">範例：</span><span class="sxs-lookup"><span data-stu-id="068a1-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="068a1-134">上傳 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="068a1-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="068a1-135">請參閱 Application Insights 中的 hello 記錄</span><span class="sxs-lookup"><span data-stu-id="068a1-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="068a1-136">短暫延遲之後 (五分鐘之內)，您在 Application Insights 中才會看到新的記錄。</span><span class="sxs-lookup"><span data-stu-id="068a1-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="068a1-137">開啟您在 hello hello Application Insights 資源[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="068a1-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="068a1-138">在 hello**概觀**功能表，然後按一下**分析**。</span><span class="sxs-lookup"><span data-stu-id="068a1-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="068a1-139">在 Application Insights 入口網站中開啟新的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="068a1-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="068a1-140">以下是您可以使用 toosee hello 記錄的查詢清單</span><span class="sxs-lookup"><span data-stu-id="068a1-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="068a1-141">查詢</span><span class="sxs-lookup"><span data-stu-id="068a1-141">Query</span></span> | <span data-ttu-id="068a1-142">說明</span><span class="sxs-lookup"><span data-stu-id="068a1-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="068a1-143">traces</span><span class="sxs-lookup"><span data-stu-id="068a1-143">traces</span></span> | <span data-ttu-id="068a1-144">查看所有 Azure AD B2C 所產生的 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="068a1-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="068a1-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="068a1-145">traces \\</span></span>| <span data-ttu-id="068a1-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="068a1-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="068a1-147">查看所有 hello 為產生的 Azure AD B2C hello 最後一天的記錄檔</span><span class="sxs-lookup"><span data-stu-id="068a1-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="068a1-148">hello 項目可能會很長。</span><span class="sxs-lookup"><span data-stu-id="068a1-148">hello entries may be long.</span></span>  <span data-ttu-id="068a1-149">深入解說的匯出 tooCSV。</span><span class="sxs-lookup"><span data-stu-id="068a1-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="068a1-150">您可以進一步了解 hello 分析工具[這裡](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)。</span><span class="sxs-lookup"><span data-stu-id="068a1-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="068a1-151">使用者之旅檢視器 toohelp 身分識別開發人員開發了 hello 社群。</span><span class="sxs-lookup"><span data-stu-id="068a1-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="068a1-152">此檢視器不受 Microsoft 支援，僅依原狀提供使用。</span><span class="sxs-lookup"><span data-stu-id="068a1-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="068a1-153">它會從您的 Application Insights 執行個體讀取，並提供 hello 使用者之旅事件的格式結構檢視。</span><span class="sxs-lookup"><span data-stu-id="068a1-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="068a1-154">您取得 hello 原始程式碼，並將它部署在您自己的解決方案。</span><span class="sxs-lookup"><span data-stu-id="068a1-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="068a1-155">目前，hello 此處所述的詳細的活動記錄檔設計**只**tooaid 中開發的自訂原則。</span><span class="sxs-lookup"><span data-stu-id="068a1-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="068a1-156">請勿在生產環境中使用開發模式。</span><span class="sxs-lookup"><span data-stu-id="068a1-156">Do not use development mode in production.</span></span>  <span data-ttu-id="068a1-157">記錄檔收集 tooand 寄 hello 身分識別提供者，在開發期間的所有宣告。</span><span class="sxs-lookup"><span data-stu-id="068a1-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="068a1-158">如果在生產環境中使用，hello 開發人員負責 PII （私下識別資訊） 他們自己的 hello App Insights 記錄中收集。</span><span class="sxs-lookup"><span data-stu-id="068a1-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="068a1-159">這些詳細的記錄檔只會收集當 hello 原則放置在**開發模式**。</span><span class="sxs-lookup"><span data-stu-id="068a1-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="068a1-160">Github 用來存放不受支援之自訂原則範例和相關工具的存放庫</span><span class="sxs-lookup"><span data-stu-id="068a1-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="068a1-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="068a1-161">Next Steps</span></span>

<span data-ttu-id="068a1-162">瀏覽在您了解 Application Insights toohelp hello 資料如何 hello 基礎 B2C 運作的 toodeliver 發生您自己的身分識別的身分識別體驗架構。</span><span class="sxs-lookup"><span data-stu-id="068a1-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
