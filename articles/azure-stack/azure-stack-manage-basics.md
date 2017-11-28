---
title: "aaaAzure 堆疊管理基本概念 |Microsoft 文件"
description: "了解您的需要 tooknow tooadminister Azure 堆疊。"
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 856738a7-1510-442a-88a8-d316c67c757c
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: twooley
ms.openlocfilehash: cdf2818e9fc819b448508ca52bbdbec259890265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-administration-basics"></a><span data-ttu-id="8c596-103">Azure Stack 管理基本知識</span><span class="sxs-lookup"><span data-stu-id="8c596-103">Azure Stack administration basics</span></span>

<span data-ttu-id="8c596-104">有幾件事，您需要 tooknow，如果您是新 tooAzure 堆疊管理。</span><span class="sxs-lookup"><span data-stu-id="8c596-104">There are several things you need tooknow if you're new tooAzure Stack administration.</span></span> <span data-ttu-id="8c596-105">本指南概述您角色的雲端運算子，以及您為他們需要 tootell 您的使用者生產力 toobecome 快速。</span><span class="sxs-lookup"><span data-stu-id="8c596-105">This guidance provides an overview of your role as a cloud operator, and what you need tootell your users for them toobecome productive quickly.</span></span>

## <a name="understand-development-kit-builds"></a><span data-ttu-id="8c596-106">了解開發套件組建</span><span class="sxs-lookup"><span data-stu-id="8c596-106">Understand development kit builds</span></span>

<span data-ttu-id="8c596-107">檢閱 hello[什麼是 Azure 堆疊？](azure-stack-poc.md)文章 toomake 確定您了解 hello 目的 hello Azure 堆疊開發套件，以及其限制。</span><span class="sxs-lookup"><span data-stu-id="8c596-107">Review hello [What is Azure Stack?](azure-stack-poc.md) article toomake sure you understand hello purpose of hello Azure Stack Development Kit, and its limitations.</span></span> <span data-ttu-id="8c596-108">您應該為 「 沙箱 」 評估 Azure 堆疊和開發和測試您的應用程式在非生產環境中使用 hello 開發套件。</span><span class="sxs-lookup"><span data-stu-id="8c596-108">You should use hello development kit as a "sandbox," where you can evaluate Azure Stack, and develop and test your apps in a non-production environment.</span></span> <span data-ttu-id="8c596-109">(如需部署資訊，請參閱 hello [Azure 堆疊開發套件部署](azure-stack-deploy-overview.md)快速入門。)</span><span class="sxs-lookup"><span data-stu-id="8c596-109">(For deployment information, see hello [Azure Stack Development Kit deployment](azure-stack-deploy-overview.md) quickstart.)</span></span>

<span data-ttu-id="8c596-110">就像 Azure 一樣，我們迅速地進行創新。</span><span class="sxs-lookup"><span data-stu-id="8c596-110">Like Azure, we innovate rapidly.</span></span> <span data-ttu-id="8c596-111">我們會定期發行新組建。</span><span class="sxs-lookup"><span data-stu-id="8c596-111">We'll regularly release new builds.</span></span> <span data-ttu-id="8c596-112">當您想 toomove toohello 最新組建時，您必須[重新部署 Azure 堆疊](azure-stack-redeploy.md)。</span><span class="sxs-lookup"><span data-stu-id="8c596-112">When you want toomove toohello latest build, you must [redeploy Azure Stack](azure-stack-redeploy.md).</span></span> <span data-ttu-id="8c596-113">此程序需要的時間，但 hello 好處是您可以試用 hello 最新的功能。</span><span class="sxs-lookup"><span data-stu-id="8c596-113">This process takes time, but hello benefit is that you can try out hello latest features.</span></span> <span data-ttu-id="8c596-114">我們的網站上的 hello 文件會反映最新版本組建 hello。</span><span class="sxs-lookup"><span data-stu-id="8c596-114">hello documentation on our website reflects hello latest release build.</span></span>

## <a name="learn-about-available-services"></a><span data-ttu-id="8c596-115">了解可用的服務</span><span class="sxs-lookup"><span data-stu-id="8c596-115">Learn about available services</span></span>

<span data-ttu-id="8c596-116">您將需要的哪些服務，您可以將可用的 tooyour 使用者感知。</span><span class="sxs-lookup"><span data-stu-id="8c596-116">You'll need an awareness of which services you can make available tooyour users.</span></span> <span data-ttu-id="8c596-117">Azure Stack 支援 Azure 服務的子集。</span><span class="sxs-lookup"><span data-stu-id="8c596-117">Azure Stack supports a subset of Azure services.</span></span> <span data-ttu-id="8c596-118">支援服務 hello 清單將會繼續 tooevolve。</span><span class="sxs-lookup"><span data-stu-id="8c596-118">hello list of supported services will continue tooevolve.</span></span>

