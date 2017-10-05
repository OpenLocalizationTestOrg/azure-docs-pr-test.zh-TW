---
title: "Azure Active Directory Domain Services：更新 Azure 虛擬網路的 DNS 設定 | Microsoft Docs"
description: "開始使用 Azure Active Directory Domain Services"
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
ms.openlocfilehash: c704ee189072ce8ed196d1ef0a23edd528a10025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="fe302-103">啟用 Azure Active Directory Domain Services (預覽)</span><span class="sxs-lookup"><span data-stu-id="fe302-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="fe302-104">工作 4：更新 Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="fe302-104">Task 4: update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="fe302-105">在先前的組態工作中，您已成功為目錄啟用 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="fe302-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="fe302-106">下一個工作是確保虛擬網路內的電腦可以連線並取用這些服務。</span><span class="sxs-lookup"><span data-stu-id="fe302-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="fe302-107">在本文中，您可以更新虛擬網路的 DNS 伺服器設定，以指向虛擬網路上可以使用 Azure Active Directory Domain Services 的兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fe302-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

<span data-ttu-id="fe302-108">若要為已啟用 Azure Active Directory Domain Services 的虛擬網路更新 DNS 伺服器設定，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="fe302-108">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="fe302-109">[概觀] 索引標籤會列出在完整佈建受控網域之後所要執行的一組**必要設定步驟**。</span><span class="sxs-lookup"><span data-stu-id="fe302-109">The **Overview** tab lists a set of **Required configuration steps** to be performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="fe302-110">第一個設定步驟是**更新虛擬網路的 DNS 伺服器設定**。</span><span class="sxs-lookup"><span data-stu-id="fe302-110">The first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services - 完全佈建後的 [概觀] 索引標籤](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="fe302-112">完整佈建您的網域時，此圖格會顯示兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fe302-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="fe302-113">每個 IP 位址都代表受控網域的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="fe302-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="fe302-114">若要將第一個 IP 位址複製到剪貼簿，請按一下其旁邊的複製按鈕。</span><span class="sxs-lookup"><span data-stu-id="fe302-114">To copy the first IP address to clipboard, click the copy button next to it.</span></span> <span data-ttu-id="fe302-115">然後按一下 [設定 DNS 伺服器] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fe302-115">Then click the **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="fe302-116">將第一個 IP 位址貼上到 [DNS 伺服器] 刀鋒視窗的 [新增 DNS 伺服器] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="fe302-116">Paste the first IP address into the **Add DNS server** textbox in the **DNS servers** blade.</span></span> <span data-ttu-id="fe302-117">水平捲動至左邊以複製第二個 IP 位址，並將它貼到 [新增 DNS 伺服器] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="fe302-117">Scroll horizontally to the left to copy the second IP address and paste it into the **Add DNS server** textbox.</span></span>

    ![Domain Services - 更新 DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="fe302-119">當您完成虛擬網路的 DNS 伺服器更新時，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="fe302-119">Click **Save** when you are done to update the DNS servers for the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="fe302-120">網路中的虛擬機器只會在重新啟動後取得新的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="fe302-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="fe302-121">如果您希望它們立即取得更新後的 DNS 設定，請透過入口網站、PowerShell 或 CLI 觸發重新啟動。</span><span class="sxs-lookup"><span data-stu-id="fe302-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="fe302-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe302-122">Next step</span></span>
[<span data-ttu-id="fe302-123">工作 5：啟用 Azure Active Directory Domain Services 的密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="fe302-123">Task 5: enable password synchronization to Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
