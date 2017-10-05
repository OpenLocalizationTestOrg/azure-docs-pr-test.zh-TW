---
title: "針對已加入 Azure AD 網域之 Windows 下層用戶端電腦的自動註冊進行疑難排解 | Microsoft Docs"
description: "針對已加入 Azure AD 網域之 Windows 下層用戶端電腦的自動註冊進行疑難排解。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="b49d6-103">針對已加入網域之 Windows 下層用戶端電腦的自動註冊 Azure AD 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b49d6-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="b49d6-104">本主題僅適用於下列用戶端：</span><span class="sxs-lookup"><span data-stu-id="b49d6-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="b49d6-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="b49d6-105">Windows 7</span></span> 
- <span data-ttu-id="b49d6-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b49d6-106">Windows 8.1</span></span> 
- <span data-ttu-id="b49d6-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="b49d6-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="b49d6-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b49d6-108">Windows Server 2012</span></span> 
- <span data-ttu-id="b49d6-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b49d6-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="b49d6-110">針對 Windows 10 或 Windows Server 2016，請參閱[針對已加入網域之電腦的自動註冊 Azure AD 進行疑難排解 – Windows 10 和 Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="b49d6-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="b49d6-111">本主題假設您已經依照[如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊](active-directory-device-registration-get-started.md)所述，設定讓已加入網域的裝置自動註冊。</span><span class="sxs-lookup"><span data-stu-id="b49d6-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="b49d6-112">本主題提供有關如何解決潛在問題的疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="b49d6-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="b49d6-113">以下是獲得成功結果的一些注意事項：</span><span class="sxs-lookup"><span data-stu-id="b49d6-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="b49d6-114">在 Azure AD 上註冊這些用戶端時是依據個別使用者/裝置。</span><span class="sxs-lookup"><span data-stu-id="b49d6-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="b49d6-115">舉例來說：如果 jdoe 和 jharnett 登入此裝置，在 [使用者資訊] 索引標籤中就會為這每位使用者建立個別的註冊 (DeviceID)。</span><span class="sxs-lookup"><span data-stu-id="b49d6-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="b49d6-116">預設是設定為在登入或鎖定/解除鎖定時嘗試註冊這些用戶端，而且可能會有 5 分鐘的延遲，這是使用「工作排程器」工作來觸發。</span><span class="sxs-lookup"><span data-stu-id="b49d6-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="b49d6-117">重新安裝作業系統或手動取消註冊再重新註冊時，可能會在 Azure AD 上建立新的註冊，而將導致在 Azure 入口網站中 [使用者資訊] 索引標籤底下有多個項目。</span><span class="sxs-lookup"><span data-stu-id="b49d6-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="b49d6-118">步驟 1：擷取註冊狀態</span><span class="sxs-lookup"><span data-stu-id="b49d6-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="b49d6-119">**確認註冊狀態：**</span><span class="sxs-lookup"><span data-stu-id="b49d6-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="b49d6-120">以系統管理員身分開啟命令提示字元</span><span class="sxs-lookup"><span data-stu-id="b49d6-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="b49d6-121">輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="b49d6-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="b49d6-122">此命令會顯示一個對話方塊，可提供您有關加入狀態的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b49d6-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="b49d6-124">步驟 2：評估註冊狀態</span><span class="sxs-lookup"><span data-stu-id="b49d6-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="b49d6-125">如果未成功加入，對話方塊會提供有關所發生問題的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b49d6-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="b49d6-126">**最常見的問題包括：**</span><span class="sxs-lookup"><span data-stu-id="b49d6-126">**The most common issues are:**</span></span>

- <span data-ttu-id="b49d6-127">AD FS 或 Azure AD 設定不正確</span><span class="sxs-lookup"><span data-stu-id="b49d6-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="b49d6-129">您不是以網域使用者身分登入</span><span class="sxs-lookup"><span data-stu-id="b49d6-129">You are not signed on as a domain user</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="b49d6-131">已達到配額限制</span><span class="sxs-lookup"><span data-stu-id="b49d6-131">A quota has been reached</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="b49d6-133">服務沒有回應</span><span class="sxs-lookup"><span data-stu-id="b49d6-133">The service is not responding</span></span> 

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="b49d6-135">您也可以在事件記錄檔的 [應用程式及服務記錄檔] > [Microsoft-Workplace Join] 底下找到狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="b49d6-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="b49d6-136">**註冊失敗的最常見原因包括︰**</span><span class="sxs-lookup"><span data-stu-id="b49d6-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="b49d6-137">您的電腦不在組織的內部網路上，或不在可連線到內部部署 AD 網域控制站的 VPN 上。</span><span class="sxs-lookup"><span data-stu-id="b49d6-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="b49d6-138">您是使用本機電腦帳戶來登入您的電腦。</span><span class="sxs-lookup"><span data-stu-id="b49d6-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="b49d6-139">服務組態問題：</span><span class="sxs-lookup"><span data-stu-id="b49d6-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="b49d6-140">同盟伺服器已設定為支援 **WIAORMULTIAUTHN**。</span><span class="sxs-lookup"><span data-stu-id="b49d6-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="b49d6-141">沒有「服務連接點」物件指向電腦所屬 AD 樹系之 Azure AD 中已驗證的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="b49d6-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="b49d6-142">使用者已達到裝置限制。</span><span class="sxs-lookup"><span data-stu-id="b49d6-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="b49d6-143">請參閱＜開始使用 Azure Active Directory 裝置註冊＞。</span><span class="sxs-lookup"><span data-stu-id="b49d6-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b49d6-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b49d6-144">Next steps</span></span>

<span data-ttu-id="b49d6-145">如需詳細資訊，請參閱[自動裝置註冊常見問題集](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="b49d6-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
