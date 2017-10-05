---
title: "在 Azure RemoteApp 集合中發佈應用程式給個別使用者 (預覽) | Microsoft Docs"
description: "了解如何在 Azure RemoteApp 中發佈應用程式給個別使用者，而非以群組為單位來發佈。"
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
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="227df-103">在 Azure RemoteApp 集合中發佈應用程式給個別使用者 (預覽)</span><span class="sxs-lookup"><span data-stu-id="227df-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="227df-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="227df-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="227df-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="227df-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="227df-106">本文說明如何在 Azure RemoteApp 集合中發佈應用程式給個別使用者。</span><span class="sxs-lookup"><span data-stu-id="227df-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="227df-107">這是 Azure RemoteApp 的新功能，目前還是私人預覽狀態，僅提供給選出的早期採用者進行評估。</span><span class="sxs-lookup"><span data-stu-id="227df-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span></span>

<span data-ttu-id="227df-108">Azure RemoteApp 最初只啟用一種發佈應用程式的方式：系統管理員會從映像發佈應用程式，而且集合中的所有使用者都能看見。</span><span class="sxs-lookup"><span data-stu-id="227df-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span></span>

<span data-ttu-id="227df-109">常見的案例是在單一映像中包含許多應用程式並部署一個集合，以降低管理成本。</span><span class="sxs-lookup"><span data-stu-id="227df-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span></span> <span data-ttu-id="227df-110">但有時候並非所有應用程式都與所有使用者有關，因此系統管理員會想要將應用程式發佈給個別使用者，讓使用者不會在應用程式摘要中看到不必要的應用程式。</span><span class="sxs-lookup"><span data-stu-id="227df-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="227df-111">現在 Azure RemoteApp 已提供這項功能，但目前為受限制的預覽功能。</span><span class="sxs-lookup"><span data-stu-id="227df-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="227df-112">以下是新功能的簡短摘要：</span><span class="sxs-lookup"><span data-stu-id="227df-112">Here is a brief summary of the new functionality:</span></span>

1. <span data-ttu-id="227df-113">集合可以設定成兩種模式之一：</span><span class="sxs-lookup"><span data-stu-id="227df-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="227df-114">原始的集合模式，在此模式中，集合內的所有使用者都可以看到所有已發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="227df-114">the original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="227df-115">這是預設模式。</span><span class="sxs-lookup"><span data-stu-id="227df-115">This is the default mode.</span></span>
   * <span data-ttu-id="227df-116">新推出的應用程式模式，在此模式中，使用者只能看見明確指派給他們的應用程式</span><span class="sxs-lookup"><span data-stu-id="227df-116">the new application mode, where users only see applications that have been explicitly assigned to them</span></span>
2. <span data-ttu-id="227df-117">應用程式模式目前只能使用 Azure RemoteApp PowerShell Cmdlet 來啟用。</span><span class="sxs-lookup"><span data-stu-id="227df-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="227df-118">設定為應用程式模式時，將無法透過 Azure 入口網站管理集合中的使用者指派。</span><span class="sxs-lookup"><span data-stu-id="227df-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span></span> <span data-ttu-id="227df-119">您必須透過 PowerShell Cmdlet 管理使用者指派。</span><span class="sxs-lookup"><span data-stu-id="227df-119">User assignment has to be managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="227df-120">使用者只會看到直接發佈給他們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="227df-120">Users will only see the applications published directly to them.</span></span> <span data-ttu-id="227df-121">不過，使用者若想啟動映像上的其他可用應用程式，仍可藉由在作業系統中直接進行存取來達成。</span><span class="sxs-lookup"><span data-stu-id="227df-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span></span>
   
   * <span data-ttu-id="227df-122">此功能只是限制應用程式摘要中的可見性，並不提供應用程式的安全鎖定。</span><span class="sxs-lookup"><span data-stu-id="227df-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span></span>
   * <span data-ttu-id="227df-123">如果您需要讓使用者與應用程式隔離開來，您必須使用不同的集合。</span><span class="sxs-lookup"><span data-stu-id="227df-123">If you need to isolate users from applications, you will need to use separate collections for that.</span></span>

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="227df-124">如何取得 Azure RemoteApp PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="227df-124">How to get Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="227df-125">若要嘗試新的預覽功能，您必須使用 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="227df-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span></span> <span data-ttu-id="227df-126">目前還無法使用 Azure 管理入口網站來啟用新的應用程式發佈模式。</span><span class="sxs-lookup"><span data-stu-id="227df-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span></span>

