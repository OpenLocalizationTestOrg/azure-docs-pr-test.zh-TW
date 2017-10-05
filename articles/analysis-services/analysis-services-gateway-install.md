---
title: "安裝內部部署資料閘道 | Microsoft Docs"
description: "了解如何安裝及設定內部部署資料閘道。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: 6ef296fb98478be9240f0231c8ad39cd2a0af995
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="0bfa9-103">安裝及設定內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="0bfa9-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="0bfa9-104">如果相同區域中有一或多部 Analysis Services 伺服器連線到內部部署資料來源，則需要一個內部部署閘道。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in the same region connect to on-premises data sources.</span></span> <span data-ttu-id="0bfa9-105">若要深入了解閘道，請參閱[內部部署資料閘道](analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-105">To learn more about the gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bfa9-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="0bfa9-106">Prerequisites</span></span>
<span data-ttu-id="0bfa9-107">**最低需求：**</span><span class="sxs-lookup"><span data-stu-id="0bfa9-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="0bfa9-108">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="0bfa9-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="0bfa9-109">64 位元版本的 Windows 7 / Windows Server 2008 R2 (或更新版本)</span><span class="sxs-lookup"><span data-stu-id="0bfa9-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="0bfa9-110">**建議配備：**</span><span class="sxs-lookup"><span data-stu-id="0bfa9-110">**Recommended:**</span></span>

* <span data-ttu-id="0bfa9-111">8 核心 CPU</span><span class="sxs-lookup"><span data-stu-id="0bfa9-111">8 Core CPU</span></span>
* <span data-ttu-id="0bfa9-112">8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="0bfa9-112">8 GB Memory</span></span>
* <span data-ttu-id="0bfa9-113">64 位元版本的 Windows 2012 R2 (或更新版本)</span><span class="sxs-lookup"><span data-stu-id="0bfa9-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="0bfa9-114">**重要考量︰**</span><span class="sxs-lookup"><span data-stu-id="0bfa9-114">**Important considerations:**</span></span>

* <span data-ttu-id="0bfa9-115">在設定期間，向 Azure 註冊您的閘道時，系統會選取您訂用帳戶的預設區域。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-115">During setup, when registering your gateway with Azure, the default region for your subscription is selected.</span></span> <span data-ttu-id="0bfa9-116">您可以選擇不同的區域。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-116">You can choose a different region.</span></span> <span data-ttu-id="0bfa9-117">如果您有伺服器位於多個區域中，您必須針對每個區域安裝一個閘道。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="0bfa9-118">閘道無法安裝在網域控制站上。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-118">The gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="0bfa9-119">一部電腦只能安裝一個閘道。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="0bfa9-120">請在電源維持開啟且不會進入睡眠狀態的電腦上安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-120">Install the gateway on a computer that remains on and does not go to sleep.</span></span>
* <span data-ttu-id="0bfa9-121">請勿將閘道安裝於採用無線網路的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-121">Do not install the gateway on a computer wirelessly connected to your network.</span></span> <span data-ttu-id="0bfa9-122">效能會因此降低。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-122">Performance can be diminished.</span></span>


## <span data-ttu-id="0bfa9-123"><a name="download"></a>下載</span><span class="sxs-lookup"><span data-stu-id="0bfa9-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="0bfa9-124">下載閘道</span><span class="sxs-lookup"><span data-stu-id="0bfa9-124">Download the gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="0bfa9-125"><a name="install"></a>安裝</span><span class="sxs-lookup"><span data-stu-id="0bfa9-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="0bfa9-126">執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-126">Run setup.</span></span>

