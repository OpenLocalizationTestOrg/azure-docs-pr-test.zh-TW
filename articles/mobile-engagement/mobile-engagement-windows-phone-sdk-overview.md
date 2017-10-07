---
title: "aaaAzure Mobile Engagement Windows Phone Silverlight SDK 概觀 |Microsoft 文件"
description: "Hello Azure Mobile Engagement 適用於 Windows Phone Silverlight SDK 的概觀"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>適用於 Azure Mobile Engagement 的 Windows Phone Silverlight SDK 概觀
從這裡開始 tooget hello 詳細資料如何在 Windows Phone Silverlight 應用程式中的 Azure Mobile Engagement toointegrate。 如果您想要 toogive 它再試一次第一次，請確定您完成我們[15 分鐘教學課程](mobile-engagement-windows-phone-get-started.md)。

按一下 toosee hello [SDK 內容](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>整合程序
1. 從這裡開始：[如何在 Windows Phone Silverlight 應用程式中的 toointegrate Mobile Engagement](mobile-engagement-windows-phone-integrate-engagement.md)
2. 通知：[如何在 Windows Phone Silverlight 應用程式中的 toointegrate 觸達 （通知）](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. 標記計劃實作： [toouse hello 進階 Mobile Engagement 標記您的 Windows Phone Silverlight 應用程式中的應用程式開發介面的方式](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>版本資訊
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Hello 一部分*MicrosoftAzure.MobileEngagement* Nuget 封裝**v3.4.1**

* 穩定性改進。

針對較早版本，請參閱 hello[完成版本資訊](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>升級程序
如果您已經有整合至您的應用程式較舊版本的我們 SDK，您必須升級 hello SDK 時，下列點 tooconsider hello。

如果您錯過數個版本的 hello SDK 您可能需要指定 toofollow 數個程序。 請參閱完整的 hello[升級程序](mobile-engagement-windows-phone-upgrade-procedure.md)。 例如，如果您從 0.10.1 移轉 too0.11.0 您有遵循 hello toofirst"0.9.0 從 too0.10.1 」 程序然後 hello 」 從 0.10.1 too0.11.0 」 程序。

### <a name="from-200-too330"></a>從 2.0.0 too3.3.0
#### <a name="test-logs"></a>測試記錄檔
主控台記錄檔所產生的 hello SDK 現在可以啟用/停用/篩選。 toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`hello 值可從 hello 的 tooone`EngagementTestLogLevel`列舉型別，例如：

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>從舊版升級
請參閱 [升級程序](mobile-engagement-windows-phone-upgrade-procedure.md)