<span data-ttu-id="227df-127">首先請確定您已安裝 [Azure PowerShell 模組](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="227df-127">First, make sure you have the [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="227df-128">然後以系統管理員模式啟動 PowerShell 主控台，並執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="227df-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="227df-129">它會提示您輸入 Azure 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="227df-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="227df-130">登入後，您就可以針對 Azure 訂用帳戶執行 Azure RemoteApp Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="227df-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-to-check-which-mode-a-collection-is-in"></a><span data-ttu-id="227df-131">如何確認集合目前是什麼模式</span><span class="sxs-lookup"><span data-stu-id="227df-131">How to check which mode a collection is in</span></span>
<span data-ttu-id="227df-132">執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="227df-132">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![查看集合模式](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="227df-134">AclLevel 屬性的可能值如下：</span><span class="sxs-lookup"><span data-stu-id="227df-134">The AclLevel property can have the following values:</span></span>

* <span data-ttu-id="227df-135">集合：原始發佈模式。</span><span class="sxs-lookup"><span data-stu-id="227df-135">Collection: the original publishing mode.</span></span> <span data-ttu-id="227df-136">所有使用者都能看到所有已發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="227df-136">All users see all published apps.</span></span>
* <span data-ttu-id="227df-137">應用程式：新的發佈模式。</span><span class="sxs-lookup"><span data-stu-id="227df-137">Application: the new publishing mode.</span></span> <span data-ttu-id="227df-138">使用者只會看到直接發佈給他們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="227df-138">Users see only the apps published directly to them.</span></span>

## <a name="how-to-switch-to-application-publishing-mode"></a><span data-ttu-id="227df-139">如何切換為應用程式發佈模式</span><span class="sxs-lookup"><span data-stu-id="227df-139">How to switch to application publishing mode</span></span>
<span data-ttu-id="227df-140">執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="227df-140">Run the following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="227df-141">應用程式發佈狀態將會保留下來：一開始所有使用者會看到所有原本已發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="227df-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span></span>

## <a name="how-to-list-users-who-can-see-a-specific-application"></a><span data-ttu-id="227df-142">如何列出可以看到特定應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="227df-142">How to list users who can see a specific application</span></span>
<span data-ttu-id="227df-143">執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="227df-143">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="227df-144">這會列出所有能看到應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="227df-144">This lists all users who can see the application.</span></span>

<span data-ttu-id="227df-145">附註：執行 Get-AzureRemoteAppProgram -CollectionName 就能看到應用程式別名 (在上述語法中稱為 "app alias") <collectionName>。</span><span class="sxs-lookup"><span data-stu-id="227df-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-to-assign-an-application-to-a-user"></a><span data-ttu-id="227df-146">如何指派應用程式給使用者</span><span class="sxs-lookup"><span data-stu-id="227df-146">How to assign an application to a user</span></span>
<span data-ttu-id="227df-147">執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="227df-147">Run the following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="227df-148">使用者現在將會看到 Azure RemoteApp 用戶端中的應用程式，並且能夠與其連接。</span><span class="sxs-lookup"><span data-stu-id="227df-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span></span>

## <a name="how-to-remove-an-application-from-a-user"></a><span data-ttu-id="227df-149">如何移除使用者的應用程式</span><span class="sxs-lookup"><span data-stu-id="227df-149">How to remove an application from a user</span></span>
<span data-ttu-id="227df-150">執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="227df-150">Run the following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="227df-151">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="227df-151">Providing feedback</span></span>
<span data-ttu-id="227df-152">歡迎您提供有關這項預覽功能的意見反應和建議。</span><span class="sxs-lookup"><span data-stu-id="227df-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="227df-153">請填寫 [問卷](http://www.instant.ly/s/FDdrb) ，以讓我們知道您的想法。</span><span class="sxs-lookup"><span data-stu-id="227df-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span></span>

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a><span data-ttu-id="227df-154">還沒有機會試用預覽功能嗎？</span><span class="sxs-lookup"><span data-stu-id="227df-154">Haven't had a chance to try the preview feature?</span></span>
<span data-ttu-id="227df-155">如果您還未參與使用預覽功能，請使用本 [問卷](http://www.instant.ly/s/AY83p) 來要求存取權。</span><span class="sxs-lookup"><span data-stu-id="227df-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span></span>

