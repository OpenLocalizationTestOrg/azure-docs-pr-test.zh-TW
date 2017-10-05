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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="b90f2-103">使用 Azure 入口網站 (預覽) 啟用 Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b90f2-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="b90f2-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="b90f2-104">Before you begin</span></span>
<span data-ttu-id="b90f2-105">請參閱 [Azure Active Directory Domain Services 的網路考量](active-directory-ds-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="b90f2-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="b90f2-106">工作 2：設定網路設定</span><span class="sxs-lookup"><span data-stu-id="b90f2-106">Task 2: configure network settings</span></span>
<span data-ttu-id="b90f2-107">下一個設定工作是建立 Azure 虛擬網路與其中的專用子網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="b90f2-108">您可在虛擬網路內的這個子網路中啟用 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="b90f2-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="b90f2-109">您也可以挑選現有的虛擬網路，並且建立其中的專用子網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="b90f2-110">按一下 [虛擬網路] 以選取虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-110">Click **Virtual network** to select a virtual network.</span></span>
2. <span data-ttu-id="b90f2-111">在 [選擇虛擬網路] 刀鋒視窗中，您會看到所有現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-111">On the **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="b90f2-112">您只會看到隸屬於您在 [基本] 精靈分頁上選取之資源群組和 Azure 位置的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-112">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>

3. <span data-ttu-id="b90f2-113">選擇應該在其中啟用 Azure AD Domain Services 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-113">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="b90f2-114">如果您想要建立新的虛擬網路，請按一下 [新建]。</span><span class="sxs-lookup"><span data-stu-id="b90f2-114">Click **Create new**, if you prefer to create a new virtual network.</span></span> <span data-ttu-id="b90f2-115">強烈建議針對 Azure AD Domain Services 使用專用子網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="b90f2-116">如果您挑選現有的虛擬網路，[使用虛擬網路延伸模組建立專用子網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)，然後挑選該子網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-116">If you pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![挑選虛擬網路](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="b90f2-118">按一下 [子網路] 以挑選此虛擬網路中的專用子網路，在其中啟用新的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="b90f2-118">Click **Subnet** to pick the dedicated subnet in this virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="b90f2-119">在 [建立子網路] 刀鋒視窗中，指定子網路的名稱，然後在您完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b90f2-119">In the **Create subnet** blade, specify a name for the subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="b90f2-120">例如，建立具有名稱 'DomainServices' 的子網路，讓其他系統管理員容易了解子網路內部署的內容。</span><span class="sxs-lookup"><span data-stu-id="b90f2-120">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span>

    ![挑選虛擬網路內的子網路](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="b90f2-122">**選取子網路的指導方針**</span><span class="sxs-lookup"><span data-stu-id="b90f2-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="b90f2-123">針對 Azure AD Domain Services 使用專用子網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="b90f2-124">不要將任何其他虛擬機器部署到此子網路。</span><span class="sxs-lookup"><span data-stu-id="b90f2-124">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="b90f2-125">此設定可讓您為工作負載/虛擬機器設定網路安全性群組 (NSG)，而不會中斷受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="b90f2-125">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="b90f2-126">如需詳細資訊，請參閱 [Azure Active Directory Domain Services 的網路考量](active-directory-ds-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="b90f2-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="b90f2-127">請勿選取閘道子網路來部署 Azure AD Domain Services，因為它不是支援的設定。</span><span class="sxs-lookup"><span data-stu-id="b90f2-127">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="b90f2-128">請確定您選取的子網路具有足夠的可用位址空間，至少 3-5 個可用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b90f2-128">Ensure that the subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="b90f2-129">完成時，按一下 [確定] 以繼續前往精靈的 [Administrator 群組] 分頁。</span><span class="sxs-lookup"><span data-stu-id="b90f2-129">When you are done, click **OK** to move on to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="b90f2-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b90f2-130">Next step</span></span>
[<span data-ttu-id="b90f2-131">工作 3：設定系統管理群組並啟用 Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="b90f2-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
