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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="c0a23-103">啟用 Azure Active Directory Domain Services (預覽)</span><span class="sxs-lookup"><span data-stu-id="c0a23-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="c0a23-104">工作 4： 更新 hello Azure 虛擬網路的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="c0a23-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="c0a23-105">在 hello 之前設定工作，您已成功啟用 Azure Active Directory 網域服務目錄。</span><span class="sxs-lookup"><span data-stu-id="c0a23-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="c0a23-106">hello 下一個工作是 tooensure hello 虛擬網路內的電腦可以連線，並使用這些服務。</span><span class="sxs-lookup"><span data-stu-id="c0a23-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="c0a23-107">在本文中，您可以更新 hello DNS 伺服器設定您虛擬網路 toopoint toohello 兩個 IP 位址的 Azure Active Directory 網域服務位於 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c0a23-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="c0a23-108">tooupdate hello DNS 伺服器設定為已啟用 Azure Active Directory 網域服務，完成下列步驟的 hello hello 虛擬網路的：</span><span class="sxs-lookup"><span data-stu-id="c0a23-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="c0a23-109">hello**概觀**索引標籤會列出一組**所需的設定步驟**toobe 執行之後完整佈建受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="c0a23-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="c0a23-110">hello 第一個組態步驟是**更新 DNS 伺服器設定為您的虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="c0a23-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services - 完全佈建後的 [概觀] 索引標籤](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="c0a23-112">完整佈建您的網域時，此圖格會顯示兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c0a23-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="c0a23-113">每個 IP 位址都代表受控網域的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="c0a23-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="c0a23-114">toocopy hello 第一個 IP 位址 tooclipboard，請按一下 hello 複製 按鈕的下一個 tooit。</span><span class="sxs-lookup"><span data-stu-id="c0a23-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="c0a23-115">然後按一下 [hello**設定 DNS 伺服器**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0a23-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="c0a23-116">第一個 IP 位址 hello 貼入 hello**新增 DNS 伺服器**hello 中的文字方塊中**DNS 伺服器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c0a23-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="c0a23-117">水平捲動 toohello 剩餘 toocopy hello 第二個 IP 位址，並將它貼到 hello**新增 DNS 伺服器**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c0a23-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Domain Services - 更新 DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="c0a23-119">按一下**儲存**當您完成 tooupdate hello hello 虛擬網路的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c0a23-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="c0a23-120">Hello 網路中的虛擬機器重新啟動之後，只能取得 hello 新的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="c0a23-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="c0a23-121">如果您需要它們 tooget hello 更新 DNS 設定以立即開始，會觸發重新啟動依 hello 入口網站、 PowerShell 或 hello CLI。</span><span class="sxs-lookup"><span data-stu-id="c0a23-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="c0a23-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0a23-122">Next step</span></span>
[<span data-ttu-id="c0a23-123">工作 5： 啟用密碼同步處理 tooAzure Active Directory 網域服務</span><span class="sxs-lookup"><span data-stu-id="c0a23-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