2. <span data-ttu-id="0bfa9-127">選取位置，接受條款，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-127">Select a location, accept the terms, and then click **Install**.</span></span>

   ![安裝位置和授權條款](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="0bfa9-129">選取 [內部部署資料閘道 ()]。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="0bfa9-130">Azure Analysis Services 不支援個人模式。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-130">Azure Analysis Services does not support personal mode.</span></span>

   ![選擇閘道的類型](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="0bfa9-132">輸入用來登入 Azure 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-132">Enter an account to sign in to Azure.</span></span> <span data-ttu-id="0bfa9-133">此帳戶必須位於租用戶的 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-133">The account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="0bfa9-134">此帳戶用於閘道管理員。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-134">This account is used for the gateway administrator.</span></span> 

   ![輸入用來登入 Azure 的帳戶](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="0bfa9-136">如果您使用網域帳戶進行登入，該帳戶將會對應到 Azure AD 中您的組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-136">If you sign in with a domain account, it will be mapped to your organizational account in Azure AD.</span></span> <span data-ttu-id="0bfa9-137">您的組織帳戶將作為閘道管理員使用。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-137">Your organizational account will be used as the the gateway administrator.</span></span>

## <span data-ttu-id="0bfa9-138"><a name="register"></a>註冊</span><span class="sxs-lookup"><span data-stu-id="0bfa9-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="0bfa9-139">若要在 Azure 中建立閘道資源，您必須向閘道雲端服務註冊您安裝的本機執行個體。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-139">In order to create a gateway resource in Azure, you must register the local instance you installed with the Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="0bfa9-140">選取 [在這部電腦上註冊新的閘道]。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-140">Select **Register a new gateway on this computer**.</span></span>

    ![註冊](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="0bfa9-142">輸入您的閘道名稱和復原金鑰。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="0bfa9-143">根據預設，閘道會使用您訂用帳戶的預設區域。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-143">By default, the gateway uses your subscription's default region.</span></span> <span data-ttu-id="0bfa9-144">如果您需要選取不同的區域，請選取 [變更區域]。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-144">If you need to select a different region, select **Change Region**.</span></span>

   ![註冊](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="0bfa9-146"><a name="create-resource"></a>建立 Azure 閘道資源</span><span class="sxs-lookup"><span data-stu-id="0bfa9-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="0bfa9-147">在您安裝並註冊閘道之後，您需要在您的 Azure 訂用帳戶中建立閘道資源。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-147">After you've installed and registered your gateway, you need to create a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="0bfa9-148">使用您用於註冊閘道的相同帳戶登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-148">Sign in to Azure with the same account you used when registering the gateway.</span></span>

1. <span data-ttu-id="0bfa9-149">在 Azure 入口網站中，按一下 [建立新服務] > [企業整合] > [內部部署資料閘道] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![建立閘道資源](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="0bfa9-151">在 [建立連線閘道] 中，輸入下列設定：</span><span class="sxs-lookup"><span data-stu-id="0bfa9-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="0bfa9-152">**名稱**：輸入閘道資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="0bfa9-153">**訂用帳戶**︰選取要與閘道資源關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-153">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="0bfa9-154">此訂用帳戶應該是您的伺服器所在的相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-154">This subscription should be the same subscription your servers are in.</span></span>
   
      <span data-ttu-id="0bfa9-155">預設的訂用帳戶會由您用來登入的 Azure 帳戶來決定。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-155">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="0bfa9-156">**資源群組**：建立資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="0bfa9-157">**位置**：選取您註冊閘道的區域。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-157">**Location**: Select the region you registered your gateway in.</span></span>

    * <span data-ttu-id="0bfa9-158">**安裝名稱**︰如果您的閘道安裝還不是選取狀態，請選取已註冊的閘道。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-158">**Installation Name**: If your gateway installation isn't already selected, select the gateway registered.</span></span> 

    <span data-ttu-id="0bfa9-159">完成之後，請按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="0bfa9-160"><a name="connect-servers"></a>將伺服器連線到閘道資源</span><span class="sxs-lookup"><span data-stu-id="0bfa9-160"><a name="connect-servers"></a>Connect servers to the gateway resource</span></span>

1. <span data-ttu-id="0bfa9-161">在 Azure Analysis Services 伺服器概觀中，按一下 [內部部署資料閘道]。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![將伺服器連線至閘道](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="0bfa9-163">在 [挑選要連線的內部部署資料閘道] 中，選取您的閘道資源，然後按一下 [連線選取的閘道]。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-163">In **Pick an On-Premises Data Gateway to connect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![將伺服器連線至閘道資源](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="0bfa9-165">如果您的閘道並未出現在清單中，您的伺服器可能不在註冊閘道時所指定的相同區域中。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-165">If your gateway does not appear in the list, your server is likely not in the same region as the region you specified when registering the gateway.</span></span> 

<span data-ttu-id="0bfa9-166">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-166">That's it.</span></span> <span data-ttu-id="0bfa9-167">如果您需要開啟連接埠，或進行疑難排解，請務必簽出[內部部署資料閘道](analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="0bfa9-167">If you need to open ports or do any troubleshooting, be sure to check out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bfa9-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0bfa9-168">Next steps</span></span>
* [<span data-ttu-id="0bfa9-169"> Analysis Services</span><span class="sxs-lookup"><span data-stu-id="0bfa9-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="0bfa9-170">從 Azure Analysis Services 取得資料</span><span class="sxs-lookup"><span data-stu-id="0bfa9-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
