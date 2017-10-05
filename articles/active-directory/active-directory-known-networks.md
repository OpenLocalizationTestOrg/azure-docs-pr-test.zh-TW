---
title: "Azure 傳統入口網站中的已知網路 | Microsoft Docs"
description: "藉由設定已知的網路，您可以避免貴組織擁有的 IP 位址包含在「從多個地理區域登入」和「從具有可疑活動的 IP 位址登入」報告中。"
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="e799d-103">已知的網路</span><span class="sxs-lookup"><span data-stu-id="e799d-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e799d-104">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="e799d-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="e799d-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e799d-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="e799d-106">您可以使用 Azure Active Directory 的存取和使用情況報告來了解貴組織的目錄完整性和安全性。</span><span class="sxs-lookup"><span data-stu-id="e799d-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="e799d-107">利用此資訊，目錄管理員更能夠判斷可能發生安全性風險的位置，以便適當地規劃來減輕這些風險。</span><span class="sxs-lookup"><span data-stu-id="e799d-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="e799d-108">「從多個地理區域登入」和「從具有可疑活動的 IP 位址登入」可能會不正確地報告貴組織實際擁有的旗標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e799d-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="e799d-109">比方說，這可以發生在下列情形：</span><span class="sxs-lookup"><span data-stu-id="e799d-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="e799d-110">在波士頓辦公室的使用者已從遠端登入您在舊金山的資料中心，觸發了「從多個地理區域登入」的報告</span><span class="sxs-lookup"><span data-stu-id="e799d-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="e799d-111">貴組織的使用者多次嘗試以不正確的密碼登入，觸發了「從具有可疑活動的 IP 位址登入」的報告</span><span class="sxs-lookup"><span data-stu-id="e799d-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="e799d-112">若要避免這些情況下產生誤導的安全性報告，您應該在貴組織的公用 IP 位址清單中新增已知的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="e799d-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="e799d-113">若要新增貴組織的公用 IP 位址範圍，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e799d-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="e799d-114">登入 [Azure 管理入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="e799d-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="e799d-115">在左窗格中，按一下 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="e799d-115">In the left pane, click **Active Directory**.</span></span> 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="e799d-117">在 [目錄]  索引標籤上，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="e799d-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="e799d-118">在頂端的功能表中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="e799d-118">In the menu on the top, click **Configure**.</span></span> 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="e799d-120">在 [組態] 索引標籤上，移至 [貴組織公用 IP 位址範圍]</span><span class="sxs-lookup"><span data-stu-id="e799d-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="e799d-122">按一下 新增已知的 IP 位址範圍 。</span><span class="sxs-lookup"><span data-stu-id="e799d-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="e799d-123">在出現的對話方塊中新增位址範圍，然後在完成時按一下核取按鈕。</span><span class="sxs-lookup"><span data-stu-id="e799d-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="e799d-125">**其他資源：**</span><span class="sxs-lookup"><span data-stu-id="e799d-125">**Additional resources:**</span></span>

* [<span data-ttu-id="e799d-126">檢視存取和使用情況報告</span><span class="sxs-lookup"><span data-stu-id="e799d-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="e799d-127">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="e799d-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="e799d-128">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="e799d-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

