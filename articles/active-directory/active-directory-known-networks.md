---
title: "hello Azure 傳統入口網站中的 aaaKnown 網路 |Microsoft 文件"
description: "藉由設定已知的網路，您可以避免必須包含在 hello 從多個地理位置登入 」 和 「 從具有可疑活動報告的 IP 位址登入您組織所擁有的 IP 位址。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="5a304-103">已知的網路</span><span class="sxs-lookup"><span data-stu-id="5a304-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a304-104">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="5a304-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="5a304-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5a304-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="5a304-106">您可以使用 Azure Active Directory 的存取和使用方式報表 toogain 掌握 hello 完整性與安全性貴組織的目錄。</span><span class="sxs-lookup"><span data-stu-id="5a304-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="5a304-107">利用此資訊，目錄管理員更能夠判斷可能發生安全性風險的地方，讓他們做充裕的計畫 toomitigate 這些風險。</span><span class="sxs-lookup"><span data-stu-id="5a304-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="5a304-108">它有可能在 hello"*從多個地理位置登入*"和"*來自 IP 位址的登入具有可疑活動*」 報告不正確的旗標實際擁有的 IP 位址您組織。</span><span class="sxs-lookup"><span data-stu-id="5a304-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="5a304-109">比方說，這可以發生在下列情形：</span><span class="sxs-lookup"><span data-stu-id="5a304-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="5a304-110">波士頓辦公室中的使用者登入遠端 tooyour 資料中心 San Francisco 觸發程序 hello 「 從多個地理位置登入 」 報告中</span><span class="sxs-lookup"><span data-stu-id="5a304-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="5a304-111">您組織的使用者嘗試 toosign 入數次以不正確的密碼觸發程序 hello 「 從具有可疑活動的 IP 位址的登入 」 報告</span><span class="sxs-lookup"><span data-stu-id="5a304-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="5a304-112">tooprevent 這種情況下，從產生誤導安全性報告，您應該加入已知的 IP 位址範圍 toohello 清單貴組織的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5a304-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="5a304-113">tooadd 貴組織的公用 IP 位址範圍，請執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a304-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="5a304-114">登入 toohello [Azure 管理入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="5a304-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="5a304-115">在 hello 左窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="5a304-115">In hello left pane, click **Active Directory**.</span></span> 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="5a304-117">在 hello**目錄**索引標籤上，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="5a304-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="5a304-118">在 hello 最上層顯示 hello 功能表上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="5a304-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="5a304-120">Hello 設定索引標籤上，前往 太**您組織公用 IP 位址範圍**</span><span class="sxs-lookup"><span data-stu-id="5a304-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="5a304-122">按一下 新增已知的 IP 位址範圍 。</span><span class="sxs-lookup"><span data-stu-id="5a304-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="5a304-123">在 hello 對話方塊出現，新增您的位址範圍，然後按一下 hello 核取記號按鈕完成時。</span><span class="sxs-lookup"><span data-stu-id="5a304-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="5a304-125">**其他資源：**</span><span class="sxs-lookup"><span data-stu-id="5a304-125">**Additional resources:**</span></span>

* [<span data-ttu-id="5a304-126">檢視存取和使用情況報告</span><span class="sxs-lookup"><span data-stu-id="5a304-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="5a304-127">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="5a304-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="5a304-128">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="5a304-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