<span data-ttu-id="8c596-119">**基礎服務**</span><span class="sxs-lookup"><span data-stu-id="8c596-119">**Foundational services**</span></span>

<span data-ttu-id="8c596-120">根據預設，Azure 堆疊會包含下列 「 基本服務 」 的 hello 當您部署 Azure 堆疊：</span><span class="sxs-lookup"><span data-stu-id="8c596-120">By default, Azure Stack includes hello following "foundational services" when you deploy Azure Stack:</span></span>

- <span data-ttu-id="8c596-121">計算</span><span class="sxs-lookup"><span data-stu-id="8c596-121">Compute</span></span>
- <span data-ttu-id="8c596-122">儲存體</span><span class="sxs-lookup"><span data-stu-id="8c596-122">Storage</span></span>
- <span data-ttu-id="8c596-123">網路</span><span class="sxs-lookup"><span data-stu-id="8c596-123">Networking</span></span>
- <span data-ttu-id="8c596-124">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="8c596-124">Key Vault</span></span>

<span data-ttu-id="8c596-125">利用這些基本服務，您可以提供基礎結構做為服務 (IaaS) tooyour 使用者，以最低組態。</span><span class="sxs-lookup"><span data-stu-id="8c596-125">With these foundational services, you can offer Infrastructure-as-a-Service (IaaS) tooyour users with minimal configuration.</span></span>

<span data-ttu-id="8c596-126">**其他服務**</span><span class="sxs-lookup"><span data-stu-id="8c596-126">**Additional services**</span></span>

<span data-ttu-id="8c596-127">目前，我們支援下列其他平台做為服務 (PaaS) 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c596-127">Currently, we support hello following additional Platform-as-a-Service (PaaS) services:</span></span>

- <span data-ttu-id="8c596-128">App Service</span><span class="sxs-lookup"><span data-stu-id="8c596-128">App Service</span></span>
- <span data-ttu-id="8c596-129">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="8c596-129">Azure Functions</span></span>
- <span data-ttu-id="8c596-130">SQL 和 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="8c596-130">SQL and MySQL databases</span></span>

<span data-ttu-id="8c596-131">這些服務需要其他設定，才能讓可用 tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="8c596-131">These services require additional configuration before you can make them available tooyour users.</span></span> <span data-ttu-id="8c596-132">如需詳細資訊，請參閱 hello 」 教學課程 」 和 hello 文件的 「 如何 tooguides\Offer 服務 」 各節。</span><span class="sxs-lookup"><span data-stu-id="8c596-132">For more information, see hello "Tutorials" and hello "How-tooguides\Offer services" sections of our documentation.</span></span>

<span data-ttu-id="8c596-133">**服務藍圖**</span><span class="sxs-lookup"><span data-stu-id="8c596-133">**Service roadmap**</span></span>

<span data-ttu-id="8c596-134">Azure 堆疊將會繼續 tooadd 支援 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="8c596-134">Azure Stack will continue tooadd support for Azure services.</span></span> <span data-ttu-id="8c596-135">預計的 hello 藍圖，請參閱 hello[混合式應用程式創新，使用 Azure 和 Azure 堆疊](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)白皮書。</span><span class="sxs-lookup"><span data-stu-id="8c596-135">For hello projected roadmap, see hello [Hybrid Application Innovation with Azure and Azure Stack](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409) whitepaper.</span></span> <span data-ttu-id="8c596-136">您也可以監視 hello [Azure 堆疊部落格文章](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview)新宣告。</span><span class="sxs-lookup"><span data-stu-id="8c596-136">You can also monitor hello [Azure Stack blog posts](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview) for new announcements.</span></span>

## <a name="what-tools-do-i-use-toomanage"></a><span data-ttu-id="8c596-137">工具的作用為何使用 toomanage 嗎？</span><span class="sxs-lookup"><span data-stu-id="8c596-137">What tools do I use toomanage?</span></span>
 
