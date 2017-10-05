---
title: "使用 Office 與 Azure RemoteApp 搭配 | Microsoft Docs"
description: "了解 Office 和 Azure RemoteApp 如何共同運作"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a776d877c764109f15c1025db2be3114eea2130a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-office-with-azure-remoteapp"></a><span data-ttu-id="dca49-103">使用 Office 與 Azure RemoteApp 搭配</span><span class="sxs-lookup"><span data-stu-id="dca49-103">Using Office with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dca49-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="dca49-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="dca49-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="dca49-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="dca49-106">在 Azure RemoteApp 中裝載 Office 應用程式有兩個選項：Office 365 ProPlus 或 Office 2013 Professional Plus 試用版。</span><span class="sxs-lookup"><span data-stu-id="dca49-106">You have two choices for hosting Office applications in Azure RemoteApp: Office 365 ProPlus or Office 2013 Professional Plus Trial.</span></span>

<span data-ttu-id="dca49-107">**您知道我們即將取代這篇文章的更佳新文章嗎？請查看[如何搭配 Azure RemoteApp 使用 Office 365 訂閱](remoteapp-officesubscription.md)。該文涵蓋了使用 Office 365 + Azure RemoteApp 所需的所有資訊。**</span><span class="sxs-lookup"><span data-stu-id="dca49-107">**Hey, did you know we have a new, better article that will soon replace this? Check out [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md). It covers all the info you need for using Office 365 + Azure RemoteApp.**</span></span>

## <a name="office-365-proplus"></a><span data-ttu-id="dca49-108">Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="dca49-108">Office 365 ProPlus</span></span>
<span data-ttu-id="dca49-109">您可以使用 Office 365 ProPlus 範本映像建立 RemoteApp 收藏。</span><span class="sxs-lookup"><span data-stu-id="dca49-109">You can create a RemoteApp collection using the Office 365 ProPlus template image.</span></span> <span data-ttu-id="dca49-110">此選項可讓您將 Office 365 服務延伸至 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="dca49-110">This option allows you to extend your Office 365 service to RemoteApp.</span></span> <span data-ttu-id="dca49-111">您必須有現有的訂閱方案，而且您的使用者必須有 Office 365 ProPlus 服務的授權 (獨立授權或透過 Office 365 服務方案授權)。</span><span class="sxs-lookup"><span data-stu-id="dca49-111">You must have an existing subscription plan and your users must be licensed for the Office 365 ProPlus service, either standalone or through the Office 365 service plans.</span></span>

