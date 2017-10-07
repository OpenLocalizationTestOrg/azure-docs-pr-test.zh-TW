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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="606a5-103">啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）</span><span class="sxs-lookup"><span data-stu-id="606a5-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="606a5-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="606a5-104">Before you begin</span></span>
<span data-ttu-id="606a5-105">請參閱太[Azure Active Directory 網域服務的網路功能考量](active-directory-ds-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="606a5-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="606a5-106">工作 2：設定網路設定</span><span class="sxs-lookup"><span data-stu-id="606a5-106">Task 2: configure network settings</span></span>
<span data-ttu-id="606a5-107">hello 下一項組態工作，而且 toocreate Azure 虛擬網路內的專用子網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="606a5-108">您可在虛擬網路內的這個子網路中啟用 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="606a5-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="606a5-109">您也可以挑選現有的虛擬網路，並建立 hello 專用子網路內。</span><span class="sxs-lookup"><span data-stu-id="606a5-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="606a5-110">按一下**虛擬網路**tooselect 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="606a5-111">在 hello**選擇虛擬網路**刀鋒視窗中，您會看到所有現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="606a5-112">您會看到只 hello 屬於 toohello 資源群組和 Azure 位置 hello 上已選取虛擬網路**基本概念**精靈頁面。</span><span class="sxs-lookup"><span data-stu-id="606a5-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="606a5-113">選擇已啟用 Azure AD 網域服務的 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="606a5-114">按一下**建立新**，如果您偏好 toocreate 新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="606a5-115">強烈建議針對 Azure AD Domain Services 使用專用子網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="606a5-116">如果您挑選現有的虛擬網路，[建立專用子網路使用 hello 虛擬網路的延伸模組](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)然後選擇 子網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![挑選虛擬網路](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="606a5-118">按一下**子網路**toopick hello 這個虛擬網路，在內哪些 tooenable 新受管理網域中的專用子網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="606a5-119">在 hello**建立子網路**刀鋒視窗中，指定 hello 子網路名稱，然後按一下**確定**完成。</span><span class="sxs-lookup"><span data-stu-id="606a5-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="606a5-120">例如，建立子網路與 hello 名稱 'DomainServices'，因此可方便的其他系統管理員 toounderstand hello 子網路內部署的內容。</span><span class="sxs-lookup"><span data-stu-id="606a5-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![挑選 hello 虛擬網路內的子網路](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="606a5-122">**選取子網路的指導方針**</span><span class="sxs-lookup"><span data-stu-id="606a5-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="606a5-123">針對 Azure AD Domain Services 使用專用子網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="606a5-124">不會部署任何其他虛擬機器 toothis 子網路。</span><span class="sxs-lookup"><span data-stu-id="606a5-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="606a5-125">此設定可讓您 tooconfigure 網路安全性群組 (Nsg) 為您的工作負載/虛擬機器而不會中斷您受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="606a5-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="606a5-126">如需詳細資訊，請參閱 [Azure Active Directory Domain Services 的網路考量](active-directory-ds-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="606a5-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="606a5-127">請勿選取部署 Azure AD 網域服務的 hello 閘道子網路，因為它不是支援的組態。</span><span class="sxs-lookup"><span data-stu-id="606a5-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="606a5-128">請確定您已選取該 hello 子網路有足夠可用的位址空間至少 3-5 可用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="606a5-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="606a5-129">當您完成之後時，按一下  **確定**上 toohello toomove **Administrator 群組**hello 精靈頁面。</span><span class="sxs-lookup"><span data-stu-id="606a5-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="606a5-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="606a5-130">Next step</span></span>
[<span data-ttu-id="606a5-131">工作 3：設定系統管理群組並啟用 Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="606a5-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