<span data-ttu-id="8c596-138">您可以使用 hello[管理員入口網站](azure-stack-manage-portals.md)或 PowerShell toomanage Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="8c596-138">You can use hello [administrator portal](azure-stack-manage-portals.md) or PowerShell toomanage Azure Stack.</span></span> <span data-ttu-id="8c596-139">hello 最簡單方式 toolearn hello 基本概念都是透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8c596-139">hello easiest way toolearn hello basic concepts is through hello portal.</span></span> <span data-ttu-id="8c596-140">如果您想 toouse PowerShell 時，有準備步驟。</span><span class="sxs-lookup"><span data-stu-id="8c596-140">If you want toouse PowerShell, there are preparation steps.</span></span> <span data-ttu-id="8c596-141">您必須[安裝](azure-stack-powershell-install.md) PowerShell、[下載](azure-stack-powershell-download.md)其他模組，並[設定](azure-stack-powershell-configure-admin.md) PowerShell。</span><span class="sxs-lookup"><span data-stu-id="8c596-141">You must [install](azure-stack-powershell-install.md) PowerShell, [download](azure-stack-powershell-download.md) additional modules, and [configure](azure-stack-powershell-configure-admin.md) PowerShell.</span></span>

<span data-ttu-id="8c596-142">Azure Stack 使用 Azure Resource Manager 作為其基礎的部署、管理及組織機制。</span><span class="sxs-lookup"><span data-stu-id="8c596-142">Azure Stack uses Azure Resource Manager as its underlying deployment, management, and organization mechanism.</span></span> <span data-ttu-id="8c596-143">如果您打算 toomanage Azure 堆疊和說明支援使用者，您應該了解有關資源管理員。</span><span class="sxs-lookup"><span data-stu-id="8c596-143">If you're going toomanage Azure Stack and help support users, you should learn about Resource Manager.</span></span> <span data-ttu-id="8c596-144">請參閱 hello[開始使用 Azure 資源管理員](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf)白皮書。</span><span class="sxs-lookup"><span data-stu-id="8c596-144">See hello [Getting Started with Azure Resource Manager](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) whitepaper.</span></span>

## <a name="your-typical-responsibilities"></a><span data-ttu-id="8c596-145">您的一般責任</span><span class="sxs-lookup"><span data-stu-id="8c596-145">Your typical responsibilities</span></span>

