---
title: "使用 Azure 行動應用程式將推播通知新增至 iOS 應用程式"
description: "了解如何使用 Azure 行動應用程式將推播通知傳送至 iOS 應用程式。"
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
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="00239-103">將推播通知新增至您的 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="00239-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="00239-104">概觀</span><span class="sxs-lookup"><span data-stu-id="00239-104">Overview</span></span>
<span data-ttu-id="00239-105">在本教學課程中，您會將推播通知新增至 [iOS 快速入門]專案，以便在每次插入一筆記錄時傳送推播通知至裝置。</span><span class="sxs-lookup"><span data-stu-id="00239-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="00239-106">如果您不要使用下載的快速入門伺服器專案，將需要推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="00239-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="00239-107">如需詳細資訊，請參閱[使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="00239-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="00239-108">[iOS 模擬器不支援推播通知](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html)。</span><span class="sxs-lookup"><span data-stu-id="00239-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="00239-109">您需要實體 iOS 裝置和 [Apple Developer Program 成員資格](https://developer.apple.com/programs/ios/)。</span><span class="sxs-lookup"><span data-stu-id="00239-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="00239-110"><a name="configure-hub"></a>設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="00239-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="00239-111"><a id="register"></a>註冊應用程式以取得推播通知</span><span class="sxs-lookup"><span data-stu-id="00239-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="00239-112">設定 Azure 來傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="00239-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="00239-113"><a id="update-server"></a>更新後端程式碼以傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="00239-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="00239-114"><a id="add-push"></a>將推播通知新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="00239-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="00239-115"><a id="test"></a>測試推播通知</span><span class="sxs-lookup"><span data-stu-id="00239-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="00239-116"><a id="more"></a>更多資訊</span><span class="sxs-lookup"><span data-stu-id="00239-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="00239-117">範本可讓您彈性地傳送跨平台推播和當地語系化推播。</span><span class="sxs-lookup"><span data-stu-id="00239-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="00239-118">[如何使用適用於 Azure 行動應用程式的 iOS 用戶端程式庫](app-service-mobile-ios-how-to-use-client-library.md#templates) 一文，說明如何註冊範本。</span><span class="sxs-lookup"><span data-stu-id="00239-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="00239-119">[iOS 快速入門]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="00239-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>