<span data-ttu-id="dca49-112">RemoteApp 支援 Office 365 共用電腦啟用。</span><span class="sxs-lookup"><span data-stu-id="dca49-112">RemoteApp supports Office 365 Shared Computer Activation.</span></span> <span data-ttu-id="dca49-113">當您啟用「共用電腦啟用」時，以及使用 [Office 部署工具](http://www.microsoft.com/download/details.aspx?id=36778) 進行安裝時，Office 365 ProPlus 會進行安裝但不會啟用。</span><span class="sxs-lookup"><span data-stu-id="dca49-113">When you enable Shared Computer Activation, and use the [Office Deployment tool](http://www.microsoft.com/download/details.aspx?id=36778) for installation, Office 365 ProPlus installs without being activated.</span></span> <span data-ttu-id="dca49-114">當使用者登入包含 Office 365 的收藏時，Office 會檢查是否已為 Office 365 ProPlus 佈建使用者。</span><span class="sxs-lookup"><span data-stu-id="dca49-114">When a user signs into a collection that contains Office 365, Office checks to see if the user has been provisioned for Office 365 ProPlus.</span></span> <span data-ttu-id="dca49-115">如果是，則 Office 會暫時啟用 Office 365 ProPlus - 這個啟用只會持續到該使用者登出服務為止。</span><span class="sxs-lookup"><span data-stu-id="dca49-115">If so, Office temporarily activates Office 365 ProPlus - this activation persists until that users signs out of the service.</span></span>

<span data-ttu-id="dca49-116">若要使用 Office 365 共用電腦啟用，您必須依照[這些指示](https://technet.microsoft.com/library/dn782858.aspx)建立[自訂範本](remoteapp-create-custom-image.md)並在該處安裝 Office 365 ProPlus。</span><span class="sxs-lookup"><span data-stu-id="dca49-116">To use Office 365 Shared Computer Activation, you need to create a [custom template](remoteapp-create-custom-image.md) and install Office 365 ProPlus there, following [these directions](https://technet.microsoft.com/library/dn782858.aspx).</span></span>

<span data-ttu-id="dca49-117">您可以在 [Office 365 管理入口網站](https://portal.office365.com/)中管理使用者的 Office 365 授權。</span><span class="sxs-lookup"><span data-stu-id="dca49-117">You can manage your users’ Office 365 licenses at the [Office 365 Admin Portal](https://portal.office365.com/).</span></span> <span data-ttu-id="dca49-118">閱讀更多關於 [Office 365 服務方案](http://technet.microsoft.com/library/office-365-plan-options.aspx)的資訊。</span><span class="sxs-lookup"><span data-stu-id="dca49-118">Read more information about [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span>  

## <a name="office-2013-professional-plus-trial"></a><span data-ttu-id="dca49-119">Office 2013 Professional Plus 試用版</span><span class="sxs-lookup"><span data-stu-id="dca49-119">Office 2013 Professional Plus Trial</span></span>
<span data-ttu-id="dca49-120">在 RemoteApp 30 天的試用版期間，您可以使用 Office 2013 Professional Plus (試用版) 範本映像來建立 RemoteApp 收藏。</span><span class="sxs-lookup"><span data-stu-id="dca49-120">During a 30-day trial of RemoteApp, you can use the Office 2013 Professional Plus (trial) template image to create a RemoteApp collection.</span></span> <span data-ttu-id="dca49-121">您可以透過使用者的 Azure Active Directory 工作帳戶或 Microsoft 帳戶，將他們指派至這個試用版收藏。</span><span class="sxs-lookup"><span data-stu-id="dca49-121">You can assign users to this trial collection using their Azure Active Directory work accounts or Microsoft accounts.</span></span> <span data-ttu-id="dca49-122">不需再另外訂閱。</span><span class="sxs-lookup"><span data-stu-id="dca49-122">No additional subscription is required.</span></span>

<span data-ttu-id="dca49-123">這是能親自在 RemoteApp 中體驗和感受 Office 的絕佳選項。</span><span class="sxs-lookup"><span data-stu-id="dca49-123">This is a great option to kick the tires and get a good feeling for Office in RemoteApp.</span></span> <span data-ttu-id="dca49-124">不過，此選項僅適用於評估和測試。</span><span class="sxs-lookup"><span data-stu-id="dca49-124">However, this option is intended for evaluation and testing only.</span></span> <span data-ttu-id="dca49-125">使用 Office 2013 Professional Plus (試用版) 範本映像建立的 RemoteApp 收藏無法轉換成實際執行模式，在試用期結束後就會停用。</span><span class="sxs-lookup"><span data-stu-id="dca49-125">RemoteApp collections created using the Office 2013 Professional Plus (trial) template image cannot be transitioned to production mode and will be disabled at the end of the trial period.</span></span>

## <a name="switching-from-trial-to-production"></a><span data-ttu-id="dca49-126">從試用版切換到實際執行</span><span class="sxs-lookup"><span data-stu-id="dca49-126">Switching from trial to production</span></span>
<span data-ttu-id="dca49-127">開始 30 天的免費試用後，入口網站中 RemoteApp 區段的備註會告知您距離轉換為付費帳戶前所剩餘的試用天數。</span><span class="sxs-lookup"><span data-stu-id="dca49-127">When you start your 30-day free trial, a note in the RemoteApp section of the portal will tell you how long you have left in the trial before you need to transition to a paid account.</span></span> <span data-ttu-id="dca49-128">您可以使用這個備註中的連結來啟用您的帳戶並切換成實際執行模式。</span><span class="sxs-lookup"><span data-stu-id="dca49-128">You can activate your account and switch to production mode using the link in this note.</span></span>

<span data-ttu-id="dca49-129">啟用帳戶後，將會影響您帳戶中的所有 RemoteApp 收藏。</span><span class="sxs-lookup"><span data-stu-id="dca49-129">When you activate your account, this will affect all the RemoteApp collections in your account.</span></span>

* <span data-ttu-id="dca49-130">透過 Windows Server 2012 R2 或 Office 365 ProPlus 範本映像執行的收藏將順利地轉換成實際執行。</span><span class="sxs-lookup"><span data-stu-id="dca49-130">Collections that are running with the Windows Server 2012 R2 or the Office 365 ProPlus template images will transition to production seamlessly.</span></span> <span data-ttu-id="dca49-131">所有使用者資料與設定 (包括進行中的工作階段) 都將維持不變。</span><span class="sxs-lookup"><span data-stu-id="dca49-131">All user data and settings, including ongoing sessions, remain intact.</span></span>
* <span data-ttu-id="dca49-132">如果您已上傳自訂範本映像，使用這些映像的收藏也將順利轉換。</span><span class="sxs-lookup"><span data-stu-id="dca49-132">If you have uploaded custom template images, collections using those images will also transition seamlessly.</span></span>
* <span data-ttu-id="dca49-133">Office 2013 Professional Plus (試用版) 範本映像僅適用於評估。</span><span class="sxs-lookup"><span data-stu-id="dca49-133">The Office 2013 Professional Plus (Trial) template image is intended for evaluation only.</span></span> <span data-ttu-id="dca49-134">透過此範本映像執行的收藏無法轉換成實際執行。</span><span class="sxs-lookup"><span data-stu-id="dca49-134">Collections running with this template image cannot be transitioned to production.</span></span> <span data-ttu-id="dca49-135">它們會成為「停用」狀態。</span><span class="sxs-lookup"><span data-stu-id="dca49-135">They will be put in "disabled" state.</span></span>

<span data-ttu-id="dca49-136">如果您在試用期過後還未轉換成實際執行模式，將會停用您的 RemoteApp 收藏。</span><span class="sxs-lookup"><span data-stu-id="dca49-136">If you do not transition to production mode by the expiration of your trial, your RemoteApp collections will be disabled.</span></span> <span data-ttu-id="dca49-137">別擔心，您的設定和使用者資料會持續儲存 90 天，因此，您仍可以啟用您的服務和切換到實際執行模式，不會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="dca49-137">Don't worry - Your settings and users’ data are saved for another 90 days, so you can still activate your service and switch to production mode without any data loss.</span></span>

