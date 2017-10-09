---
title: "Office 與 Azure RemoteApp aaaUsing |Microsoft 文件"
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
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a><span data-ttu-id="c8573-103">使用 Office 與 Azure RemoteApp 搭配</span><span class="sxs-lookup"><span data-stu-id="c8573-103">Using Office with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c8573-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="c8573-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c8573-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c8573-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c8573-106">在 Azure RemoteApp 中裝載 Office 應用程式有兩個選項：Office 365 ProPlus 或 Office 2013 Professional Plus 試用版。</span><span class="sxs-lookup"><span data-stu-id="c8573-106">You have two choices for hosting Office applications in Azure RemoteApp: Office 365 ProPlus or Office 2013 Professional Plus Trial.</span></span>

<span data-ttu-id="c8573-107">**您知道我們即將取代這篇文章的更佳新文章嗎？簽出[如何 toouse 您 Office 365 訂用帳戶與 Azure RemoteApp 一起](remoteapp-officesubscription.md)。它涵蓋了所有您需要使用 Office 365 + Azure RemoteApp 的 hello 資訊。**</span><span class="sxs-lookup"><span data-stu-id="c8573-107">**Hey, did you know we have a new, better article that will soon replace this? Check out [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md). It covers all hello info you need for using Office 365 + Azure RemoteApp.**</span></span>

## <a name="office-365-proplus"></a><span data-ttu-id="c8573-108">Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="c8573-108">Office 365 ProPlus</span></span>
<span data-ttu-id="c8573-109">您可以建立 RemoteApp 集合，使用 Office 365 ProPlus hello 範本映像。</span><span class="sxs-lookup"><span data-stu-id="c8573-109">You can create a RemoteApp collection using hello Office 365 ProPlus template image.</span></span> <span data-ttu-id="c8573-110">此選項可讓您 tooextend 您 Office 365 服務 tooRemoteApp。</span><span class="sxs-lookup"><span data-stu-id="c8573-110">This option allows you tooextend your Office 365 service tooRemoteApp.</span></span> <span data-ttu-id="c8573-111">您必須擁有現有的訂用帳戶方案和您的使用者必須獲得授權，hello Office 365 ProPlus 服務，獨立或透過 hello Office 365 服務方案。</span><span class="sxs-lookup"><span data-stu-id="c8573-111">You must have an existing subscription plan and your users must be licensed for hello Office 365 ProPlus service, either standalone or through hello Office 365 service plans.</span></span>

