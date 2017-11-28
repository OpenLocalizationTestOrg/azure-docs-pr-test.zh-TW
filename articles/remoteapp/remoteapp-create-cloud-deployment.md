---
title: "如何建立 Azure RemoteApp 的雲端收藏 | Microsoft Docs"
description: "了解如何建立將資料儲存在 Azure 雲端中的 Azure RemoteApp 部署。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 52d5a073c0de42a77cd7163bf402ed2cdf598d95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-cloud-collection-of-azure-remoteapp"></a><span data-ttu-id="92210-103">如何建立 Azure RemoteApp 的雲端收藏</span><span class="sxs-lookup"><span data-stu-id="92210-103">How to create a cloud collection of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="92210-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="92210-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="92210-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="92210-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="92210-106">[Azure RemoteApp 收藏](remoteapp-collections.md)分成兩種：</span><span class="sxs-lookup"><span data-stu-id="92210-106">There are two kinds of [Azure RemoteApp collections](remoteapp-collections.md):</span></span> 

* <span data-ttu-id="92210-107">雲端：完全位於 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="92210-107">Cloud: resides completely in Azure.</span></span> <span data-ttu-id="92210-108">您可以選擇在雲端儲存所有資料 (也就是僅限雲端的集合) 或將您的集合連線到 VNET，並於該處儲存資料。</span><span class="sxs-lookup"><span data-stu-id="92210-108">You can choose to save all data in the cloud (so a cloud-only collection) or to connect your collection to a VNET and save data there.</span></span>   
* <span data-ttu-id="92210-109">混合式：包含可內部存取的虛擬網路，這需要使用 Azure AD 和內部部署的 Active Directory 環境。</span><span class="sxs-lookup"><span data-stu-id="92210-109">Hybrid: includes a virtual network for on-premises access - this requires the use of Azure AD and an on-premises Active Directory environment.</span></span>

<span data-ttu-id="92210-110">本教學課程將逐步引導您完成建立雲端收藏的程序。</span><span class="sxs-lookup"><span data-stu-id="92210-110">This tutorial walks you through the process of creating a cloud collection.</span></span> <span data-ttu-id="92210-111">共有四個步驟：</span><span class="sxs-lookup"><span data-stu-id="92210-111">There are four steps:</span></span> 

1. <span data-ttu-id="92210-112">建立 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="92210-112">Create an Azure RemoteApp collection.</span></span>
2. <span data-ttu-id="92210-113">選擇性地設定目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="92210-113">Optionally configure directory synchronization.</span></span> <span data-ttu-id="92210-114">如果您使用 Azure AD + Active Directory，就必須將使用者、連絡人和密碼從您的內部部署 Active Directory 同步處理至 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92210-114">If you are using Azure AD + Active Directory, you have to synchronize users, contacts, and passwords from your on-premises Active Directory to your Azure AD tenant.</span></span>
3. <span data-ttu-id="92210-115">發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="92210-115">Publish apps.</span></span>
4. <span data-ttu-id="92210-116">設定使用者存取。</span><span class="sxs-lookup"><span data-stu-id="92210-116">Configure user access.</span></span>

<span data-ttu-id="92210-117">**開始之前**</span><span class="sxs-lookup"><span data-stu-id="92210-117">**Before you begin**</span></span>

<span data-ttu-id="92210-118">在建立收藏之前，您必須執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="92210-118">You need to do the following before creating the collection:</span></span>

