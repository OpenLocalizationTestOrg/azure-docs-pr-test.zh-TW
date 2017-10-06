---
title: "aaaInstall 在內部部署資料閘道 |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定內部資料閘道。"
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
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="18fd2-103">安裝及設定內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="18fd2-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="18fd2-104">中的一個或多個 Azure Analysis Services 伺服器 hello 相同時，就需要在內部部署資料閘道區域連接 tooon 內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="18fd2-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="18fd2-105">請參閱深入了解 hello 閘道 toolearn[在內部部署資料閘道](analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="18fd2-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18fd2-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="18fd2-106">Prerequisites</span></span>
<span data-ttu-id="18fd2-107">**最低需求：**</span><span class="sxs-lookup"><span data-stu-id="18fd2-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="18fd2-108">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="18fd2-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="18fd2-109">64 位元版本的 Windows 7 / Windows Server 2008 R2 (或更新版本)</span><span class="sxs-lookup"><span data-stu-id="18fd2-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="18fd2-110">**建議配備：**</span><span class="sxs-lookup"><span data-stu-id="18fd2-110">**Recommended:**</span></span>

* <span data-ttu-id="18fd2-111">8 核心 CPU</span><span class="sxs-lookup"><span data-stu-id="18fd2-111">8 Core CPU</span></span>
* <span data-ttu-id="18fd2-112">8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="18fd2-112">8 GB Memory</span></span>
* <span data-ttu-id="18fd2-113">64 位元版本的 Windows 2012 R2 (或更新版本)</span><span class="sxs-lookup"><span data-stu-id="18fd2-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="18fd2-114">**重要考量︰**</span><span class="sxs-lookup"><span data-stu-id="18fd2-114">**Important considerations:**</span></span>

* <span data-ttu-id="18fd2-115">在安裝期間，向您的閘道註冊 Azure 時，會選取 hello 預設訂用帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="18fd2-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="18fd2-116">您可以選擇不同的區域。</span><span class="sxs-lookup"><span data-stu-id="18fd2-116">You can choose a different region.</span></span> <span data-ttu-id="18fd2-117">如果您有伺服器位於多個區域中，您必須針對每個區域安裝一個閘道。</span><span class="sxs-lookup"><span data-stu-id="18fd2-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="18fd2-118">hello 閘道不能安裝在網域控制站上。</span><span class="sxs-lookup"><span data-stu-id="18fd2-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="18fd2-119">一部電腦只能安裝一個閘道。</span><span class="sxs-lookup"><span data-stu-id="18fd2-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="18fd2-120">資料會保留在並不討論 toosleep 的電腦上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="18fd2-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="18fd2-121">請勿以無線方式連線的 tooyour 網路上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="18fd2-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="18fd2-122">效能會因此降低。</span><span class="sxs-lookup"><span data-stu-id="18fd2-122">Performance can be diminished.</span></span>


## <span data-ttu-id="18fd2-123"><a name="download"></a>下載</span><span class="sxs-lookup"><span data-stu-id="18fd2-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="18fd2-124">下載 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="18fd2-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="18fd2-125"><a name="install"></a>安裝</span><span class="sxs-lookup"><span data-stu-id="18fd2-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="18fd2-126">執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="18fd2-126">Run setup.</span></span>

2. <span data-ttu-id="18fd2-127">選取的位置，接受 hello 條款，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="18fd2-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![安裝位置和授權條款](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="18fd2-129">選取 [內部部署資料閘道 ()]。</span><span class="sxs-lookup"><span data-stu-id="18fd2-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="18fd2-130">Azure Analysis Services 不支援個人模式。</span><span class="sxs-lookup"><span data-stu-id="18fd2-130">Azure Analysis Services does not support personal mode.</span></span>

   ![選擇閘道的類型](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="18fd2-132">輸入帳戶 toosign tooAzure 中。</span><span class="sxs-lookup"><span data-stu-id="18fd2-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="18fd2-133">hello 帳戶必須是租用戶的 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="18fd2-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="18fd2-134">此帳戶用於 hello 閘道系統管理員。</span><span class="sxs-lookup"><span data-stu-id="18fd2-134">This account is used for hello gateway administrator.</span></span> 

   ![輸入帳戶 toosign tooAzure 中](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="18fd2-136">如果您使用網域帳戶登入，就會在 Azure AD 中對應 tooyour 組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="18fd2-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="18fd2-137">您的組織帳戶將用於 hello hello 閘道系統管理員。</span><span class="sxs-lookup"><span data-stu-id="18fd2-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="18fd2-138"><a name="register"></a>註冊</span><span class="sxs-lookup"><span data-stu-id="18fd2-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="18fd2-139">在順序 toocreate 閘道資源在 Azure 中，您必須註冊您安裝閘道器雲端服務的 hello 與 hello 本機執行個體。</span><span class="sxs-lookup"><span data-stu-id="18fd2-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="18fd2-140">選取 [在這部電腦上註冊新的閘道]。</span><span class="sxs-lookup"><span data-stu-id="18fd2-140">Select **Register a new gateway on this computer**.</span></span>

    ![註冊](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="18fd2-142">輸入您的閘道名稱和復原金鑰。</span><span class="sxs-lookup"><span data-stu-id="18fd2-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="18fd2-143">根據預設，hello 閘道會使用您的訂用帳戶預設區域。</span><span class="sxs-lookup"><span data-stu-id="18fd2-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="18fd2-144">如果您需要 tooselect 不同的區域，選取**變更區域**。</span><span class="sxs-lookup"><span data-stu-id="18fd2-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![註冊](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="18fd2-146"><a name="create-resource"></a>建立 Azure 閘道資源</span><span class="sxs-lookup"><span data-stu-id="18fd2-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="18fd2-147">在您安裝並註冊您的閘道之後，您會需要您 Azure 訂用帳戶中 toocreate 閘道資源。</span><span class="sxs-lookup"><span data-stu-id="18fd2-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="18fd2-148">登入以 hello tooAzure 相同註冊 hello 閘道時所使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="18fd2-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="18fd2-149">在 Azure 入口網站中，按一下 [建立新服務] > [企業整合] > [內部部署資料閘道] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="18fd2-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![建立閘道資源](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="18fd2-151">在 [建立連線閘道] 中，輸入下列設定：</span><span class="sxs-lookup"><span data-stu-id="18fd2-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="18fd2-152">**名稱**：輸入閘道資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="18fd2-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="18fd2-153">**訂用帳戶**： 選取 hello Azure 訂用帳戶 tooassociate 與閘道資源。</span><span class="sxs-lookup"><span data-stu-id="18fd2-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="18fd2-154">此訂用帳戶應為 hello 您的伺服器位於相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="18fd2-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="18fd2-155">hello 預設訂用帳戶根據 hello 用 toosign 中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="18fd2-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="18fd2-156">**資源群組**：建立資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="18fd2-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="18fd2-157">**位置**： 您註冊您的閘道器中選取 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="18fd2-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="18fd2-158">**安裝名稱**： 如果尚未選取閘道安裝，選取 hello 閘道註冊。</span><span class="sxs-lookup"><span data-stu-id="18fd2-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="18fd2-159">完成之後，請按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="18fd2-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="18fd2-160"><a name="connect-servers"></a>連接伺服器 toohello 閘道資源</span><span class="sxs-lookup"><span data-stu-id="18fd2-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="18fd2-161">在 Azure Analysis Services 伺服器概觀中，按一下 [內部部署資料閘道]。</span><span class="sxs-lookup"><span data-stu-id="18fd2-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![連接伺服器 toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="18fd2-163">在**挑選內部資料閘道 tooconnect**，選取您的閘道資源，然後按一下**選取的連線的閘道**。</span><span class="sxs-lookup"><span data-stu-id="18fd2-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![連接伺服器 toogateway 資源](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="18fd2-165">如果您的閘道器不會出現在 hello 清單中，您的伺服器可能不是處於 hello 與 hello 註冊 hello 閘道時，您指定的區域相同的區域。</span><span class="sxs-lookup"><span data-stu-id="18fd2-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="18fd2-166">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="18fd2-166">That's it.</span></span> <span data-ttu-id="18fd2-167">如果您需要 tooopen 連接埠，或執行進行疑難排解，是確定 toocheck 出[在內部部署資料閘道](analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="18fd2-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18fd2-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18fd2-168">Next steps</span></span>
* [<span data-ttu-id="18fd2-169"> Analysis Services</span><span class="sxs-lookup"><span data-stu-id="18fd2-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="18fd2-170">從 Azure Analysis Services 取得資料</span><span class="sxs-lookup"><span data-stu-id="18fd2-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
