---
title: "aaaAdd 推播通知 tooiOS 應用程式與 Azure 行動應用程式"
description: "了解如何 toouse Azure 行動應用程式 toosend 推播通知 tooyour iOS 應用程式。"
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a>加入推播通知 tooyour iOS 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>概觀
在本教學課程中，您將加入推播通知 toohello [iOS 快速啟動]專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。

如果您不要使用 hello 下載快速入門的伺服器專案，您將需要 hello 推播通知擴充套件。 請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)如需詳細資訊。

hello [iOS 模擬器不支援推播通知](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html)。 您需要實體 iOS 裝置和 [Apple Developer Program 成員資格](https://developer.apple.com/programs/ios/)。

## <a name="configure-hub"></a>設定通知中樞
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>註冊應用程式以取得推播通知
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a>設定 Azure toosend 推播通知
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a>更新後端 toosend 推播通知
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>加入推播通知 tooapp
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>測試推播通知
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a>更多資訊
* 範本可讓您彈性 toosend 跨平台的推送和當地語系化的推播通知。 [如何 tooUse iOS Azure 行動應用程式的用戶端程式庫](app-service-mobile-ios-how-to-use-client-library.md#templates)為您示範如何 tooregister 範本。

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS 快速啟動]: app-service-mobile-ios-get-started.md
