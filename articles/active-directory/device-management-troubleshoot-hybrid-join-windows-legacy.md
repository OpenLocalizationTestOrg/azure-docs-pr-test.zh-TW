---
title: "aaaTroubleshooting 混合 Azure Active Directory 加入下層裝置 |Microsoft 文件"
description: "針對已加入混合式 Azure Active Directory 的下層裝置進行疑難排解。"
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="dce0f-103">針對已加入混合式 Azure Active Directory 的下層裝置進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="dce0f-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="dce0f-104">本主題是適用的唯一 toohello 下列裝置：</span><span class="sxs-lookup"><span data-stu-id="dce0f-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="dce0f-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="dce0f-105">Windows 7</span></span> 
- <span data-ttu-id="dce0f-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="dce0f-106">Windows 8.1</span></span> 
- <span data-ttu-id="dce0f-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="dce0f-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="dce0f-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="dce0f-108">Windows Server 2012</span></span> 
- <span data-ttu-id="dce0f-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="dce0f-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="dce0f-110">對於 Windows 10 或 Windows Server 2016，請參閱[針對已加入混合式 Azure Active Directory 的 Windows 10 和 Windows Server 2016 裝置進行疑難排解](device-management-troubleshoot-hybrid-join-windows-current.md)。</span><span class="sxs-lookup"><span data-stu-id="dce0f-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="dce0f-111">本主題假設您有[設定混合式 Azure Active Directory 加入裝置](device-management-hybrid-azuread-joined-devices-setup.md)toosupport hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="dce0f-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="dce0f-112">裝置型條件式存取</span><span class="sxs-lookup"><span data-stu-id="dce0f-112">Device-based conditional access</span></span>

- [<span data-ttu-id="dce0f-113">設定的企業漫遊</span><span class="sxs-lookup"><span data-stu-id="dce0f-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="dce0f-114">Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="dce0f-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="dce0f-115">此主題提供疑難排解指引 tooresolve 可能問題的方式。</span><span class="sxs-lookup"><span data-stu-id="dce0f-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="dce0f-116">**您應該知道的事情：**</span><span class="sxs-lookup"><span data-stu-id="dce0f-116">**What you should know:**</span></span> 

- <span data-ttu-id="dce0f-117">hello 的每個使用者的裝置數目上限是裝置為中心。</span><span class="sxs-lookup"><span data-stu-id="dce0f-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="dce0f-118">例如，如果*jdoe*和*jharnett*登入 tooa 裝置建立個別登錄 (DeviceID) 為每個在 hello**使用者**資訊 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dce0f-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="dce0f-119">hello 初始註冊 / 聯結的裝置是已設定的 tooperform 次嘗試登入或鎖定 / 解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="dce0f-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="dce0f-120">工作排程器工作可能會觸發 5 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="dce0f-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="dce0f-121">Hello 作業系統或手動重新安裝取消登錄 」 以及 「 重新註冊可能會在 Azure AD 上建立新的註冊和 hello 使用者資訊 索引標籤底下的多個項目會導致 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="dce0f-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="dce0f-122">步驟 1： 擷取 hello 註冊狀態</span><span class="sxs-lookup"><span data-stu-id="dce0f-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="dce0f-123">**tooverify hello 註冊狀態：**</span><span class="sxs-lookup"><span data-stu-id="dce0f-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="dce0f-124">以系統管理員身分開啟 hello 命令提示字元</span><span class="sxs-lookup"><span data-stu-id="dce0f-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="dce0f-125">輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="dce0f-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="dce0f-126">此命令會顯示對話方塊，讓您提供更多詳細 hello 聯結狀態。</span><span class="sxs-lookup"><span data-stu-id="dce0f-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="dce0f-128">步驟 2： 評估 hello 混合 Azure AD 的聯結狀態</span><span class="sxs-lookup"><span data-stu-id="dce0f-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="dce0f-129">如果未成功加入 hello 混合 Azure AD，hello 對話方塊會提供您 hello 問題已經發生的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dce0f-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="dce0f-130">**hello 最常見的問題是：**</span><span class="sxs-lookup"><span data-stu-id="dce0f-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="dce0f-131">AD FS 或 Azure AD 設定不正確</span><span class="sxs-lookup"><span data-stu-id="dce0f-131">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="dce0f-133">您不是以網域使用者身分登入</span><span class="sxs-lookup"><span data-stu-id="dce0f-133">You are not signed on as a domain user</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="dce0f-135">已達到配額限制</span><span class="sxs-lookup"><span data-stu-id="dce0f-135">A quota has been reached</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="dce0f-137">hello 服務沒有回應</span><span class="sxs-lookup"><span data-stu-id="dce0f-137">hello service is not responding</span></span> 

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="dce0f-139">您也可以在 hello 事件記錄檔中找到 hello 狀態資訊**應用程式和服務 Log\Microsoft 地點**。</span><span class="sxs-lookup"><span data-stu-id="dce0f-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="dce0f-140">**失敗的混合式 Azure AD 聯結 hello 最常見原因包括：**</span><span class="sxs-lookup"><span data-stu-id="dce0f-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="dce0f-141">您的電腦不在 hello 組織內部網路或 VPN 連線 tooan 沒有內部部署 AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="dce0f-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="dce0f-142">您登入 tooyour 電腦與本機電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="dce0f-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="dce0f-143">服務組態問題：</span><span class="sxs-lookup"><span data-stu-id="dce0f-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="dce0f-144">hello 同盟伺服器已設定的 toosupport **WIAORMULTIAUTHN**。</span><span class="sxs-lookup"><span data-stu-id="dce0f-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="dce0f-145">沒有在 Azure AD 中指向 tooyour 驗證的網域名稱，其中 hello 電腦屬於 hello AD 樹系中的服務連接點物件。</span><span class="sxs-lookup"><span data-stu-id="dce0f-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="dce0f-146">使用者已達到 hello 的裝置。</span><span class="sxs-lookup"><span data-stu-id="dce0f-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dce0f-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dce0f-147">Next steps</span></span>

<span data-ttu-id="dce0f-148">如有問題，請參閱 hello[裝置管理常見問題集](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="dce0f-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
