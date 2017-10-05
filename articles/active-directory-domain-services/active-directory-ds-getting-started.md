---
title: "Azure Active Directory Domain Services：開始使用 | Microsoft Docs"
description: "使用 Azure 入口網站 (預覽) 啟用 Azure Active Directory Domain Services"
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
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="fc16a-103">使用 Azure 入口網站 (預覽) 啟用 Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="fc16a-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>
<span data-ttu-id="fc16a-104">本文說明如何使用 Azure 入口網站啟用 Azure Active Directory Domain Services (Azure AD DS)。</span><span class="sxs-lookup"><span data-stu-id="fc16a-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


<span data-ttu-id="fc16a-105">若要啟動 [啟用 Azure AD Domain Services] 精靈，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fc16a-105">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="fc16a-106">移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="fc16a-106">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fc16a-107">在左窗格中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fc16a-107">In the left pane, click on **New**.</span></span>
3. <span data-ttu-id="fc16a-108">在 [新增] 刀鋒視窗中，將「網域服務」輸入到搜尋列。</span><span class="sxs-lookup"><span data-stu-id="fc16a-108">In the **New** blade, type **Domain Services** into the search bar.</span></span>

    ![搜尋網域服務](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="fc16a-110">按一下以從搜尋建議清單中選取 [Azure AD Domain Services]。</span><span class="sxs-lookup"><span data-stu-id="fc16a-110">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="fc16a-111">在 [Azure AD Domain Services] 刀鋒視窗中，按一下 [建立] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fc16a-111">On the **Azure AD Domain Services** blade, click the **Create** button.</span></span>

    ![網域服務刀鋒視窗](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="fc16a-113">[啟用 Azure AD Domain Services] 精靈隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="fc16a-113">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="fc16a-114">工作 1：設定基本設定</span><span class="sxs-lookup"><span data-stu-id="fc16a-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="fc16a-115">在精靈的 [基本] 分頁中，您可以指定受管理的網域的 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="fc16a-115">In the **Basics** page of the wizard, you can specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="fc16a-116">您也可以選擇應該部署受管理的網域的資源群組和 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="fc16a-116">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![設定基本](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="fc16a-118">為受管理的網域選擇 [DNS 網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="fc16a-118">Choose the **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="fc16a-119">根據預設，將會指定目錄的預設網域名稱 (具有 **.onmicrosoft.com** 尾碼)。</span><span class="sxs-lookup"><span data-stu-id="fc16a-119">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="fc16a-120">您也可以輸入自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="fc16a-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="fc16a-121">在此範例中，自訂網域名稱是 contoso100.com。</span><span class="sxs-lookup"><span data-stu-id="fc16a-121">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="fc16a-122">指定網域名稱的前置詞 (例如，contoso100.com 網域名稱中的 contoso100) 必須包含 15 個以內的字元。</span><span class="sxs-lookup"><span data-stu-id="fc16a-122">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="fc16a-123">您無法使用超過 15 個字元的前置詞來建立受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="fc16a-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="fc16a-124">確定虛擬網路中還沒有您為受管理網域選擇的 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="fc16a-124">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="fc16a-125">具體來說，請檢查是否有下列情況︰</span><span class="sxs-lookup"><span data-stu-id="fc16a-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="fc16a-126">您在虛擬網路上已有包含相同 DNS 網域名稱的網域。</span><span class="sxs-lookup"><span data-stu-id="fc16a-126">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="fc16a-127">您打算啟用受管理的網域的虛擬網路具有與內部部署網路的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="fc16a-127">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="fc16a-128">在此案例中，確定您在內部部署網路上沒有使用相同 DNS 網域名稱的網域。</span><span class="sxs-lookup"><span data-stu-id="fc16a-128">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="fc16a-129">您在虛擬網路上已有具有該名稱的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fc16a-129">You have an existing cloud service with that name on the virtual network.</span></span>

3. <span data-ttu-id="fc16a-130">選擇 [虛擬網路的類型]。</span><span class="sxs-lookup"><span data-stu-id="fc16a-130">Choose the **type of virtual network**.</span></span> <span data-ttu-id="fc16a-131">根據預設，會選取 **Resource Manager** 虛擬網路類型。</span><span class="sxs-lookup"><span data-stu-id="fc16a-131">By default, the **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="fc16a-132">建議所有新建立的受管理網域使用這種類型的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fc16a-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="fc16a-133">選取您要在其中建立受管理的網域的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fc16a-133">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

5. <span data-ttu-id="fc16a-134">選取受管理的網域應該隸屬的**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="fc16a-134">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="fc16a-135">您可以選擇**新建**或**使用現有**選項，以選取資源群組。</span><span class="sxs-lookup"><span data-stu-id="fc16a-135">You can choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

6. <span data-ttu-id="fc16a-136">選擇應該在其中建立受管理的網域的 Azure**位置**。</span><span class="sxs-lookup"><span data-stu-id="fc16a-136">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="fc16a-137">在精靈的 [網路] 分頁上，您只會看到屬於您所選取之位置的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fc16a-137">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

7. <span data-ttu-id="fc16a-138">完成時，按一下 [確定] 以繼續前往精靈的 [網路] 分頁。</span><span class="sxs-lookup"><span data-stu-id="fc16a-138">When you are done, click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="fc16a-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc16a-139">Next step</span></span>
[<span data-ttu-id="fc16a-140">工作 2：設定網路基本設定</span><span class="sxs-lookup"><span data-stu-id="fc16a-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
