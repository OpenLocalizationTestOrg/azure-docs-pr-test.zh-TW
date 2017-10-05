---
title: "將已加入網域的裝置連接到 Azure AD 以體驗 Windows 10 | Microsoft Docs"
description: "說明系統管理員應如何設定群組原則，使裝置成為企業網路中已加入網域的裝置。"
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="f980c-103">將已加入網域的裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="f980c-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="f980c-104">「加入網域」是過去 15 年來組織使用連接的裝置進行工作的傳統方式。</span><span class="sxs-lookup"><span data-stu-id="f980c-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="f980c-105">這讓使用者能夠使用他們的 Windows Server Active Directory (Active Directory) 工作或學校帳戶來登入其裝置，並允許 IT 能夠完全管理這些裝置。</span><span class="sxs-lookup"><span data-stu-id="f980c-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="f980c-106">組織通常依賴映像處理方法將裝置佈建給使用者，且通常使用 System Center Configuration Manager (SCCM) 或群組原則加以管理。</span><span class="sxs-lookup"><span data-stu-id="f980c-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="f980c-107">當您將裝置連接到 Azure Active Directory (Azure AD) 後，Windows 10 中的「網域加入」會提供您下列優點：</span><span class="sxs-lookup"><span data-stu-id="f980c-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="f980c-108">從任何位置單一登入 (SSO) 至 Azure AD 資源</span><span class="sxs-lookup"><span data-stu-id="f980c-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="f980c-109">使用工作或學校帳戶存取企業 Windows 市集 (不需要 Microsoft 帳戶)</span><span class="sxs-lookup"><span data-stu-id="f980c-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="f980c-110">使用工作或學校帳戶進行符合企業標準的跨裝置使用者設定漫遊 (不需要 Microsoft 帳戶)</span><span class="sxs-lookup"><span data-stu-id="f980c-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="f980c-111">透過 Windows Hello 企業版和 Windows Hello 進行工作或學校帳戶的增強式驗證與便利的登入</span><span class="sxs-lookup"><span data-stu-id="f980c-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="f980c-112">能夠限制為只能存取遵循組織裝置群組原則設定的裝置</span><span class="sxs-lookup"><span data-stu-id="f980c-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f980c-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="f980c-113">Prerequisites</span></span>
<span data-ttu-id="f980c-114">「網域加入」仍持續有用。</span><span class="sxs-lookup"><span data-stu-id="f980c-114">Domain join continues to be useful.</span></span> <span data-ttu-id="f980c-115">但是，若要透過 Azure AD 享有 SSO、使用工作或學校帳戶漫遊設定，以及使用工作或學校帳戶存取 Windows 市集的好處，您必須符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="f980c-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="f980c-116">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f980c-116">Azure AD subscription</span></span>
* <span data-ttu-id="f980c-117">Azure AD Connect，以將內部部署目錄擴充至 Azure AD</span><span class="sxs-lookup"><span data-stu-id="f980c-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="f980c-118">設定來將已加入網域的裝置連接到 Azure AD 的原則</span><span class="sxs-lookup"><span data-stu-id="f980c-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="f980c-119">裝置的 Windows 10 組建 (組建 10551 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="f980c-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="f980c-120">若要啟用 Windows Hello 企業版和 Windows Hello，您還需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f980c-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="f980c-121">適用於使用者憑證發行的**公開金鑰基礎結構 (PKI)**。</span><span class="sxs-lookup"><span data-stu-id="f980c-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="f980c-122">**System Center Configuration Manager 最新分支** - 您必須安裝 1606 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f980c-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="f980c-123">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f980c-123">For more information, see:</span></span> 
    - [<span data-ttu-id="f980c-124">System Center Configuration Manager 文件</span><span class="sxs-lookup"><span data-stu-id="f980c-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="f980c-125">System Center Configuration Manager 團隊部落格</span><span class="sxs-lookup"><span data-stu-id="f980c-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="f980c-126"> System Center Configuration Manager 中的 Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="f980c-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="f980c-127">若要以 PKI 以外的方式進行部署，您可以執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="f980c-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="f980c-128">建立幾個 Windows Server 2016 Active Directory 網域服務的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="f980c-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="f980c-129">若要啟用條件式存取，您可以建立群組原則設定，允許存取已加入網域的裝置，而不需其他部署。</span><span class="sxs-lookup"><span data-stu-id="f980c-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="f980c-130">若要根據裝置的合規性來管理存取控制，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f980c-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="f980c-131">適用於 Windows Hello 企業版案例的 System Center Configuration Manager 目前分支 (1606 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="f980c-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="f980c-132">部署指示</span><span class="sxs-lookup"><span data-stu-id="f980c-132">Deployment instructions</span></span>

<span data-ttu-id="f980c-133">若要進行部署，請依照[如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊](active-directory-conditional-access-automatic-device-registration-setup.md)中所列的步驟操作</span><span class="sxs-lookup"><span data-stu-id="f980c-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="f980c-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f980c-134">Next step</span></span>
* [<span data-ttu-id="f980c-135">適合企業使用的 Windows 10：使用裝置工作的方式</span><span class="sxs-lookup"><span data-stu-id="f980c-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="f980c-136">透過 Azure Active Directory Join 擴充 Windows 10 裝置的雲端功能</span><span class="sxs-lookup"><span data-stu-id="f980c-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="f980c-137">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="f980c-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="f980c-138">將已加入網域裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="f980c-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="f980c-139">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="f980c-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

