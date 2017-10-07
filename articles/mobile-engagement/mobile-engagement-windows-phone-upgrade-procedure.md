---
title: "aaaWindows Phone Silverlight SDK 升級程序"
description: "Azure Mobile Engagement 的 Windows Phone Silverlight SDK 升級程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Windows Phone Silverlight SDK 升級程序
如果您已經有整合至您的應用程式較舊版本的我們 SDK，您必須升級 hello SDK 時，下列點 tooconsider hello。

如果您錯過數個版本的 hello SDK 您可能需要指定 toofollow 數個程序。 例如，如果您從 0.10.1 移轉 too0.11.0 您有遵循 hello toofirst"0.9.0 從 too0.10.1 」 程序然後 hello 」 從 0.10.1 too0.11.0 」 程序。

## <a name="from-200-too330"></a>從 2.0.0 too3.3.0
### <a name="test-logs"></a>測試記錄檔
主控台記錄檔所產生的 hello SDK 現在可以啟用/停用/篩選。 toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`hello 值可從 hello 的 tooone`EngagementTestLogLevel`列舉型別，例如：

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>從 1.1.1 too2.0.0
hello 下列程式碼說明如何 toomigrate hello Capptain 服務從 SDK 整合提供 Capptain SAS 到由 Azure Mobile Engagement 應用程式。 

> [!IMPORTANT]
> Capptain 和 Mobile Engagement 不是 hello 相同的服務和 hello 下列程序只會反白顯示 toomigrate hello 用戶端應用程式的方式。 移轉 hello SDK hello 應用程式中的不會移轉您的資料從 hello Capptain 伺服器 toohello Mobile Engagement 伺服器
> 
> 

如果您從舊版移轉，請先參閱 hello Capptain 網站 toomigrate too1.1.1 則套用 hello 遵循程序

### <a name="nuget-package"></a>Nuget 封裝
以 **MicrosoftAzure.MobileEngagement** Nuget 套件取代 **Capptain.WindowsPhone**。

### <a name="applying-mobile-engagement"></a>套用 Mobile Engagement
hello SDK 會使用 hello 詞彙`Engagement`。 您需要 tooupdate 專案 toomatch 這項變更。

您需要 toouninstall 目前 Capptain nuget 套件。 請考慮您在 [Capptain Resources] 資料夾中所有的變更將會移除。 如果您要 tookeep 那些檔案，請建立一份。

之後，請在您的專案上安裝 hello 新 Microsoft Azure Engagement nuget 封裝。 您可以直接在 [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement)上找到。 這個動作會取代所有的資源檔案由參與，並將新 Engagement DLL tooyour hello 專案參考。

您的 tooclean 您的專案參考刪除 Capptain DLL 的參考。 如果不這樣做，Capptain hello 版本會發生衝突，會發生錯誤。

如果您已自訂 Capptain 資源，複製舊的檔案內容，並將它們貼在 hello 新 Engagement 檔案中。 請注意，xaml 和 cs 檔案有 toobe 更新。

這些步驟都完成之後，您只需要由 hello 新 Engagement 參考 tooreplace 舊 Capptain 參考。

1. 所有 Capptain 命名空間都有 toobe 更新。
   
    移轉前：
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    移轉後：
   
        using Microsoft.Azure.Engagement;
2. 所有包含 "Capptain" 的 Capptain 類別應該要包含 "Engagement"。
   
    移轉前：
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    移轉後：
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. 對於 xaml 檔案，Capptain 命名空間和屬性也會變更。
   
    移轉前：
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    移轉後：
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Hello 的其他資源，例如 Capptain 圖片，請注意，它們也已重新命名的 toouse 「 參與 」。

### <a name="application-id--sdk-key"></a>應用程式 ID / SDK 金鑰
Engagement 使用連接字串。 您沒有 toospecify 應用程式識別碼和與 Mobile Engagement SDK 金鑰，您只需要 toospecify 連接字串。 您可以在您的 EngagementConfiguration 檔案中設定它。

hello Engagement 組態可以設定您`Resources\EngagementConfiguration.xml`專案檔。

編輯此檔案 toospecify:

* 應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。

如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

您的應用程式的 hello 連接字串會顯示在 [hello Azure 傳統入口網站。

### <a name="items-name-change"></a>項目名稱變更
所有名為 capptain 的項目已命名為 engagement。 同樣地針對*Capptain*太*Engagement*。

常用 Capptain 項目的範例：

* CapptainConfiguration 現在名為 EngagementConfiguration
* CapptainAgent 現在名為 EngagementAgent
* CapptainReach 現在名為 EngagementReach
* CapptainHttpConfig 現在名為 EngagementHttpConfig
* GetCapptainPageName 現在名為 GetEngagementPageName

請注意，重新命名也會影響覆寫方法。

