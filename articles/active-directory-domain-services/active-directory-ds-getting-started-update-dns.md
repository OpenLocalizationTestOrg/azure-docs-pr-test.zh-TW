---
title: "Azure Active Directory Domain Services：更新 Azure 虛擬網路的 DNS 設定 | Microsoft Docs"
description: "開始使用 Azure Active Directory 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 8bee2a25f196d645b27f30f21305b1550e44e07a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="3b07a-103">更新 Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="3b07a-103">Update DNS settings for the Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="3b07a-104">工作 4 - 更新 Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="3b07a-104">Task 4: Update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="3b07a-105">在先前的組態工作中，您已成功為目錄啟用 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="3b07a-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="3b07a-106">下一個工作是確保虛擬網路內的電腦可以連線並取用這些服務。</span><span class="sxs-lookup"><span data-stu-id="3b07a-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="3b07a-107">在本文中，您可以更新虛擬網路的 DNS 伺服器設定，以指向虛擬網路上可以使用 Azure Active Directory Domain Services 的兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3b07a-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="3b07a-108">在您已啟用目錄的 Azure Active Directory Domain Services 之後，請記下在您目錄的 [設定] 索引標籤上顯示之 Azure Active Directory Domain Services 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3b07a-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="3b07a-109">若要為已啟用 Azure Active Directory Domain Services 的虛擬網路更新 DNS 伺服器設定，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="3b07a-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="3b07a-110">前往 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3b07a-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3b07a-111">在左側窗格中，選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="3b07a-111">In the left pane, select **Networks**.</span></span>  
    <span data-ttu-id="3b07a-112">隨即開啟 [網路] 視窗。</span><span class="sxs-lookup"><span data-stu-id="3b07a-112">The **Networks** window opens.</span></span>

    ![虛擬網路視窗](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="3b07a-114">在 [虛擬網路] 索引標籤上，選取已啟用 Azure Active Directory Domain Services 的虛擬網路，以檢視其內容。</span><span class="sxs-lookup"><span data-stu-id="3b07a-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span></span>
4. <span data-ttu-id="3b07a-115">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3b07a-115">Click the **Configure** tab.</span></span>

    ![虛擬網路視窗](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="3b07a-117">已在 [DNS 伺服器] 區段中，輸入您目錄的 [設定] 索引標籤之 [網域服務] 中所顯示的兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3b07a-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="3b07a-118">若要儲存此虛擬網路的 DNS 伺服器設定，請在頁面底部之工作窗格上按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="3b07a-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span></span>

   ![更新虛擬網路的 DNS 伺服器設定](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="3b07a-120">網路中的虛擬機器只會在重新啟動後取得新的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="3b07a-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="3b07a-121">如果您希望它們立即取得更新後的 DNS 設定，請透過入口網站、PowerShell 或 CLI 觸發重新啟動。</span><span class="sxs-lookup"><span data-stu-id="3b07a-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3b07a-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b07a-122">Next steps</span></span>
<span data-ttu-id="3b07a-123">工作 5：[啟用 Azure Active Directory Domain Services 的密碼同步處理](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="3b07a-123">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