<span data-ttu-id="8c596-146">您的使用者想 toouse 服務。</span><span class="sxs-lookup"><span data-stu-id="8c596-146">Your users want toouse services.</span></span> <span data-ttu-id="8c596-147">從其觀點來看，您的主要角色是 toomake 這些服務可用 toothem。</span><span class="sxs-lookup"><span data-stu-id="8c596-147">From their perspective, your main role is toomake these services available toothem.</span></span> <span data-ttu-id="8c596-148">您必須決定哪些服務 toooffer，並藉由建立提供這些服務[配額](azure-stack-setting-quotas.md)，[計劃](azure-stack-create-plan.md)，和[提供](azure-stack-create-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="8c596-148">You must decide which services toooffer, and make those services available by creating [quotas](azure-stack-setting-quotas.md), [plans](azure-stack-create-plan.md), and [offers](azure-stack-create-offer.md).</span></span> 

<span data-ttu-id="8c596-149">您還需要 tooadd 項目 toohello marketplace，例如虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="8c596-149">You'll also need tooadd items toohello marketplace, such as virtual machine images.</span></span> <span data-ttu-id="8c596-150">hello 最簡單方式是太[下載 marketplace 項目從 Azure tooAzure 堆疊](azure-stack-download-azure-marketplace-item.md)。</span><span class="sxs-lookup"><span data-stu-id="8c596-150">hello easiest way is too[download marketplace items from Azure tooAzure Stack](azure-stack-download-azure-marketplace-item.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8c596-151">如果您計劃、 提議和服務，您會想 tootest，您應該使用 hello[使用者入口網站](azure-stack-manage-portals.md); hello 管理員入口網站。</span><span class="sxs-lookup"><span data-stu-id="8c596-151">If you want tootest your plans, offers, and services, you should use hello [user portal](azure-stack-manage-portals.md); not hello administrator portal.</span></span>

<span data-ttu-id="8c596-152">在加法 tooproviding services 中，您必須執行雲端運算子 tookeep Azure 堆疊的 hello 一般的責任啟動且正在執行。</span><span class="sxs-lookup"><span data-stu-id="8c596-152">In addition tooproviding services, you must perform all hello regular  duties of a cloud operator tookeep Azure Stack up and running.</span></span> <span data-ttu-id="8c596-153">這些責任 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="8c596-153">These duties include hello following:</span></span>

- <span data-ttu-id="8c596-154">新增使用者帳戶 (如 [Azure Active Directory](azure-stack-add-new-user-aad.md) 部署或 [Active Directory 同盟服務](azure-stack-add-users-adfs.md)部署)</span><span class="sxs-lookup"><span data-stu-id="8c596-154">Add user accounts (for [Azure Active Directory](azure-stack-add-new-user-aad.md) deployment or for [Active Directory Federation Services](azure-stack-add-users-adfs.md) deployment)</span></span>
- <span data-ttu-id="8c596-155">[指派角色型存取控制 (RBAC) 角色](azure-stack-manage-permissions.md)（這是不受限制的 tooadministrators。）</span><span class="sxs-lookup"><span data-stu-id="8c596-155">[Assign role-based access control (RBAC) roles](azure-stack-manage-permissions.md) (This is not restricted tooadministrators.)</span></span>
- [<span data-ttu-id="8c596-156">監視基礎結構健康情況</span><span class="sxs-lookup"><span data-stu-id="8c596-156">Monitor infrastructure health</span></span>](azure-stack-monitor-health.md)
- <span data-ttu-id="8c596-157">管理[網路](azure-stack-viewing-public-ip-address-consumption.md)和[儲存體](azure-stack-manage-storage-accounts.md)資源</span><span class="sxs-lookup"><span data-stu-id="8c596-157">Manage [network](azure-stack-viewing-public-ip-address-consumption.md) and [storage](azure-stack-manage-storage-accounts.md) resources</span></span>
- <span data-ttu-id="8c596-158">取代故障的硬體</span><span class="sxs-lookup"><span data-stu-id="8c596-158">Replace bad hardware</span></span>

## <a name="what-tootell-your-users"></a><span data-ttu-id="8c596-159">哪些 tootell 您的使用者</span><span class="sxs-lookup"><span data-stu-id="8c596-159">What tootell your users</span></span>

<span data-ttu-id="8c596-160">您將需要您的使用者知道與 toowork services 如何在 Azure 堆疊 tooconnect toohello 開發套件的環境中，以及如何 toolet toosubscribe toooffers。</span><span class="sxs-lookup"><span data-stu-id="8c596-160">You'll need toolet your users know how toowork with services in Azure Stack, how tooconnect toohello development kit environment, and how toosubscribe toooffers.</span></span>

<span data-ttu-id="8c596-161">**了解 Azure 堆疊中 toowork 與服務的方式**</span><span class="sxs-lookup"><span data-stu-id="8c596-161">**Understand how toowork with services in Azure Stack**</span></span>

<span data-ttu-id="8c596-162">在使用服務和 Azure Stack 中的應用程式之前，有些資訊您的使用者必須先了解。</span><span class="sxs-lookup"><span data-stu-id="8c596-162">There's information your users must understand before they use services and build apps in Azure Stack.</span></span> <span data-ttu-id="8c596-163">例如，有特定的 PowerShell 和 API 版本需求。</span><span class="sxs-lookup"><span data-stu-id="8c596-163">For example, there are specific PowerShell and API version requirements.</span></span> <span data-ttu-id="8c596-164">此外，還有 Azure 服務與 hello Azure 堆疊中的對等服務之間的某些功能差異。</span><span class="sxs-lookup"><span data-stu-id="8c596-164">Also, there are some feature deltas between a service in Azure and hello equivalent service in Azure Stack.</span></span> <span data-ttu-id="8c596-165">請確定您的使用者，檢閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="8c596-165">Make sure that your users review hello following articles:</span></span>

- [<span data-ttu-id="8c596-166">關鍵考量：使用 Azure Stack 的服務或組建 Azure Stack 應用程式</span><span class="sxs-lookup"><span data-stu-id="8c596-166">Key considerations: Using services or building apps for Azure Stack</span></span>](azure-stack-considerations.md)
- [<span data-ttu-id="8c596-167">Azure Stack 中虛擬機器的考量</span><span class="sxs-lookup"><span data-stu-id="8c596-167">Considerations for Virtual Machines in Azure Stack</span></span>](azure-stack-vm-considerations.md)
- [<span data-ttu-id="8c596-168">儲存體：差異和考量</span><span class="sxs-lookup"><span data-stu-id="8c596-168">Storage: differences and considerations</span></span>](azure-stack-acs-differences-tp2.md)

<span data-ttu-id="8c596-169">這些文章中的 hello 資訊摘要說明 hello Azure 中的服務與 Azure 堆疊之間的差異。</span><span class="sxs-lookup"><span data-stu-id="8c596-169">hello information in these articles summarizes hello differences between a service in Azure and Azure Stack.</span></span> <span data-ttu-id="8c596-170">它會補充適用於 Azure 服務 hello 全域 Azure 文件中的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="8c596-170">It supplements hello information that's available for an Azure service in hello global Azure documentation.</span></span> 

<span data-ttu-id="8c596-171">**以使用者身分連接 tooAzure 堆疊**</span><span class="sxs-lookup"><span data-stu-id="8c596-171">**Connect tooAzure Stack as a user**</span></span>

<span data-ttu-id="8c596-172">在開發套件環境中，如果使用者沒有遠端桌面存取 toohello 開發套件主應用程式，它們必須設定虛擬私人網路 (VPN) 連線，才能存取 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="8c596-172">In a development kit environment, if a user doesn't have Remote Desktop access toohello development kit host, they must configure a virtual private network (VPN) connection before they can access Azure Stack.</span></span> <span data-ttu-id="8c596-173">請參閱[連接 tooAzure 堆疊](azure-stack-connect-azure-stack.md)。</span><span class="sxs-lookup"><span data-stu-id="8c596-173">See [Connect tooAzure Stack](azure-stack-connect-azure-stack.md).</span></span> 

<span data-ttu-id="8c596-174">您的使用者將如何太想 tooknow[存取 hello 使用者入口網站](azure-stack-manage-portals.md)或如何透過 PowerShell tooconnect。</span><span class="sxs-lookup"><span data-stu-id="8c596-174">Your users will want tooknow how too[access hello user portal ](azure-stack-manage-portals.md) or how tooconnect through PowerShell.</span></span> <span data-ttu-id="8c596-175">如果使用 PowerShell，使用者可能必須 tooregister 資源提供者，才能使用服務。</span><span class="sxs-lookup"><span data-stu-id="8c596-175">If using PowerShell, users may have tooregister resource providers before they can use services.</span></span> <span data-ttu-id="8c596-176">(資源提供者負責管理服務。</span><span class="sxs-lookup"><span data-stu-id="8c596-176">(A resource provider manages a service.</span></span> <span data-ttu-id="8c596-177">例如，網路功能資源提供者的 hello 管理資源，例如虛擬網路、 網路介面和負載平衡器。)他們必須[安裝](azure-stack-powershell-install.md) PowerShell、[下載](azure-stack-powershell-download.md) 其他模組，並[設定](azure-stack-powershell-configure-user.md) PowerShell (其中包含資源提供者註冊)。</span><span class="sxs-lookup"><span data-stu-id="8c596-177">For example, hello networking resource provider manages resources such as virtual networks, network interfaces, and load balancers.) They must [install](azure-stack-powershell-install.md) PowerShell, [download](azure-stack-powershell-download.md) additional modules, and [configure](azure-stack-powershell-configure-user.md) PowerShell (which includes resource provider registration).</span></span>

<span data-ttu-id="8c596-178">**訂閱 tooan 供應項目**</span><span class="sxs-lookup"><span data-stu-id="8c596-178">**Subscribe tooan offer**</span></span>

<span data-ttu-id="8c596-179">使用者可以存取服務之前，它們必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)您已建立雲端操作員。</span><span class="sxs-lookup"><span data-stu-id="8c596-179">Before a user can access services, they must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that you've created as a cloud operator.</span></span>

