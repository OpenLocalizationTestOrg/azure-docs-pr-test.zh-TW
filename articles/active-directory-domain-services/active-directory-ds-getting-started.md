---
title: "Azure Active Directory Domain Services：開始使用 | Microsoft Docs"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="4c15a-103">啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）</span><span class="sxs-lookup"><span data-stu-id="4c15a-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="4c15a-104">本文將說明如何 tooenable Azure Active Directory 網域服務 (Azure AD DS) 使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4c15a-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="4c15a-105">toolaunch hello**啟用 Azure AD 網域服務** 精靈，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c15a-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="4c15a-106">移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4c15a-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c15a-107">在 [hello] 左窗格中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="4c15a-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="4c15a-108">在 hello**新增**刀鋒視窗中，輸入**網域服務**hello 搜尋列。</span><span class="sxs-lookup"><span data-stu-id="4c15a-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![搜尋網域服務](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="4c15a-110">按一下 tooselect **Azure AD 網域服務**hello 清單中的搜尋建議。</span><span class="sxs-lookup"><span data-stu-id="4c15a-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="4c15a-111">在 [hello **Azure AD 網域服務**刀鋒視窗中，按一下 hello**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4c15a-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![網域服務刀鋒視窗](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="4c15a-113">hello**啟用 Azure AD 網域服務**精靈啟動。</span><span class="sxs-lookup"><span data-stu-id="4c15a-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="4c15a-114">工作 1：設定基本設定</span><span class="sxs-lookup"><span data-stu-id="4c15a-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="4c15a-115">在 hello**基本概念**頁面的 hello 精靈，您可以指定 hello hello 受管理的網域的 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4c15a-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="4c15a-116">您也可以選擇 hello 資源群組和 Azure 位置 toowhich hello 受管理的網域，應該先部署。</span><span class="sxs-lookup"><span data-stu-id="4c15a-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![設定基本](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="4c15a-118">選擇 hello **DNS 網域名稱**的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="4c15a-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="4c15a-119">hello 目錄 hello 預設網域名稱 (與**。 onmicrosoft.com**後置詞) 的預設指定。</span><span class="sxs-lookup"><span data-stu-id="4c15a-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="4c15a-120">您也可以輸入自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4c15a-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="4c15a-121">在此範例中，hello 自訂網域名稱是*contoso100.com*。</span><span class="sxs-lookup"><span data-stu-id="4c15a-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="4c15a-122">hello 前置詞指定的網域名稱 (例如， *contoso100*在 hello *contoso100.com*網域名稱) 必須包含 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="4c15a-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="4c15a-123">您無法使用超過 15 個字元的前置詞來建立受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="4c15a-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="4c15a-124">請確定您已選擇 hello 受管理的網域不存在 hello 虛擬網路中的 hello DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4c15a-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="4c15a-125">具體來說，請檢查是否有下列情況︰</span><span class="sxs-lookup"><span data-stu-id="4c15a-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="4c15a-126">您已經擁有網域以 hello 相同 hello 虛擬網路上的 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4c15a-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="4c15a-127">hello 您計劃 tooenable hello 受管理的網域的虛擬網路已與您在內部部署網路的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="4c15a-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="4c15a-128">在此案例中，請確定您不需要以 hello 網域相同的 DNS 網域名稱，在內部部署網路上。</span><span class="sxs-lookup"><span data-stu-id="4c15a-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="4c15a-129">Hello 虛擬網路上有該名稱與現有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="4c15a-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="4c15a-130">選擇 hello**的虛擬網路類型**。</span><span class="sxs-lookup"><span data-stu-id="4c15a-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="4c15a-131">根據預設，hello**資源管理員**所選取的虛擬網路類型。</span><span class="sxs-lookup"><span data-stu-id="4c15a-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="4c15a-132">建議所有新建立的受管理網域使用這種類型的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4c15a-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="4c15a-133">選取 hello Azure**訂用帳戶**中您想要 toocreate hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="4c15a-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="4c15a-134">選取 hello**資源群組**應該屬於 toowhich hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="4c15a-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="4c15a-135">您可以選擇其中一個 hello**建立新**或**使用現有**選項 tooselect hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="4c15a-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="4c15a-136">選擇 hello Azure**位置**應在哪個 hello 建立受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="4c15a-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="4c15a-137">在 hello**網路**頁面的 hello 精靈，請參閱唯一的虛擬網路屬於 toohello 您選取的位置。</span><span class="sxs-lookup"><span data-stu-id="4c15a-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="4c15a-138">當您完成之後時，按一下 **確定**上 toohello toomove**網路**hello 精靈頁面。</span><span class="sxs-lookup"><span data-stu-id="4c15a-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="4c15a-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c15a-139">Next step</span></span>
[<span data-ttu-id="4c15a-140">工作 2：設定網路基本設定</span><span class="sxs-lookup"><span data-stu-id="4c15a-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
