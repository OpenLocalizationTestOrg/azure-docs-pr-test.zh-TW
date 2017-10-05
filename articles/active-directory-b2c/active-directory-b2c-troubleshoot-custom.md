---
title: "用以針對自訂原則進行疑難排解的 Application Insights - Azure AD B2C | Microsoft Docs"
description: "如何設定 Application Insights 以追蹤自訂原則的執行"
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
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="dd947-103">Azure Active Directory B2C︰收集記錄</span><span class="sxs-lookup"><span data-stu-id="dd947-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="dd947-104">本文提供從 Azure AD B2C 收集記錄的步驟，讓您可以診斷自訂原則的問題。</span><span class="sxs-lookup"><span data-stu-id="dd947-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="dd947-105">目前，此處所述的詳細活動記錄**僅**針對協助開發自訂原則所設計。</span><span class="sxs-lookup"><span data-stu-id="dd947-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="dd947-106">請勿在生產環境中使用開發模式。</span><span class="sxs-lookup"><span data-stu-id="dd947-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="dd947-107">記錄會收集往返識別提供者在開發期間所傳送的所有宣告。</span><span class="sxs-lookup"><span data-stu-id="dd947-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="dd947-108">如果在生產環境中使用，開發人員會負責他們自己的 App Insights 記錄中收集的 PII (私人識別資訊)。</span><span class="sxs-lookup"><span data-stu-id="dd947-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="dd947-109">只有當原則位於**開發模式**時，才會收集這些詳細的記錄。</span><span class="sxs-lookup"><span data-stu-id="dd947-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="dd947-110">使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="dd947-110">Use Application Insights</span></span>

<span data-ttu-id="dd947-111">Azure AD B2C 支援將資料傳送至 Application Insights 的功能。</span><span class="sxs-lookup"><span data-stu-id="dd947-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="dd947-112">Application Insights 提供方法來診斷例外狀況和將應用程式效能問題視覺化。</span><span class="sxs-lookup"><span data-stu-id="dd947-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="dd947-113">設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="dd947-113">Setup Application Insights</span></span>

1. <span data-ttu-id="dd947-114">移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="dd947-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dd947-115">確定您所在的租用戶具有您的 Azure 訂用帳戶 (不是 Azure AD B2C 租用戶)。</span><span class="sxs-lookup"><span data-stu-id="dd947-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="dd947-116">在左側導覽功能表中按一下 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="dd947-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="dd947-117">搜尋並選取 [Application Insights]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="dd947-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="dd947-118">完成表單，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="dd947-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="dd947-119">在 [應用程式類型] 中，選取 [一般]。</span><span class="sxs-lookup"><span data-stu-id="dd947-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="dd947-120">建立資源後，開啟 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="dd947-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="dd947-121">在左邊功能表中尋找 [屬性]並按一下它。</span><span class="sxs-lookup"><span data-stu-id="dd947-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="dd947-122">複製 [檢測金鑰]，將它儲存起來供下一節使用。</span><span class="sxs-lookup"><span data-stu-id="dd947-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="dd947-123">設定自訂原則</span><span class="sxs-lookup"><span data-stu-id="dd947-123">Set up the custom policy</span></span>

1. <span data-ttu-id="dd947-124">開啟 RP 檔案 (例如 SignUpOrSignin.xml)。</span><span class="sxs-lookup"><span data-stu-id="dd947-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="dd947-125">將下列屬性新增至 `<TrustFrameworkPolicy>` 元素：</span><span class="sxs-lookup"><span data-stu-id="dd947-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="dd947-126">將子節點 `<UserJourneyBehaviors>` (如果尚未存在) 新增至 `<RelyingParty>` 節點。</span><span class="sxs-lookup"><span data-stu-id="dd947-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="dd947-127">它必須緊接在 `<DefaultUserJourney ReferenceId="YourPolicyName" />` 之後</span><span class="sxs-lookup"><span data-stu-id="dd947-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="dd947-128">新增下列節點作為 `<UserJourneyBehaviors>` 元素的子節點。</span><span class="sxs-lookup"><span data-stu-id="dd947-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="dd947-129">務必以您在上一節中從 Application Insights 取得的 [檢測金鑰] 取代 `{Your Application Insights Key}`。</span><span class="sxs-lookup"><span data-stu-id="dd947-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="dd947-130">`DeveloperMode="true"` 會指示 ApplicationInsights 透過處理管線加速遙測，雖然有助於開發，但數量龐大時會受限。</span><span class="sxs-lookup"><span data-stu-id="dd947-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="dd947-131">`ClientEnabled="true"` 會將用戶端指令碼傳送至 ApplicationInsights，以追蹤頁面檢視和用戶端錯誤 (不需要)。</span><span class="sxs-lookup"><span data-stu-id="dd947-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="dd947-132">`ServerEnabled="true"` 會將現有的 UserJourneyRecorder JSON 當作自訂事件傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="dd947-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="dd947-133">範例：</span><span class="sxs-lookup"><span data-stu-id="dd947-133">Sample:</span></span>

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