## <a name="where-tooget-support"></a><span data-ttu-id="8c596-180">其中 tooget 支援</span><span class="sxs-lookup"><span data-stu-id="8c596-180">Where tooget support</span></span>

<span data-ttu-id="8c596-181">Hello Azure 堆疊開發套件，您可以要求支援相關的問題，在 hello [Microsoft 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack)。</span><span class="sxs-lookup"><span data-stu-id="8c596-181">For hello Azure Stack Development Kit, you can ask support-related questions in hello [Microsoft forums](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack).</span></span> <span data-ttu-id="8c596-182">如果您按一下 hello 說明及支援圖示 （問號） 中的 hello 管理員入口網站，hello 右上角，然後按一下**新增支援要求**，這會直接開啟 hello 論壇網站。</span><span class="sxs-lookup"><span data-stu-id="8c596-182">If you click hello Help and support icon (question mark) in hello upper-right corner of hello administrator portal, and then click **New support request**, this opens hello forums site directly.</span></span> <span data-ttu-id="8c596-183">我們會定期留意這些論壇。</span><span class="sxs-lookup"><span data-stu-id="8c596-183">These forums are regularly monitored.</span></span> <span data-ttu-id="8c596-184">Hello 開發套件是評估環境，因為沒有提供透過 Microsoft 客戶支援服務 (CSS) 提供官方支援。</span><span class="sxs-lookup"><span data-stu-id="8c596-184">Because hello development kit is an evaluation environment, there is no official support offered through Microsoft Customer Support Services (CSS).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c596-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c596-185">Next steps</span></span>

- [<span data-ttu-id="8c596-186">Azure Stack 中的區域管理</span><span class="sxs-lookup"><span data-stu-id="8c596-186">Region management in Azure Stack</span></span>](azure-stack-region-management.md)


