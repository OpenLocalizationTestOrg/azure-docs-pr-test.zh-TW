---
title: "aaaUsage 案例和 Azure AD Join 的部署考量 |Microsoft 文件"
description: "說明系統管理員如何為其使用者 (員工、學生、其他使用者) 設定 Azure AD Join。 它也會討論使用 Azure AD Join hello 不同真實世界的案例。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>適用於 Azure AD Join 的使用案例和部署考量
## <a name="usage-scenarios-for-azure-ad-join"></a>適用於 Azure AD Join 的使用案例
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Hello 定域機組中大部分的案例 1： 企業
Azure Active Directory Join (Azure AD Join) 可以受益您您目前操作和管理您的業務 hello 雲端中的身分識別或要移動 toohello 雲端推出。 您可以使用您已在 Azure AD toosign tooWindows 10 中建立的帳戶。 透過[第一次執行體驗 (FRX) 程序的 hello](active-directory-azureadjoin-user-frx.md)，或是從 Azure AD [hello 設定功能表](active-directory-azureadjoin-user-upgrade.md)，您的使用者可以加入其機器 tooAzure AD。  您的使用者也可以享受單一登入 (SSO) 存取太雲端資源，例如 Office 365，在瀏覽器中或在 Office 應用程式。

### <a name="scenario-2-educational-institutions"></a>案例 2：教育機構
教育機構通常有兩種使用者類型：教職員和學生。 教職員版成員視為長期 hello 組織成員。 為他們建立內部部署帳戶是比較好的做法。 不過學生 shorter-term hello 組織成員，因此可以在 Azure AD 中管理他們的帳戶。 這表示，而不是儲存在內部 toohello 雲端可以推送目錄小數位數。 這也表示學生會是能在他們的 Azure AD 帳戶與 tooWindows toosign 和 tooOffice 365 資源取得存取權，在 Office 應用程式。

### <a name="scenario-3-retail-businesses"></a>案例 3：零售業
零售業擁有季節性工作者和長期員工。 您通常會為較長期的全職員工建立內部部署帳戶，讓他們能夠使用已加入網域的電腦。 但季節性工作者 shorter-term hello 組織的成員，而且希望 toomanage 其中使用者授權可以更輕鬆地移動其帳戶。 當您使用 Office 365 授權的 hello 雲端中建立他們的使用者帳戶時，這些使用者會獲得 hello 優勢登入 tooWindows 和 Azure AD 帳戶，Office 應用程式，當您離開後可維持更大的彈性與使用者的授權。

### <a name="scenario-4-additional-scenarios"></a>案例 4：其他案例
先前討論過的 hello 優點，以及您從您的使用者因為簡化聯結的經驗、 有效率的裝置管理、 自動的行動裝置管理註冊和單一登入 tooAzure 加入其裝置 tooAzure AD 中獲益AD 和內部部署資源。  

## <a name="deployment-considerations-for-azure-ad-join"></a>適用於 Azure AD Join 的部署考量
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>啟用您的使用者 toojoin 公司擁有的裝置直接 tooAzure AD
企業可以提供僅限雲端帳戶 toopartner 公司和組織。 這些合作夥伴之後就能使用單一登入，輕易地存取公司的應用程式和資源。 這個案例是適用的 toousers 存取主要是在 hello 雲端中，例如 Office 365 或 SaaS 依賴 Azure AD 進行驗證的應用程式的資源。

### <a name="prerequisites"></a>必要條件
**在 hello 企業層級 （系統管理員）**

* Azure 訂用帳戶搭配 Azure Active Directory  

**Hello 使用者層級**

* Windows 10 (專業版和企業版)

### <a name="administrator-tasks"></a>系統管理員工作
* [設定裝置註冊](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>使用者工作
* [設定期間使用 Azure AD 設定新的 Windows 10 裝置](active-directory-azureadjoin-user-frx.md)
* [設定 Azure AD 與 Windows 10 裝置 hello 設定 功能表](active-directory-azureadjoin-user-upgrade.md)
* [加入個人的 Windows 10 裝置 tooyour 組織](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>在組織中針對 Windows 10 啟用 BYOD
您可以設定您的使用者和員工 toouse 其個人的 Windows 裝置 (BYOD) tooaccess 公司應用程式和資源。 使用者可以將其 Azure AD 帳戶 （工作或學校帳戶） tooa 個人的 Windows 裝置 tooaccess 資源安全且相容的方式。

### <a name="prerequisites"></a>必要條件
**在 hello 企業層級 （系統管理員）**

* Azure AD 訂用帳戶

**Hello 使用者層級**

* Windows 10 (專業版和企業版)

### <a name="administrator-tasks"></a>系統管理員工作
* [設定裝置註冊](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>使用者工作
* [加入個人的 Windows 10 裝置 tooyour 組織](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>其他資訊
* [Hello 企業版的 Windows 10： 工作的方式 toouse 裝置](active-directory-azureadjoin-windows10-devices-overview.md)
* [擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端](active-directory-azureadjoin-user-upgrade.md)
* [透過 Microsoft Passport 不需要密碼就能驗證身分識別](active-directory-azureadjoin-passport.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

