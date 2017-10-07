---
title: "Azure Active Directory 網域服務： 更新 hello Azure 虛擬網路的 DNS 設定 |Microsoft 文件"
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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="3e938-103">更新 hello Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="3e938-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="3e938-104">工作 4： 更新 hello Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="3e938-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="3e938-105">在 hello 之前設定工作，您已成功啟用 Azure Active Directory 網域服務目錄。</span><span class="sxs-lookup"><span data-stu-id="3e938-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="3e938-106">hello 下一個工作是 tooensure hello 虛擬網路內的電腦可以連線，並使用這些服務。</span><span class="sxs-lookup"><span data-stu-id="3e938-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="3e938-107">在本文中，您可以更新 hello DNS 伺服器設定您虛擬網路 toopoint toohello 兩個 IP 位址的 Azure Active Directory 網域服務位於 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="3e938-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="3e938-108">啟用 Azure Active Directory 網域服務的 hello 目錄之後，請注意 hello IP 位址的 Azure Active Directory 網域服務，會顯示在 hello**設定**您目錄的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3e938-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="3e938-109">tooupdate hello DNS 伺服器設定為已啟用 Azure Active Directory 網域服務，完成下列步驟的 hello hello 虛擬網路的：</span><span class="sxs-lookup"><span data-stu-id="3e938-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="3e938-110">移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3e938-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3e938-111">Hello 左窗格中，選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="3e938-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="3e938-112">hello**網路**視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="3e938-112">hello **Networks** window opens.</span></span>

    ![虛擬網路視窗](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="3e938-114">在 hello**虛擬網路**索引標籤，選取 hello 虛擬網路中您已啟用 Azure Active Directory 網域服務 tooview 其屬性。</span><span class="sxs-lookup"><span data-stu-id="3e938-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="3e938-115">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3e938-115">Click hello **Configure** tab.</span></span>

    ![虛擬網路視窗](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="3e938-117">在 [hello **DNS 伺服器**區段中，輸入這兩個 hello hello 中所顯示的 IP 位址**網域服務**hello] 區段**設定**您目錄的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3e938-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="3e938-118">toosave hello DNS 伺服器設定為此虛擬網路，在 hello hello 視窗底部的 hello 工作窗格中按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="3e938-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![更新 hello hello 虛擬網路的 DNS 伺服器設定](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="3e938-120">Hello 網路中的虛擬機器重新啟動之後，只能取得 hello 新的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="3e938-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="3e938-121">如果您需要它們 tooget hello 更新 DNS 設定以立即開始，會觸發重新啟動依 hello 入口網站、 PowerShell 或 hello CLI。</span><span class="sxs-lookup"><span data-stu-id="3e938-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3e938-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e938-122">Next steps</span></span>
<span data-ttu-id="3e938-123">工作 5:[啟用密碼同步處理 tooAzure Active Directory 網域服務](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="3e938-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
