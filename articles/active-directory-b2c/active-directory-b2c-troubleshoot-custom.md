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
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C︰收集記錄

本文提供從 Azure AD B2C 收集記錄的步驟，讓您可以診斷自訂原則的問題。

>[!NOTE]
>目前，hello 此處所述的詳細的活動記錄檔設計**只**tooaid 中開發的自訂原則。 請勿在生產環境中使用開發模式。  記錄檔收集 tooand 寄 hello 身分識別提供者，在開發期間的所有宣告。  如果在生產環境中使用，hello 開發人員負責 PII （私下識別資訊） 他們自己的 hello App Insights 記錄中收集。  這些詳細的記錄檔只會收集當 hello 原則放置在**開發模式**。


## <a name="use-application-insights"></a>使用 Application Insights

Azure AD B2C 傳送資料 tooApplication Insights 支援的功能。  Application Insights 提供方式 toodiagnose 例外狀況，並以視覺化方式檢視應用程式效能問題。

### <a name="setup-application-insights"></a>設定 Application Insights

1. 移 toohello [Azure 入口網站](https://portal.azure.com)。 請確定您是在 hello 租用戶與 Azure 訂用帳戶 （不您 Azure AD B2C 租用戶）。
1. 按一下**+ 新增**hello 左側瀏覽功能表中。
1. 搜尋並選取 [Application Insights]，然後按一下 [建立]。
1. 完成 hello 表單，然後按一下**建立**。 選取**一般**hello**應用程式類型**。
1. 一旦建立 hello 資源之後，開啟 hello Application Insights 資源。
1. 尋找**屬性**在 hello 左邊功能表上，並加以點選。
1. 複製 hello**檢測金鑰**並儲存起來供 hello 下一節。

### <a name="set-up-hello-custom-policy"></a>Hello 自訂原則設定

1. 開啟 hello RP 檔案 (例如，SignUpOrSignin.xml)。
1. 新增下列屬性 toohello hello`<TrustFrameworkPolicy>`項目：

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. 如果它已不存在，將子節點加入`<UserJourneyBehaviors>`toohello`<RelyingParty>`節點。 它必須位於後面 hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. 新增做為 hello 的子節點的後 hello`<UserJourneyBehaviors>`項目。 請確定 tooreplace`{Your Application Insights Key}`以 hello**檢測金鑰**您從 hello 前一節中的 Application Insights 取得。

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`良好告知 ApplicationInsights tooexpedite hello 遙測經由 hello 處理管線，開發項目，但在高的磁碟區的 受條件約束。
  * `ClientEnabled="true"`會傳送 hello ApplicationInsights 用戶端指令碼追蹤頁面檢視和用戶端錯誤 （不需要）。
  * `ServerEnabled="true"`傳送 hello 現有 UserJourneyRecorder JSON 做為自訂事件 tooApplication 深入資訊。
範例：

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

3. 上傳 hello 原則。

### <a name="see-hello-logs-in-application-insights"></a>請參閱 Application Insights 中的 hello 記錄

>[!NOTE]
> 短暫延遲之後 (五分鐘之內)，您在 Application Insights 中才會看到新的記錄。

1. 開啟您在 hello hello Application Insights 資源[Azure 入口網站](https://portal.azure.com)。
1. 在 hello**概觀**功能表，然後按一下**分析**。
1. 在 Application Insights 入口網站中開啟新的索引標籤。
1. 以下是您可以使用 toosee hello 記錄的查詢清單

| 查詢 | 說明 |
|---------------------|--------------------|
traces | 查看所有 Azure AD B2C 所產生的 hello 記錄檔 |
traces \| where timestamp > ago(1d) | 查看所有 hello 為產生的 Azure AD B2C hello 最後一天的記錄檔

hello 項目可能會很長。  深入解說的匯出 tooCSV。

您可以進一步了解 hello 分析工具[這裡](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)。

>[!NOTE]
>使用者之旅檢視器 toohelp 身分識別開發人員開發了 hello 社群。  此檢視器不受 Microsoft 支援，僅依原狀提供使用。  它會從您的 Application Insights 執行個體讀取，並提供 hello 使用者之旅事件的格式結構檢視。  您取得 hello 原始程式碼，並將它部署在您自己的解決方案。

>[!NOTE]
>目前，hello 此處所述的詳細的活動記錄檔設計**只**tooaid 中開發的自訂原則。 請勿在生產環境中使用開發模式。  記錄檔收集 tooand 寄 hello 身分識別提供者，在開發期間的所有宣告。  如果在生產環境中使用，hello 開發人員負責 PII （私下識別資訊） 他們自己的 hello App Insights 記錄中收集。  這些詳細的記錄檔只會收集當 hello 原則放置在**開發模式**。

[Github 用來存放不受支援之自訂原則範例和相關工具的存放庫](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>後續步驟

瀏覽在您了解 Application Insights toohelp hello 資料如何 hello 基礎 B2C 運作的 toodeliver 發生您自己的身分識別的身分識別體驗架構。
