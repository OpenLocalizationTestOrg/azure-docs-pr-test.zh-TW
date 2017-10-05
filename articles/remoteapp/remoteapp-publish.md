---
title: "在 Azure RemoteApp 中發佈 App | Microsoft Docs"
description: "了解如何在 Azure RemoteApp 中發佈應用程式和資源。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="858cf-103">如何在 RemoteApp 中發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="858cf-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="858cf-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="858cf-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="858cf-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="858cf-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="858cf-106">建立 RemoteApp 收藏之後，您必須發佈想供使用者使用的應用程式或資源。</span><span class="sxs-lookup"><span data-stu-id="858cf-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="858cf-107">隨您的訂閱提供的範本映像預設只會發佈幾個應用程式，若要共用其他應用程式，您必須發佈它們。</span><span class="sxs-lookup"><span data-stu-id="858cf-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="858cf-108">您需要更新應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="858cf-108">Do you need to update an app?</span></span> <span data-ttu-id="858cf-109">您將需要先 [更新映像](remoteapp-update.md) 。</span><span class="sxs-lookup"><span data-stu-id="858cf-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="858cf-110">在入口網站的 [發佈] 索引標籤中，按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="858cf-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="858cf-111">您可以從您範本映像的 [ **開始** ] 功能表新增應用程式，或是在範本映像提供安裝程式的路徑。</span><span class="sxs-lookup"><span data-stu-id="858cf-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="858cf-112">如果您選擇從 [開始]  功能表新增，請從清單中選擇要發佈的 App。</span><span class="sxs-lookup"><span data-stu-id="858cf-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="858cf-113">如果您選擇提供應用程式的路徑，請輸入應用程式的名稱和應用程式路徑。</span><span class="sxs-lookup"><span data-stu-id="858cf-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="858cf-114">請在路徑中使用變數，例如 "%systemdrive%" 而非 "c:\"。</span><span class="sxs-lookup"><span data-stu-id="858cf-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="858cf-115">如果您想要從 [開始] 功能表新增您的應用程式，就必須先「在您的範本映像上將該應用程式新增至 [開始] 功能表」。</span><span class="sxs-lookup"><span data-stu-id="858cf-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="858cf-116">否則，RemoteApp 只會看到在 [開始] 功能表上的項目，而您會覺得很困惑。</span><span class="sxs-lookup"><span data-stu-id="858cf-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="858cf-117">若要確定您的 App 位於 [開始] 功能表，請將捷徑檔案 (**.lnk**) 置於 %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="858cf-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="858cf-118">如果您忘記在建立範本時將應用程式新增到 [開始] 功能表，請選擇新增路徑到應用程式。</span><span class="sxs-lookup"><span data-stu-id="858cf-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="858cf-119">(或者重新建立您的範本映像，但是這會比較費工。)</span><span class="sxs-lookup"><span data-stu-id="858cf-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

