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
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗
網域聯結是 hello 傳統方式組織已連接的裝置 hello 過去 15 年及更多的工作。 必須啟用該使用者 toosign tootheir 裝置中的使用 Windows Server Active Directory (Active Directory) 工作或學校帳戶，並允許的 IT toofully 管理這些裝置。 組織通常依賴映像方法 tooprovision 裝置 toousers 和通常使用 System Center Configuration Manager (SCCM) 或群組原則 toomanage 它們。


在 Windows 10 中的網域加入為您提供 hello 連接裝置 tooAzure Active Directory (Azure AD) 之後，下列優點：

* 單一登入 (SSO) tooAzure AD 資源從任何地方
* 存取 toohello 企業 Windows 市集所使用的工作或學校帳戶 （不需要 Microsoft 帳戶）
* 使用工作或學校帳戶進行符合企業標準的跨裝置使用者設定漫遊 (不需要 Microsoft 帳戶)
* 透過 Windows Hello 企業版和 Windows Hello 進行工作或學校帳戶的增強式驗證與便利的登入
* 能力 toorestrict 存取符合組織的裝置群組原則設定的 toodevices

## <a name="prerequisites"></a>必要條件
加入網域會繼續 toobe 很有用。 不過，tooget hello Azure AD 的 SSO 的優點，漫遊的設定與工作或學校帳戶，並存取 tooWindows 存放區的工作或學校帳戶，您必須遵循的 hello:

* Azure AD 訂用帳戶
* Azure AD Connect tooextend hello 在內部部署目錄 tooAzure AD
* 已設定 tooconnect 已加入網域裝置 tooAzure AD 原則
* 裝置的 Windows 10 組建 (組建 10551 或更新版本)

tooenable Windows Hello 的商務和 Windows Hello，您還需要下列 hello:

- 適用於使用者憑證發行的**公開金鑰基礎結構 (PKI)**。

- **System Center Configuration Manager 最新分支**-您需要 tooinstall 版本 1606年或更高。  
如需詳細資訊，請參閱： 
    - [System Center Configuration Manager 文件](https://technet.microsoft.com/library/mt346023.aspx)
    - [System Center Configuration Manager 團隊部落格](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [ System Center Configuration Manager 中的 Windows Hello 企業版](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

為替代 toohello PKI 部署需求，您可以執行下列 hello:

* 建立幾個 Windows Server 2016 Active Directory 網域服務的網域控制站。

tooenable 條件式存取，您可以建立群組原則設定，以允許存取 toodomain 聯結裝置與任何其他的部署。 toomanage hello 裝置的相容性為基礎的存取控制，您需要下列 hello:

* 適用於 Windows Hello 企業版案例的 System Center Configuration Manager 目前分支 (1606 或更新版本)

## <a name="deployment-instructions"></a>部署指示

toodeploy，後續的 hello 步驟中所列[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>後續步驟
* [Hello 企業版的 Windows 10： 工作的方式 toouse 裝置](active-directory-azureadjoin-windows10-devices-overview.md)
* [擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端](active-directory-azureadjoin-user-upgrade.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