* <span data-ttu-id="92210-119">[註冊](https://azure.microsoft.com/services/remoteapp/) Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="92210-119">[Sign up](https://azure.microsoft.com/services/remoteapp/) for Azure RemoteApp.</span></span> 
* <span data-ttu-id="92210-120">收集您想授與存取權之使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="92210-120">Gather information about the users that you want to grant access to.</span></span> <span data-ttu-id="92210-121">這可以是使用者 Microsoft 帳戶資訊或 Active Directory 工作帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="92210-121">This can be either Microsoft account information or Active Directory work account information for users.</span></span>
* <span data-ttu-id="92210-122">此程序假設您將使用您的訂閱隨附的範本映像之一，或是您已上傳所要使用的範本映像。</span><span class="sxs-lookup"><span data-stu-id="92210-122">This procedure assumes you are either going to use one of the template images provided as part of your subscription or that you have already uploaded the template image you want to use.</span></span> <span data-ttu-id="92210-123">如果您需要上傳不同的範本映像，您可以從 [範本映像] 頁面執行此作業。</span><span class="sxs-lookup"><span data-stu-id="92210-123">If you need to upload a different template image, you can do that from the Template Images page.</span></span> <span data-ttu-id="92210-124">只要按一下 [上傳範本映像]  ，然後遵循精靈中的步驟即可。</span><span class="sxs-lookup"><span data-stu-id="92210-124">Just click **upload a template image** and follow the steps in the wizard.</span></span> 
* <span data-ttu-id="92210-125">想要使用 Office 365 ProPlus 的映像嗎？</span><span class="sxs-lookup"><span data-stu-id="92210-125">Want to use the Office 365 ProPlus image?</span></span> <span data-ttu-id="92210-126">請在 [這裡](remoteapp-officesubscription.md)查看資訊。</span><span class="sxs-lookup"><span data-stu-id="92210-126">Check out info [here](remoteapp-officesubscription.md).</span></span>
* <span data-ttu-id="92210-127">想提供自訂應用程式或 LOB 程式？</span><span class="sxs-lookup"><span data-stu-id="92210-127">Want to provide custom apps or LOB programs?</span></span> <span data-ttu-id="92210-128">請建立新的 [映像](remoteapp-imageoptions.md) ，並在您的雲端部署中加以使用。</span><span class="sxs-lookup"><span data-stu-id="92210-128">Create a new [image](remoteapp-imageoptions.md) and use it in your cloud collection.</span></span>
* <span data-ttu-id="92210-129">了解您是否需要連接到 VNET。</span><span class="sxs-lookup"><span data-stu-id="92210-129">Figure out whether you need to connect to a VNET.</span></span> <span data-ttu-id="92210-130">如果您選擇連接到 VNET，請確定它是否符合[調整大小的指導方針](remoteapp-vnetsizing.md)，以及它是否[可以連接到 RemoteApp](remoteapp-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="92210-130">If you choose to connect to a VNET, make sure it meets the [sizing guidelines](remoteapp-vnetsizing.md) and that it [can connect to RemoteApp](remoteapp-vnet.md).</span></span> <span data-ttu-id="92210-131">如需詳細資訊，請參閱 [VNET 規劃文章 ](remoteapp-planvnet.md)。</span><span class="sxs-lookup"><span data-stu-id="92210-131">Check out the [VNET planning article ](remoteapp-planvnet.md)for more information.</span></span>
* <span data-ttu-id="92210-132">如果您使用 VNET，請決定是否要將它聯結至本機 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="92210-132">If you're using a VNET, decide whether you want to join it to your local Active Directory domain.</span></span>

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a><span data-ttu-id="92210-133">步驟 1：建立雲端集合 - 不論是否有 VNET</span><span class="sxs-lookup"><span data-stu-id="92210-133">Step 1: Create a cloud collection - with or without a VNET</span></span>
<span data-ttu-id="92210-134">請使用下列步驟 **建立純雲端集合**：</span><span class="sxs-lookup"><span data-stu-id="92210-134">Use the following steps to **create a cloud-only collection**:</span></span>

1. <span data-ttu-id="92210-135">在 Azure 管理入口網站中，移至 RemoteApp 頁面。</span><span class="sxs-lookup"><span data-stu-id="92210-135">In the management portal, go to the RemoteApp page.</span></span>
2. <span data-ttu-id="92210-136">按一下 [新增] > [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="92210-136">Click **New > Quick Create**.</span></span>
3. <span data-ttu-id="92210-137">輸入收藏的名稱，然後選取區域。</span><span class="sxs-lookup"><span data-stu-id="92210-137">Enter a name for your collection, and select your region.</span></span>
4. <span data-ttu-id="92210-138">選擇您要使用的方案 - 標準或基本。</span><span class="sxs-lookup"><span data-stu-id="92210-138">Choose the plan that you want to use - standard or basic.</span></span>
5. <span data-ttu-id="92210-139">選擇要用於此收藏的範本。</span><span class="sxs-lookup"><span data-stu-id="92210-139">Choose the template to use for this collection.</span></span> 
   
    <span data-ttu-id="92210-140">**提示：** 您的 RemoteApp 訂閱會隨附於包含 Office 365 或 Office 2013 (供試用) 程式的 [範本映像](remoteapp-images.md) ，其中有些程式已發佈 (例如 Word)，有些即將發佈。</span><span class="sxs-lookup"><span data-stu-id="92210-140">**Tip:** Your subscription for RemoteApp comes with [template images](remoteapp-images.md) that contain Office 365 or Office 2013 (for trial use) programs, some published (such as Word) and others ready to publish.</span></span> <span data-ttu-id="92210-141">您也可以建立新的 [映像](remoteapp-imageoptions.md) ，並在您的雲端部署中加以使用。</span><span class="sxs-lookup"><span data-stu-id="92210-141">You can also create a new [image](remoteapp-imageoptions.md) and use it in your cloud collection.</span></span>
6. <span data-ttu-id="92210-142">按一下 [建立 RemoteApp 收藏] 。</span><span class="sxs-lookup"><span data-stu-id="92210-142">Click **Create RemoteApp collection**.</span></span>
   
    <span data-ttu-id="92210-143">**重要：** 佈建收藏最多可能需要 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="92210-143">**Important:** It can take up to 30 minutes to provision your collection.</span></span>

<span data-ttu-id="92210-144">建立了 Azure RemoteApp 集合之後，請按兩下集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="92210-144">After your Azure RemoteApp collection has been created, double-click the name of the collection.</span></span> <span data-ttu-id="92210-145">這時會顯示 [快速入門]  頁面，您可以在這裡完成設定集合。</span><span class="sxs-lookup"><span data-stu-id="92210-145">That will bring up the **Quick Start** page - this is where you finish configuring the collection.</span></span>

<span data-ttu-id="92210-146">請使用下列步驟建立 **雲端 + VNET 集合**：</span><span class="sxs-lookup"><span data-stu-id="92210-146">Use the following steps to create a **cloud + VNET collection**:</span></span>

1. <span data-ttu-id="92210-147">在管理入口網站中，前往 [Azure RemoteApp] 頁面。</span><span class="sxs-lookup"><span data-stu-id="92210-147">In the management portal, go to the Azure RemoteApp page.</span></span>
2. <span data-ttu-id="92210-148">按一下 [新增] > [使用 VNET 建立]。</span><span class="sxs-lookup"><span data-stu-id="92210-148">Click **New** > **Create with VNET**.</span></span>
3. <span data-ttu-id="92210-149">輸入收藏的名稱。</span><span class="sxs-lookup"><span data-stu-id="92210-149">Enter a name for your collection.</span></span>
4. <span data-ttu-id="92210-150">選擇您要使用的方案 - 標準或基本。</span><span class="sxs-lookup"><span data-stu-id="92210-150">Choose the plan that you want to use - standard or basic.</span></span>
5. <span data-ttu-id="92210-151">選擇您已經建立的 VNET。</span><span class="sxs-lookup"><span data-stu-id="92210-151">Choose the VNET you already created.</span></span> <span data-ttu-id="92210-152">不知道該怎麼做？</span><span class="sxs-lookup"><span data-stu-id="92210-152">Don't know how to do that?</span></span> <span data-ttu-id="92210-153">這些步驟目前都在 [混合式](remoteapp-create-hybrid-deployment.md) 主題中。</span><span class="sxs-lookup"><span data-stu-id="92210-153">For now, the steps are in the [hybrid](remoteapp-create-hybrid-deployment.md) topic.</span></span>
6. <span data-ttu-id="92210-154">決定您是否要將集合聯結至網域。</span><span class="sxs-lookup"><span data-stu-id="92210-154">Decide whether you want to join your collection to your domain.</span></span> <span data-ttu-id="92210-155">如果是，您需要使用 AD Connect 來整合 Azure AD 及 Active Directory 環境。</span><span class="sxs-lookup"><span data-stu-id="92210-155">If yes, you'll need to use AD Connect to integrate Azure AD and your Active Directory environment.</span></span> <span data-ttu-id="92210-156">這涵蓋在 **步驟 2**中。</span><span class="sxs-lookup"><span data-stu-id="92210-156">That's covered in below in **Step 2**.</span></span>
7. <span data-ttu-id="92210-157">按一下 [建立 RemoteApp 收藏] 。</span><span class="sxs-lookup"><span data-stu-id="92210-157">Click **Create RemoteApp collection**.</span></span>

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a><span data-ttu-id="92210-158">步驟 2：設定 Active Directory 目錄同步處理 (選用)</span><span class="sxs-lookup"><span data-stu-id="92210-158">Step 2: Configure Active Directory directory synchronization (optional)</span></span>
<span data-ttu-id="92210-159">如果您要使用 Active Directory，則必須在 Azure Active Directory 與您的內部部署 Active Directory 之間進行目錄同步處理，RemoteApp 才能將使用者、連絡人和密碼同步處理至您的 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92210-159">If you want to use Active Directory, Azure RemoteApp requires directory synchronization between Azure Active Directory and your on-premises Active Directory to synchronize users,  contacts, and passwords to your Azure Active Directory tenant.</span></span> <span data-ttu-id="92210-160">如需規劃資訊，請參閱 [設定 Azure RemoteApp 的 Active Directory](remoteapp-ad.md) 。</span><span class="sxs-lookup"><span data-stu-id="92210-160">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for planning information.</span></span> <span data-ttu-id="92210-161">您也可以直接移至 [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) 以取得資訊。</span><span class="sxs-lookup"><span data-stu-id="92210-161">You can also go directly to [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) for information.</span></span>

## <a name="step-3-publish-apps"></a><span data-ttu-id="92210-162">步驟 3：發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="92210-162">Step 3: Publish apps</span></span>
<span data-ttu-id="92210-163">Azure RemoteApp 應用程式就是您提供給使用者的應用程式或程式。</span><span class="sxs-lookup"><span data-stu-id="92210-163">An Azure RemoteApp app is the app or program that you provide to your users.</span></span> <span data-ttu-id="92210-164">此程式位於您為收藏上傳的範本映像中。</span><span class="sxs-lookup"><span data-stu-id="92210-164">It is located in the template image you uploaded for the collection.</span></span> <span data-ttu-id="92210-165">當使用者存取應用程式時，應用程式看起來會像是在本機環境中執行，但其實是在 Azure 中的虛擬機器中執行。</span><span class="sxs-lookup"><span data-stu-id="92210-165">When a user accesses an app, the app appears to run in their local environment, but it is really running in a virtual machine in Azure.</span></span> 

<span data-ttu-id="92210-166">您必須先發佈應用程式，您的使用者才能存取應用程式 – 發佈應用程式可讓您的使用者透過遠端桌面用戶端存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="92210-166">Before your users can access apps, you need to publish them – publishing apps lets your users access the apps through the Remote Desktop client.</span></span>

<span data-ttu-id="92210-167">您可以將多個應用程式發佈到自己的 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="92210-167">You can publish multiple apps to your Azure RemoteApp collection.</span></span> <span data-ttu-id="92210-168">請在發佈頁面中按一下 [發佈]  來新增程式。</span><span class="sxs-lookup"><span data-stu-id="92210-168">From the publishing page, click **Publish** to add a program.</span></span> <span data-ttu-id="92210-169">您可以從範本映像的 [開始]  功能表發佈，或藉由為 App 指定範本映像的路徑來發佈。</span><span class="sxs-lookup"><span data-stu-id="92210-169">You can either publish from the **Start** menu of the template image or by specifying the path on the template image for the app.</span></span> <span data-ttu-id="92210-170">如果您選擇從 [開始]  功能表新增，請選擇要發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="92210-170">If you choose to add from the **Start** menu, choose the app to publish.</span></span> <span data-ttu-id="92210-171">如果您選擇提供應用程式的路徑，請提供應用程式的名稱，以及應用程式在範本映像上的安裝路徑。</span><span class="sxs-lookup"><span data-stu-id="92210-171">If you choose to provide the path to the app, provide a name for the app and the path to where it is installed on the template image.</span></span>

## <a name="step-4-configure-user-access"></a><span data-ttu-id="92210-172">步驟 4：設定使用者存取</span><span class="sxs-lookup"><span data-stu-id="92210-172">Step 4: Configure user access</span></span>
<span data-ttu-id="92210-173">您已經建立集合，現在您必須新增可使用您遠端資源的使用者。</span><span class="sxs-lookup"><span data-stu-id="92210-173">Now that you have created your collection, you need to add the users that you want to be able to use your remote resources.</span></span> <span data-ttu-id="92210-174">如果您使用 Active Directory，則您要給予存取權的使用者，必須存在於與您用來建立此集合的訂用帳戶相關聯的 Active Directory 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="92210-174">If you are using Active Directory, the users that you provide access to need to exist in the Active Directory tenant associated with the subscription you used to create this collection.</span></span>

1. <span data-ttu-id="92210-175">在 [快速入門] 頁面上，按一下 [Configure user access] 。</span><span class="sxs-lookup"><span data-stu-id="92210-175">From the Quick Start page, click **Configure user access**.</span></span> 
2. <span data-ttu-id="92210-176">輸入工作帳戶 (來自於 Active Directory)，或是您要為其授與存取權的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="92210-176">Enter the work account (from Active Directory) or Microsoft account that you want to grant access for.</span></span>
   
   <span data-ttu-id="92210-177">**注意：**</span><span class="sxs-lookup"><span data-stu-id="92210-177">**Notes:**</span></span> 
   
   <span data-ttu-id="92210-178">請確定您使用 *user@domain.com* 格式。</span><span class="sxs-lookup"><span data-stu-id="92210-178">Make sure that you use the *user@domain.com* format.</span></span>
   
   <span data-ttu-id="92210-179">如果您的收藏中使用 Office 365 ProPlus，您必須為使用者使用 Active Directory 身分識別。</span><span class="sxs-lookup"><span data-stu-id="92210-179">If you are using Office 365 ProPlus in your collection, you must use the Active Directory identities for your users.</span></span> <span data-ttu-id="92210-180">這有助於驗證授權。</span><span class="sxs-lookup"><span data-stu-id="92210-180">This helps validate licensing.</span></span> 
3. <span data-ttu-id="92210-181">在驗證使用者之後，按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="92210-181">After the users are validated, click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92210-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92210-182">Next steps</span></span>
<span data-ttu-id="92210-183">您已經成功建立並部署了自己的 Azure RemoteApp 雲端收藏。</span><span class="sxs-lookup"><span data-stu-id="92210-183">That's it - you have successfully created and deployed your Azure RemoteApp cloud collection.</span></span> <span data-ttu-id="92210-184">下一個步驟是要讓使用者下載並安裝遠端桌面用戶端。</span><span class="sxs-lookup"><span data-stu-id="92210-184">The next step is to have your users download and install the Remote Desktop client.</span></span> <span data-ttu-id="92210-185">您可以在 Azure RemoteApp 的 [快速啟動] 頁面上找到用戶端的 URL。</span><span class="sxs-lookup"><span data-stu-id="92210-185">You can find the URL for the client on the Azure RemoteApp Quick Start page.</span></span> <span data-ttu-id="92210-186">接著，請讓使用者登入用戶端，並存取您所發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="92210-186">Then, have users log into the client and access the apps you published.</span></span>

### <a name="help-us-help-you"></a><span data-ttu-id="92210-187">幫我們來協助您</span><span class="sxs-lookup"><span data-stu-id="92210-187">Help us help you</span></span>
<span data-ttu-id="92210-188">您知道除了評比這篇文章以及在下面留言以外，您可以變更文件本身嗎？</span><span class="sxs-lookup"><span data-stu-id="92210-188">Did you know that in addition to rating this article and making comments down below, you can make changes to the article itself?</span></span> <span data-ttu-id="92210-189">有所遺漏？</span><span class="sxs-lookup"><span data-stu-id="92210-189">Something missing?</span></span> <span data-ttu-id="92210-190">有所錯誤？</span><span class="sxs-lookup"><span data-stu-id="92210-190">Something wrong?</span></span> <span data-ttu-id="92210-191">我是否撰寫了令人混淆的內容？</span><span class="sxs-lookup"><span data-stu-id="92210-191">Did I write something that's just confusing?</span></span> <span data-ttu-id="92210-192">向上捲動並按一下 [在 GitHub 上編輯]  以進行變更 - 系統會顯示這些變更以供我們檢閱，而我們簽核後，您就會在這裡看到您所進行的變更和改良。</span><span class="sxs-lookup"><span data-stu-id="92210-192">Scroll up and click **Edit on GitHub** to make changes - those will come to us for review, and then, once we sign off on them, you'll see your changes and improvements right here.</span></span>

