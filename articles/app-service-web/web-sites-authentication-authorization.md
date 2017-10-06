---
title: "與 Azure 應用程式中的內部部署 Active Directory aaaAuthenticate |Microsoft 文件"
description: "了解如何在 Azure App Service tooauthenticate 與內部部署 Active Directory 中的特定業務應用程式的 hello 不同方式"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>在 Azure 應用程式中使用內部部署 Active Directory 進行驗證
本文章將示範如何使用 tooauthenticate 內部部署 Active Directory (AD) 中[Azure App Service](../app-service/app-service-value-prop-what-is.md)。 Azure 應用程式裝載於 hello 雲端，但有方式 tooauthenticate 內部部署 AD 使用者安全地。 

## <a name="authenticate-through-azure-active-directory"></a>透過 Azure Active Directory 進行驗證
Azure Active Directory 租用戶的目錄可與內部部署 AD 進行同步處理。 這種方法可讓 AD 使用者要能夠存取您的應用程式從 hello 網際網路，並使用其內部部署認證進行驗證。 此外，Azure App Service 還提供 [適用於此方法的周全解決方案](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。 只要按幾下按鈕，您就可以使用 Azure 應用程式的目錄同步租用戶進行驗證。 這個方法有下列優點 hello:

* 應用程式中不需要任何驗證程式碼。 可讓應用程式服務，請執行 hello 驗證為您和您的時間花在提供應用程式中的功能。
* [Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)啟用存取 toodirectory 資料從 Azure 應用程式。
* 提供 SSO 太[所有支援的 Azure Active Directory 的應用程式](/marketplace/active-directory/)，包括 Office 365、 Dynamics CRM Online、 Microsoft Intune 和數千個非 Microsoft 的雲端應用程式。 
* Azure Active Directory 支援角色型存取控制。 您可以使用 hello [Authorize(Roles="X")] 模式幾乎不需要變更 tooyour 程式碼。

如何 toowrite 業務的 Azure 應用程式，向 Azure Active Directory，請參閱的 toosee[建立業務的 Azure 應用程式與 Azure Active Directory 驗證](web-sites-dotnet-lob-application-azure-ad.md)。

## <a name="authenticate-through-an-on-premises-sts"></a>透過內部部署 STS 進行驗證
如果您有內部部署安全權杖服務 (STS) 像是 Active Directory Federation Services (AD FS)，您可以使用該 toofederate 驗證 Azure 應用程式。 當公司原則禁止 AD 資料儲存在 Azure 時，這是最合適的方法。 不過，請注意 hello 下列：

* STS 拓撲必須在內部部署，需要成本和管理費用。
* 唯一的 AD FS 系統管理員可以設定[信賴憑證者合作對象信任和宣告規則](http://technet.microsoft.com/library/dd807108.aspx)，這可能會限制 hello 開發人員選項。 在上 hello 相反地，它是可能 toomanage 及自訂[宣告](http://technet.microsoft.com/library/ee913571.aspx)每個應用程式為基礎。
* Tooon 內部部署存取 AD 資料需要不同的解決方案，透過 hello 公司防火牆。

如何 toowrite 業務的 Azure 應用程式，以便驗證與內部部署 STS，請參閱的 toosee[業務的 Azure 應用程式建立與 AD FS 驗證](web-sites-dotnet-lob-application-adfs.md)。

