---
title: "aaaHow toosend 排程通知 |Microsoft 文件"
description: "本主題說明如何透過 Azure 通知中樞使用排定通知。"
services: notification-hubs
documentationcenter: .net
keywords: "推播通知,推播通知,排程推播通知"
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="9dec1-104">作法：傳送排定通知</span><span class="sxs-lookup"><span data-stu-id="9dec1-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="9dec1-105">概觀</span><span class="sxs-lookup"><span data-stu-id="9dec1-105">Overview</span></span>
<span data-ttu-id="9dec1-106">如果您有您想在某個點 hello 通知 toosend 未來，但是並沒有簡單的方式 toowake 註冊您的後端程式碼 toosend hello 通知的案例。</span><span class="sxs-lookup"><span data-stu-id="9dec1-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="9dec1-107">標準層通知中心支援的功能，可讓您設定在未來的 hello too7 天 tooschedule 通知。</span><span class="sxs-lookup"><span data-stu-id="9dec1-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="9dec1-108">當傳送通知，只要使用 hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx)類別 hello 通知中樞 SDK hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="9dec1-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="9dec1-109">此外，您也可以使用其 notificationId 取消先前已排程的通知︰</span><span class="sxs-lookup"><span data-stu-id="9dec1-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="9dec1-110">已排程的通知，您可以將傳送的 hello 數目沒有限制。</span><span class="sxs-lookup"><span data-stu-id="9dec1-110">There are no limits on hello number of scheduled notifications you can send.</span></span>

