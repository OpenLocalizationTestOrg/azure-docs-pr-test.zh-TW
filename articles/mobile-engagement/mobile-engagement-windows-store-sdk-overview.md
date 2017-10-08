---
title: "Mobile Engagement Windows 通用 SDK 整合 aaaAzure |Microsoft 文件"
description: "適用於 Azure Mobile Engagement 的 Windows 通用 SDK 整合"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>適用於 Azure Mobile Engagement 的 Windows 通用 SDK 整合
本文件說明所有 hello 整合和組態選項可供 hello Azure Mobile Engagement Windows 通用 SDK。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須先完成 [15 分鐘教學課程](mobile-engagement-windows-store-dotnet-get-started.md)。

## <a name="advanced-features"></a>進階功能
### <a name="reporting-features"></a>報告功能
您可以新增這些功能：

1. [進階報告選項](mobile-engagement-windows-store-advanced-reporting.md)
2. [進階組態選項](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>通知
[如何在 Windows 通用應用程式中的 toointegrate 觸達 （通知）](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>標記計畫實作：
[如何 toouse hello 進階 Mobile Engagement 標記 Windows 通用應用程式中的應用程式開發介面](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>版本資訊
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* 穩定性改進。

如先前的版本，請參閱 hello[完成版本資訊](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>升級程序
如果您已經有整合至您的應用程式較舊版本的參與，則必須升級 hello SDK 時，下列點 tooconsider hello。

如果您錯過數個版本的 hello SDK，您可能必須 toofollow 數個程序。 請參閱完整的 hello[升級程序](mobile-engagement-windows-store-upgrade-procedure.md)。 例如，如果您從 0.10.1 移轉 too0.11.0 您有遵循 hello toofirst"0.9.0 從 too0.10.1 」 程序然後 hello 」 從 0.10.1 too0.11.0 」 程序。

### <a name="from-330-too340"></a>從 3.3.0 too3.4.0
#### <a name="test-logs"></a>測試記錄檔
主控台記錄檔所產生的 hello SDK 現在可以啟用/停用/篩選。 toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`的 hello 值可從 hello tooone`EngagementTestLogLevel`列舉型別，例如：

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>資源
已改善 hello 觸達重疊。 它是 hello SDK 的 NuGet 封裝資源的一部分。

升級 toohello hello SDK 新版本，您可以選擇或不 hello 從現有的檔案是否要將 tookeep 覆疊資源的資料夾：

* 如果 hello 先前覆疊適合您，或者您要整合 hello`WebView`項目以手動方式，然後您可以決定 tookeep 您結束檔案，它仍可運作。
* tooupdate toohello 新建立的重疊取代 hello 整個`overlay`從您的資源，以從 hello SDK 套件中的 hello 新資料夾 (UWP 應用程式： hello 升級之後，您可以從 %USERPROFILE%取得新重疊資料夾 hello\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources)。

> [!WARNING]
> 使用 hello 新重疊，就會覆寫 hello 舊版本上所做的任何自訂。
> 
> 

### <a name="upgrade-from-older-versions"></a>從舊版升級
請參閱 [升級程序](mobile-engagement-windows-store-upgrade-procedure.md)

