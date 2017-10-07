---
title: "aaaPublish Azure RemoteApp 中的應用程式 |Microsoft 文件"
description: "深入了解如何 toopublish 應用程式與 Azure RemoteApp 中的資源。"
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
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="75806-103">如何 toopublish RemoteApp 應用程式</span><span class="sxs-lookup"><span data-stu-id="75806-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="75806-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="75806-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="75806-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="75806-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="75806-106">建立您的 RemoteApp 集合之後，您需要 toopublish hello 應用程式或您為您的使用者想 toomake 可用資源。</span><span class="sxs-lookup"><span data-stu-id="75806-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="75806-107">hello 與您的訂用帳戶所提供的範本映像只能有少數應用程式發佈的預設值-tooshare hello 其他應用程式，您就需要 toopublish 它們。</span><span class="sxs-lookup"><span data-stu-id="75806-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="75806-108">您需要 tooupdate 應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="75806-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="75806-109">您必須太[更新 hello 影像](remoteapp-update.md)第一次。</span><span class="sxs-lookup"><span data-stu-id="75806-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="75806-110">在 hello**發行**hello 入口網站中索引標籤上，按一下 **發行**。</span><span class="sxs-lookup"><span data-stu-id="75806-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="75806-111">您可以從您的範本映像加入應用程式**啟動**功能表或提供 hello 路徑 toowhere hello 應用程式安裝在 hello 範本映像上。</span><span class="sxs-lookup"><span data-stu-id="75806-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="75806-112">如果您選擇 tooadd hello**啟動**功能表上，從 hello 清單中選擇 hello 應用程式 toopublish。</span><span class="sxs-lookup"><span data-stu-id="75806-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="75806-113">如果您選擇 tooprovide hello 路徑 toohello 應用程式，輸入 hello 和 hello 路徑 toohello app 的名稱。</span><span class="sxs-lookup"><span data-stu-id="75806-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="75806-114">使用 hello path-例如，"%systemdrive%"中的變數，而不是"c:\"。</span><span class="sxs-lookup"><span data-stu-id="75806-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="75806-115">如果您想 tooadd hello 應用程式**啟動**功能表上，您需要 toohave*加入該應用程式 toohello**啟動**範本映像上的功能表。*</span><span class="sxs-lookup"><span data-stu-id="75806-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="75806-116">否則，RemoteApp 只會看到什麼*是*hello 上**啟動**功能表上，而且您會產生混淆。</span><span class="sxs-lookup"><span data-stu-id="75806-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="75806-117">toomake 確定您的應用程式處於 hello**啟動**功能表上，將快顯檔案- **.lnk** -hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="75806-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="75806-118">如果您忘記 tooadd hello 應用程式 toohello**啟動**功能表建立 hello 範本時選擇 tooadd hello 路徑 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75806-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="75806-119">(或者重新建立您的範本映像，但是這會比較費工。)</span><span class="sxs-lookup"><span data-stu-id="75806-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