<span data-ttu-id="c8573-112">RemoteApp 支援 Office 365 共用電腦啟用。</span><span class="sxs-lookup"><span data-stu-id="c8573-112">RemoteApp supports Office 365 Shared Computer Activation.</span></span> <span data-ttu-id="c8573-113">當您啟用共用的電腦啟動過程中，並使用 hello [Office 部署工具](http://www.microsoft.com/download/details.aspx?id=36778)進行安裝，Office 365 ProPlus 會安裝但不啟動。</span><span class="sxs-lookup"><span data-stu-id="c8573-113">When you enable Shared Computer Activation, and use hello [Office Deployment tool](http://www.microsoft.com/download/details.aspx?id=36778) for installation, Office 365 ProPlus installs without being activated.</span></span> <span data-ttu-id="c8573-114">使用者會登入集合，包含 Office 365，Office 會檢查 toosee 如果已針對 Office 365 ProPlus hello 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="c8573-114">When a user signs into a collection that contains Office 365, Office checks toosee if hello user has been provisioned for Office 365 ProPlus.</span></span> <span data-ttu-id="c8573-115">因此，Office 暫時啟用 Office 365 ProPlus-如果此啟用持續發生，直到停止 hello 服務該使用者登。</span><span class="sxs-lookup"><span data-stu-id="c8573-115">If so, Office temporarily activates Office 365 ProPlus - this activation persists until that users signs out of hello service.</span></span>

<span data-ttu-id="c8573-116">toouse Office 365 共用電腦啟動，您需要 toocreate[自訂範本](remoteapp-create-custom-image.md)並安裝 Office 365 ProPlus 存在，請遵循[這些指示](https://technet.microsoft.com/library/dn782858.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c8573-116">toouse Office 365 Shared Computer Activation, you need toocreate a [custom template](remoteapp-create-custom-image.md) and install Office 365 ProPlus there, following [these directions](https://technet.microsoft.com/library/dn782858.aspx).</span></span>

<span data-ttu-id="c8573-117">您可以管理使用者的 Office 365 授權在 hello [Office 365 系統管理入口網站](https://portal.office365.com/)。</span><span class="sxs-lookup"><span data-stu-id="c8573-117">You can manage your users’ Office 365 licenses at hello [Office 365 Admin Portal](https://portal.office365.com/).</span></span> <span data-ttu-id="c8573-118">閱讀更多關於 [Office 365 服務方案](http://technet.microsoft.com/library/office-365-plan-options.aspx)的資訊。</span><span class="sxs-lookup"><span data-stu-id="c8573-118">Read more information about [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span>  

## <a name="office-2013-professional-plus-trial"></a><span data-ttu-id="c8573-119">Office 2013 Professional Plus 試用版</span><span class="sxs-lookup"><span data-stu-id="c8573-119">Office 2013 Professional Plus Trial</span></span>
<span data-ttu-id="c8573-120">在 RemoteApp 的 30 天試用版，您可以使用 hello Office 2013 Professional Plus （試用版） 範本映像 toocreate RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="c8573-120">During a 30-day trial of RemoteApp, you can use hello Office 2013 Professional Plus (trial) template image toocreate a RemoteApp collection.</span></span> <span data-ttu-id="c8573-121">您可以指派使用者 toothis 透過他們的 Azure Active Directory 工作帳戶或 Microsoft 帳戶的試用版集合。</span><span class="sxs-lookup"><span data-stu-id="c8573-121">You can assign users toothis trial collection using their Azure Active Directory work accounts or Microsoft accounts.</span></span> <span data-ttu-id="c8573-122">不需再另外訂閱。</span><span class="sxs-lookup"><span data-stu-id="c8573-122">No additional subscription is required.</span></span>

<span data-ttu-id="c8573-123">這是絕佳的選項 tookick hello 輪胎和良好感受 RemoteApp 中的 Office。</span><span class="sxs-lookup"><span data-stu-id="c8573-123">This is a great option tookick hello tires and get a good feeling for Office in RemoteApp.</span></span> <span data-ttu-id="c8573-124">不過，此選項僅適用於評估和測試。</span><span class="sxs-lookup"><span data-stu-id="c8573-124">However, this option is intended for evaluation and testing only.</span></span> <span data-ttu-id="c8573-125">使用 hello Office 2013 Professional Plus （試用版） 範本映像建立 RemoteApp 集合無法轉換的 tooproduction 模式，且結尾 hello hello 試用期間將會停用。</span><span class="sxs-lookup"><span data-stu-id="c8573-125">RemoteApp collections created using hello Office 2013 Professional Plus (trial) template image cannot be transitioned tooproduction mode and will be disabled at hello end of hello trial period.</span></span>

## <a name="switching-from-trial-tooproduction"></a><span data-ttu-id="c8573-126">從試用 tooproduction 切換</span><span class="sxs-lookup"><span data-stu-id="c8573-126">Switching from trial tooproduction</span></span>
<span data-ttu-id="c8573-127">當您啟動您的 30 天免費試用版時，請注意，在 hello RemoteApp 區段 hello 入口網站會告訴您多久之前還剩下 hello 試用需要 tootransition tooa 付費帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8573-127">When you start your 30-day free trial, a note in hello RemoteApp section of hello portal will tell you how long you have left in hello trial before you need tootransition tooa paid account.</span></span> <span data-ttu-id="c8573-128">您可以啟用您帳戶的和交換器 tooproduction 模式使用此注意事項中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="c8573-128">You can activate your account and switch tooproduction mode using hello link in this note.</span></span>

<span data-ttu-id="c8573-129">當您啟動您的帳戶時，這會影響您的帳戶中的所有 hello RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="c8573-129">When you activate your account, this will affect all hello RemoteApp collections in your account.</span></span>

* <span data-ttu-id="c8573-130">執行 Windows Server 2012 R2 hello 或 hello Office 365 ProPlus 範本映像的集合就會順暢地轉換 tooproduction。</span><span class="sxs-lookup"><span data-stu-id="c8573-130">Collections that are running with hello Windows Server 2012 R2 or hello Office 365 ProPlus template images will transition tooproduction seamlessly.</span></span> <span data-ttu-id="c8573-131">所有使用者資料與設定 (包括進行中的工作階段) 都將維持不變。</span><span class="sxs-lookup"><span data-stu-id="c8573-131">All user data and settings, including ongoing sessions, remain intact.</span></span>
* <span data-ttu-id="c8573-132">如果您已上傳自訂範本映像，使用這些映像的收藏也將順利轉換。</span><span class="sxs-lookup"><span data-stu-id="c8573-132">If you have uploaded custom template images, collections using those images will also transition seamlessly.</span></span>
* <span data-ttu-id="c8573-133">僅供評估是 hello Office 2013 Professional Plus （試用版） 範本映像。</span><span class="sxs-lookup"><span data-stu-id="c8573-133">hello Office 2013 Professional Plus (Trial) template image is intended for evaluation only.</span></span> <span data-ttu-id="c8573-134">執行的範本映像的集合不能轉換的 tooproduction。</span><span class="sxs-lookup"><span data-stu-id="c8573-134">Collections running with this template image cannot be transitioned tooproduction.</span></span> <span data-ttu-id="c8573-135">它們會成為「停用」狀態。</span><span class="sxs-lookup"><span data-stu-id="c8573-135">They will be put in "disabled" state.</span></span>

<span data-ttu-id="c8573-136">如果您無法執行轉換 tooproduction 模式由 hello 到期的試用版，將會停用 RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="c8573-136">If you do not transition tooproduction mode by hello expiration of your trial, your RemoteApp collections will be disabled.</span></span> <span data-ttu-id="c8573-137">也請別擔心-您的設定和使用者的資料會儲存另一個 90 天，所以您仍然可以啟動您的服務和交換器 tooproduction 模式不會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="c8573-137">Don't worry - Your settings and users’ data are saved for another 90 days, so you can still activate your service and switch tooproduction mode without any data loss.</span></span>

