---
title: "aaaPublish 應用程式 tooindividual 使用者的 Azure RemoteApp 集合 （預覽） |Microsoft 文件"
description: "了解如何發行應用程式 tooindividual 使用者，而不是根據 Azure RemoteApp 中的群組，而定。"
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="5080e-103">發行的 Azure RemoteApp 集合 （預覽） 中的應用程式 tooindividual 使用者</span><span class="sxs-lookup"><span data-stu-id="5080e-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5080e-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="5080e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5080e-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5080e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5080e-106">這篇文章說明如何在 Azure RemoteApp 集合 toopublish 應用程式 tooindividual 使用者。</span><span class="sxs-lookup"><span data-stu-id="5080e-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="5080e-107">這是在 Azure RemoteApp 中，目前在私人預覽和可用的唯一 tooselect 早期採用者供評估之用的新功能。</span><span class="sxs-lookup"><span data-stu-id="5080e-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="5080e-108">Azure RemoteApp 原本啟用發行應用程式的方式只有一種： hello 系統管理員會將應用程式從 hello 映像的發佈並可看見 tooall hello 集合中的使用者。</span><span class="sxs-lookup"><span data-stu-id="5080e-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="5080e-109">常見的案例是的 tooinclude 許多應用程式在單一的映像，部署一個集合的順序 tooreduce 管理成本。</span><span class="sxs-lookup"><span data-stu-id="5080e-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="5080e-110">有時候，並非所有應用程式都是相關 tooall 使用者 – 系統管理員喜歡 toopublish tooindividual 應用程式的使用者，讓他們無法看到其摘要的應用程式中不必要的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5080e-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="5080e-111">現在 Azure RemoteApp 已提供這項功能，但目前為受限制的預覽功能。</span><span class="sxs-lookup"><span data-stu-id="5080e-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="5080e-112">Hello 新功能的簡短摘要如下：</span><span class="sxs-lookup"><span data-stu-id="5080e-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="5080e-113">集合可以設定成兩種模式之一：</span><span class="sxs-lookup"><span data-stu-id="5080e-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="5080e-114">hello 原始集合模式中，集合中的所有使用者可以都查看所有已發行應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="5080e-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="5080e-115">這是 hello 預設模式。</span><span class="sxs-lookup"><span data-stu-id="5080e-115">This is hello default mode.</span></span>
   * <span data-ttu-id="5080e-116">hello 新應用程式模式中，使用者只看到應用程式已被明確指派 toothem</span><span class="sxs-lookup"><span data-stu-id="5080e-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="5080e-117">在 hello 時刻 hello 應用程式模式下才可以啟用使用 Azure RemoteApp PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5080e-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="5080e-118">當設定 tooapplication 模式 hello 集合中的使用者指派無法透過 hello Azure 入口網站進行管理。</span><span class="sxs-lookup"><span data-stu-id="5080e-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="5080e-119">使用者指派具有 toobe 透過 PowerShell cmdlet 來管理。</span><span class="sxs-lookup"><span data-stu-id="5080e-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="5080e-120">使用者只會看到 hello 應用程式直接發行 toothem。</span><span class="sxs-lookup"><span data-stu-id="5080e-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="5080e-121">不過，它還是可能對使用者 toolaunch hello hello 映像上可用的其他應用程式藉由直接在 hello 作業系統中存取它們。</span><span class="sxs-lookup"><span data-stu-id="5080e-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="5080e-122">這項功能不會提供安全的應用程式鎖定它只會限制摘要的 hello 應用程式中的可見性。</span><span class="sxs-lookup"><span data-stu-id="5080e-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="5080e-123">如果您需要 tooisolate 使用者從應用程式，您必須 toouse 個別集合的。</span><span class="sxs-lookup"><span data-stu-id="5080e-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="5080e-124">如何 tooget Azure RemoteApp PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="5080e-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="5080e-125">tootry hello 新預覽的功能，您將需要 toouse Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5080e-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="5080e-126">它是目前不可能 toouse hello Azure Management 入口網站 tooenable hello 新應用程式發行模式。</span><span class="sxs-lookup"><span data-stu-id="5080e-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="5080e-127">首先，請確定您擁有 hello [Azure PowerShell 模組](/powershell/azure/overview)安裝。</span><span class="sxs-lookup"><span data-stu-id="5080e-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="5080e-128">然後啟動在系統管理員模式下，執行下列 cmdlet 的 hello hello PowerShell 主控台：</span><span class="sxs-lookup"><span data-stu-id="5080e-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="5080e-129">它會提示您輸入 Azure 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5080e-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="5080e-130">一旦登入，您將無法 toorun Azure RemoteApp cmdlet 針對您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5080e-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="5080e-131">如何 toocheck 集合是在哪個模式下</span><span class="sxs-lookup"><span data-stu-id="5080e-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="5080e-132">執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="5080e-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![核取 hello 收集模式](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="5080e-134">hello AclLevel 屬性可以有下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="5080e-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="5080e-135">集合： hello 原始發行模式。</span><span class="sxs-lookup"><span data-stu-id="5080e-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="5080e-136">所有使用者都能看到所有已發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5080e-136">All users see all published apps.</span></span>
* <span data-ttu-id="5080e-137">應用程式： hello 新發行的模式。</span><span class="sxs-lookup"><span data-stu-id="5080e-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="5080e-138">使用者會看到只有 hello 應用程式直接發佈 toothem。</span><span class="sxs-lookup"><span data-stu-id="5080e-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="5080e-139">如何 tooswitch tooapplication 發佈模式</span><span class="sxs-lookup"><span data-stu-id="5080e-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="5080e-140">執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="5080e-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="5080e-141">應用程式的發行狀態將會保留： 一開始的所有使用者會都看到所有 hello 原始發行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5080e-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="5080e-142">如何 toolist，使用者可以看到特定的應用程式</span><span class="sxs-lookup"><span data-stu-id="5080e-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="5080e-143">執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="5080e-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="5080e-144">這樣就會列出所有使用者都可以看到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5080e-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="5080e-145">注意： 您可以看見 hello 應用程式的別名 （在上述的 hello 語法中稱為 「 應用程式的別名"） 執行 Get AzureRemoteAppProgram CollectionName <collectionName>。</span><span class="sxs-lookup"><span data-stu-id="5080e-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="5080e-146">如何 tooassign 應用程式 tooa 使用者</span><span class="sxs-lookup"><span data-stu-id="5080e-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="5080e-147">執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="5080e-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="5080e-148">hello 使用者現在會看見 hello hello Azure RemoteApp 用戶端中的應用程式，且將無法 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="5080e-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="5080e-149">如何 tooremove 使用者從應用程式</span><span class="sxs-lookup"><span data-stu-id="5080e-149">How tooremove an application from a user</span></span>
<span data-ttu-id="5080e-150">執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="5080e-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="5080e-151">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5080e-151">Providing feedback</span></span>
<span data-ttu-id="5080e-152">歡迎您提供有關這項預覽功能的意見反應和建議。</span><span class="sxs-lookup"><span data-stu-id="5080e-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="5080e-153">請填寫 hello[調查](http://www.instant.ly/s/FDdrb)toolet 我們知道您的想法。</span><span class="sxs-lookup"><span data-stu-id="5080e-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="5080e-154">沒機會 tootry hello 預覽功能嗎？</span><span class="sxs-lookup"><span data-stu-id="5080e-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="5080e-155">如果您未參與 hello 預覽尚未，請使用這項[調查](http://www.instant.ly/s/AY83p)toorequest 存取。</span><span class="sxs-lookup"><span data-stu-id="5080e-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

