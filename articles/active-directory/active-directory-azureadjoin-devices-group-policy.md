---
title: "適用於 Windows 10 的 aaaConnect 已加入網域裝置 tooAzure AD 發生 |Microsoft 文件"
description: "說明如何系統管理員可以設定群組原則 tooenable 裝置 toobe 已加入網域的 toohello 企業網路。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="3dfe5-103">連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗</span><span class="sxs-lookup"><span data-stu-id="3dfe5-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="3dfe5-104">網域聯結是 hello 傳統方式組織已連接的裝置 hello 過去 15 年及更多的工作。</span><span class="sxs-lookup"><span data-stu-id="3dfe5-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="3dfe5-105">必須啟用該使用者 toosign tootheir 裝置中的使用 Windows Server Active Directory (Active Directory) 工作或學校帳戶，並允許的 IT toofully 管理這些裝置。</span><span class="sxs-lookup"><span data-stu-id="3dfe5-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="3dfe5-106">組織通常依賴映像方法 tooprovision 裝置 toousers 和通常使用 System Center Configuration Manager (SCCM) 或群組原則 toomanage 它們。</span><span class="sxs-lookup"><span data-stu-id="3dfe5-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="3dfe5-107">在 Windows 10 中的網域加入為您提供 hello 連接裝置 tooAzure Active Directory (Azure AD) 之後，下列優點：</span><span class="sxs-lookup"><span data-stu-id="3dfe5-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="3dfe5-108">單一登入 (SSO) tooAzure AD 資源從任何地方</span><span class="sxs-lookup"><span data-stu-id="3dfe5-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="3dfe5-109">存取 toohello 企業 Windows 市集所使用的工作或學校帳戶 （不需要 Microsoft 帳戶）</span><span class="sxs-lookup"><span data-stu-id="3dfe5-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="3dfe5-110">使用工作或學校帳戶進行符合企業標準的跨裝置使用者設定漫遊 (不需要 Microsoft 帳戶)</span><span class="sxs-lookup"><span data-stu-id="3dfe5-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="3dfe5-111">透過 Windows Hello 企業版和 Windows Hello 進行工作或學校帳戶的增強式驗證與便利的登入</span><span class="sxs-lookup"><span data-stu-id="3dfe5-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="3dfe5-112">能力 toorestrict 存取符合組織的裝置群組原則設定的 toodevices</span><span class="sxs-lookup"><span data-stu-id="3dfe5-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dfe5-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="3dfe5-113">Prerequisites</span></span>
<span data-ttu-id="3dfe5-114">加入網域會繼續 toobe 很有用。</span><span class="sxs-lookup"><span data-stu-id="3dfe5-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="3dfe5-115">不過，tooget hello Azure AD 的 SSO 的優點，漫遊的設定與工作或學校帳戶，並存取 tooWindows 存放區的工作或學校帳戶，您必須遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="3dfe5-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="3dfe5-116">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3dfe5-116">Azure AD subscription</span></span>
* <span data-ttu-id="3dfe5-117">Azure AD Connect tooextend hello 在內部部署目錄 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="3dfe5-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="3dfe5-118">已設定 tooconnect 已加入網域裝置 tooAzure AD 原則</span><span class="sxs-lookup"><span data-stu-id="3dfe5-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="3dfe5-119">裝置的 Windows 10 組建 (組建 10551 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="3dfe5-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="3dfe5-120">tooenable Windows Hello 的商務和 Windows Hello，您還需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3dfe5-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="3dfe5-121">適用於使用者憑證發行的**公開金鑰基礎結構 (PKI)**。</span><span class="sxs-lookup"><span data-stu-id="3dfe5-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="3dfe5-122">**System Center Configuration Manager 最新分支**-您需要 tooinstall 版本 1606年或更高。</span><span class="sxs-lookup"><span data-stu-id="3dfe5-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="3dfe5-123">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="3dfe5-123">For more information, see:</span></span> 
    - [<span data-ttu-id="3dfe5-124">System Center Configuration Manager 文件</span><span class="sxs-lookup"><span data-stu-id="3dfe5-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="3dfe5-125">System Center Configuration Manager 團隊部落格</span><span class="sxs-lookup"><span data-stu-id="3dfe5-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="3dfe5-126"> System Center Configuration Manager 中的 Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="3dfe5-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="3dfe5-127">為替代 toohello PKI 部署需求，您可以執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3dfe5-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="3dfe5-128">建立幾個 Windows Server 2016 Active Directory 網域服務的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="3dfe5-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="3dfe5-129">tooenable 條件式存取，您可以建立群組原則設定，以允許存取 toodomain 聯結裝置與任何其他的部署。</span><span class="sxs-lookup"><span data-stu-id="3dfe5-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="3dfe5-130">toomanage hello 裝置的相容性為基礎的存取控制，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3dfe5-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="3dfe5-131">適用於 Windows Hello 企業版案例的 System Center Configuration Manager 目前分支 (1606 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="3dfe5-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="3dfe5-132">部署指示</span><span class="sxs-lookup"><span data-stu-id="3dfe5-132">Deployment instructions</span></span>

<span data-ttu-id="3dfe5-133">toodeploy，後續的 hello 步驟中所列[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="3dfe5-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="3dfe5-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3dfe5-134">Next step</span></span>
* [<span data-ttu-id="3dfe5-135">Hello 企業版的 Windows 10： 工作的方式 toouse 裝置</span><span class="sxs-lookup"><span data-stu-id="3dfe5-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="3dfe5-136">擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端</span><span class="sxs-lookup"><span data-stu-id="3dfe5-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="3dfe5-137">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="3dfe5-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="3dfe5-138">連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗</span><span class="sxs-lookup"><span data-stu-id="3dfe5-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="3dfe5-139">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="3dfe5-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

