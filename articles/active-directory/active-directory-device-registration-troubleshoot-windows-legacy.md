---
title: "aaaTroubleshooting hello 自動登錄，Azure AD 網域的電腦加入 Windows 下層用戶端 |Microsoft 文件"
description: "疑難排解 hello 自動註冊的 Azure AD 網域加入 Windows 下層用戶端的電腦。"
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="c2ab2-103">疑難排解自動登錄的網域加入 Windows 下層用戶端電腦 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="c2ab2-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="c2ab2-104">本主題僅適用於下列用戶端的唯一 toohello:</span><span class="sxs-lookup"><span data-stu-id="c2ab2-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="c2ab2-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c2ab2-105">Windows 7</span></span> 
- <span data-ttu-id="c2ab2-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c2ab2-106">Windows 8.1</span></span> 
- <span data-ttu-id="c2ab2-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c2ab2-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="c2ab2-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c2ab2-108">Windows Server 2012</span></span> 
- <span data-ttu-id="c2ab2-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c2ab2-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="c2ab2-110">針對 Windows 10 或 Windows Server 2016，請參閱[疑難排解自動登錄的網域加入電腦 tooAzure AD – Windows 10 和 Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="c2ab2-111">本主題假設您已設定自動註冊已加入網域的裝置如中所述述[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-device-registration-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="c2ab2-112">此主題提供疑難排解指引 tooresolve 可能問題的方式。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="c2ab2-113">成功的結果的一些事項 toonote:</span><span class="sxs-lookup"><span data-stu-id="c2ab2-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="c2ab2-114">在 Azure AD 上註冊這些用戶端時是依據個別使用者/裝置。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="c2ab2-115">例如： 如果 jdoe 和 jharnett 登入 toothis 裝置，這些使用者在 hello 使用者資訊] 索引標籤中的每個建立個別登錄 (DeviceID)。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="c2ab2-116">這些用戶端 hello 現成的註冊作業就會在登入或鎖定/解除鎖定設定的 tootry 和可能有 5 分鐘的延遲，這觸發使用工作排程器工作。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="c2ab2-117">重新安裝，hello 作業系統或手動取消註冊及重新登錄可能會在 Azure AD 上建立新的註冊，並會導致多個項目 hello 使用者資訊] 索引標籤底下 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="c2ab2-118">步驟 1： 擷取 hello 註冊狀態</span><span class="sxs-lookup"><span data-stu-id="c2ab2-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="c2ab2-119">**tooverify hello 註冊狀態：**</span><span class="sxs-lookup"><span data-stu-id="c2ab2-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="c2ab2-120">以系統管理員身分開啟 hello 命令提示字元</span><span class="sxs-lookup"><span data-stu-id="c2ab2-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="c2ab2-121">輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="c2ab2-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="c2ab2-122">此命令會顯示對話方塊，讓您提供更多詳細 hello 聯結狀態。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="c2ab2-124">步驟 2： 評估 hello 登錄狀態</span><span class="sxs-lookup"><span data-stu-id="c2ab2-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="c2ab2-125">如果 hello 聯結不成功，hello 對話方塊會提供您 hello 問題已經發生的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="c2ab2-126">**hello 最常見的問題是：**</span><span class="sxs-lookup"><span data-stu-id="c2ab2-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="c2ab2-127">AD FS 或 Azure AD 設定不正確</span><span class="sxs-lookup"><span data-stu-id="c2ab2-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="c2ab2-129">您不是以網域使用者身分登入</span><span class="sxs-lookup"><span data-stu-id="c2ab2-129">You are not signed on as a domain user</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="c2ab2-131">已達到配額限制</span><span class="sxs-lookup"><span data-stu-id="c2ab2-131">A quota has been reached</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="c2ab2-133">hello 服務沒有回應</span><span class="sxs-lookup"><span data-stu-id="c2ab2-133">hello service is not responding</span></span> 

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="c2ab2-135">您也可以在 hello 事件記錄檔中找到 hello 狀態資訊**應用程式和服務 Log\Microsoft 地點**。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="c2ab2-136">**hello 失敗註冊最常見的原因包括：**</span><span class="sxs-lookup"><span data-stu-id="c2ab2-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="c2ab2-137">您的電腦不在 hello 組織內部網路或 VPN 連線 tooan 沒有內部部署 AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="c2ab2-138">您登入 tooyour 電腦與本機電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="c2ab2-139">服務組態問題：</span><span class="sxs-lookup"><span data-stu-id="c2ab2-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="c2ab2-140">hello 同盟伺服器已設定的 toosupport **WIAORMULTIAUTHN**。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="c2ab2-141">沒有在 Azure AD 中指向 tooyour 驗證的網域名稱，其中 hello 電腦屬於 hello AD 樹系中的服務連接點物件。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="c2ab2-142">使用者已達到 hello 的裝置。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="c2ab2-143">請參閱＜開始使用 Azure Active Directory 裝置註冊＞。</span><span class="sxs-lookup"><span data-stu-id="c2ab2-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2ab2-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2ab2-144">Next steps</span></span>

<span data-ttu-id="c2ab2-145">如需詳細資訊，請參閱 hello[自動裝置註冊常見問題集](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c2ab2-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