3. <span data-ttu-id="dd947-134">上傳原則。</span><span class="sxs-lookup"><span data-stu-id="dd947-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="dd947-135">查看 Application Insights 中的記錄</span><span class="sxs-lookup"><span data-stu-id="dd947-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="dd947-136">短暫延遲之後 (五分鐘之內)，您在 Application Insights 中才會看到新的記錄。</span><span class="sxs-lookup"><span data-stu-id="dd947-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="dd947-137">開啟您在 [Azure 入口網站](https://portal.azure.com)中建立的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="dd947-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="dd947-138">在 [概觀] 功能表中，按一下 [分析]。</span><span class="sxs-lookup"><span data-stu-id="dd947-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="dd947-139">在 Application Insights 入口網站中開啟新的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dd947-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="dd947-140">以下是您可以用來檢視記錄的查詢清單</span><span class="sxs-lookup"><span data-stu-id="dd947-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="dd947-141">查詢</span><span class="sxs-lookup"><span data-stu-id="dd947-141">Query</span></span> | <span data-ttu-id="dd947-142">說明</span><span class="sxs-lookup"><span data-stu-id="dd947-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="dd947-143">traces</span><span class="sxs-lookup"><span data-stu-id="dd947-143">traces</span></span> | <span data-ttu-id="dd947-144">查看 Azure AD B2C 產生的所有記錄</span><span class="sxs-lookup"><span data-stu-id="dd947-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="dd947-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="dd947-145">traces \\</span></span>| <span data-ttu-id="dd947-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="dd947-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="dd947-147">查看 Azure AD B2C 在最後一天產生的所有記錄</span><span class="sxs-lookup"><span data-stu-id="dd947-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="dd947-148">此項目可能很長。</span><span class="sxs-lookup"><span data-stu-id="dd947-148">The entries may be long.</span></span>  <span data-ttu-id="dd947-149">請將它匯出至 CSV 以仔細查看。</span><span class="sxs-lookup"><span data-stu-id="dd947-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="dd947-150">您可以在[這裡](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)深入了解分析工具。</span><span class="sxs-lookup"><span data-stu-id="dd947-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="dd947-151">該社群已開發了使用者旅程圖檢視器，可協助身分識別開發人員。</span><span class="sxs-lookup"><span data-stu-id="dd947-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="dd947-152">此檢視器不受 Microsoft 支援，僅依原狀提供使用。</span><span class="sxs-lookup"><span data-stu-id="dd947-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="dd947-153">它會讀取您的 Application Insights 執行個體，並提供結構良好的使用者旅程圖事件檢視。</span><span class="sxs-lookup"><span data-stu-id="dd947-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="dd947-154">請取得原始碼，並將它部署在您自己的解決方案中。</span><span class="sxs-lookup"><span data-stu-id="dd947-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="dd947-155">目前，此處所述的詳細活動記錄**僅**針對協助開發自訂原則所設計。</span><span class="sxs-lookup"><span data-stu-id="dd947-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="dd947-156">請勿在生產環境中使用開發模式。</span><span class="sxs-lookup"><span data-stu-id="dd947-156">Do not use development mode in production.</span></span>  <span data-ttu-id="dd947-157">記錄會收集往返識別提供者在開發期間所傳送的所有宣告。</span><span class="sxs-lookup"><span data-stu-id="dd947-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="dd947-158">如果在生產環境中使用，開發人員會負責他們自己的 App Insights 記錄中收集的 PII (私人識別資訊)。</span><span class="sxs-lookup"><span data-stu-id="dd947-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="dd947-159">只有當原則位於**開發模式**時，才會收集這些詳細的記錄。</span><span class="sxs-lookup"><span data-stu-id="dd947-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="dd947-160">Github 用來存放不受支援之自訂原則範例和相關工具的存放庫</span><span class="sxs-lookup"><span data-stu-id="dd947-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="dd947-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd947-161">Next Steps</span></span>

<span data-ttu-id="dd947-162">瀏覽 Application Insights 中的資料，可協助您了解身分識別體驗架構基礎 B2C 的運作方式，從而傳遞您自己的身分識別體驗。</span><span class="sxs-lookup"><span data-stu-id="dd947-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
