---
title: "Azure Active Directory Domain Services：建立或選取虛擬網路 | Microsoft Docs"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="dad2d-103">為 Azure Active Directory Domain Services 建立或選取虛擬網路</span><span class="sxs-lookup"><span data-stu-id="dad2d-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="dad2d-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="dad2d-104">Before you begin</span></span>
<span data-ttu-id="dad2d-105">請參閱太[Azure Active Directory 網域服務的網路功能考量](active-directory-ds-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="dad2d-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="dad2d-106">工作 2：建立 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="dad2d-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="dad2d-107">hello 下一項組態工作，而且 toocreate Azure 虛擬網路內的子網路。</span><span class="sxs-lookup"><span data-stu-id="dad2d-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="dad2d-108">您可在虛擬網路內的這個子網路中啟用 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="dad2d-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="dad2d-109">如果您有現有的虛擬網路，您會希望 toouse，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="dad2d-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="dad2d-110">請確定該 hello Azure 虛擬網路，您建立或選擇 [與 Azure Active Directory 網域服務 toouse 所屬 tooan 支援的 Azure Active Directory 網域服務的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="dad2d-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="dad2d-111">tooascertain hello Azure Active Directory 網域服務可用的 Azure 區域，請參閱[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)。</span><span class="sxs-lookup"><span data-stu-id="dad2d-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="dad2d-112">請注意，當您在後續的設定步驟中啟用 Azure Active Directory 網域服務時選取 hello 右虛擬網路的 hello 虛擬網路 tooensure hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="dad2d-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="dad2d-113">toocreate 想 tooenable Azure Active Directory 網域服務，Azure 虛擬網路，請遵循這些設定指示：</span><span class="sxs-lookup"><span data-stu-id="dad2d-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="dad2d-114">移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="dad2d-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="dad2d-115">Hello 左窗格中，選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="dad2d-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="dad2d-116">![網路節點](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="dad2d-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="dad2d-117">hello**虛擬網路**視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="dad2d-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="dad2d-118">在 [hello 工作窗格在 hello hello 視窗的底部，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="dad2d-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![虛擬網路視窗](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="dad2d-120">按一下 [網絡服務]，然後選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="dad2d-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![虛擬網路 - 快速建立](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="dad2d-122">按一下 [虛擬網路，toocreate**快速建立**。</span><span class="sxs-lookup"><span data-stu-id="dad2d-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="dad2d-123">指定**名稱**為虛擬網路，然後考慮 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="dad2d-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="dad2d-124">您可以選擇 tooconfigure**位址空間**或**最大 VM 計數**對此網路。</span><span class="sxs-lookup"><span data-stu-id="dad2d-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="dad2d-125">您可以保留 hello **DNS 伺服器**設定為**無**現在。</span><span class="sxs-lookup"><span data-stu-id="dad2d-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="dad2d-126">啟用 Azure Active Directory 網域服務之後，您可以更新 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="dad2d-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="dad2d-127">在 [hello**位置**下拉式清單中，選取支援的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="dad2d-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="dad2d-128">tooascertain hello Azure Active Directory 網域服務可用的 Azure 區域，請參閱[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)。</span><span class="sxs-lookup"><span data-stu-id="dad2d-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="dad2d-129">toocreate 虛擬網路，按一下 [**建立虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="dad2d-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![為 Azure Active Directory Domain Services 建立虛擬網路](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="dad2d-131">您已建立虛擬網路之後，選取 hello hello 虛擬網路名稱，然後按一下 [hello**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dad2d-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![建立子網路](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="dad2d-133">在下**虛擬網路位址空間**，按一下 [**加入子網路**，然後指定子網路與 hello 名稱**AaddsSubnet**。</span><span class="sxs-lookup"><span data-stu-id="dad2d-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![為 Azure Active Directory Domain Services 建立子網路](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="dad2d-135">toocreate hello 子網路中，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="dad2d-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="dad2d-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dad2d-136">Next step</span></span>
[<span data-ttu-id="dad2d-137">工作 3︰啟用 Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="dad2d-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
