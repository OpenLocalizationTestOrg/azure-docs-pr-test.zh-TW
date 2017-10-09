---
title: "aaaAccess 在小組中的 Azure AD 應用程式 Proxy 應用程式 |Microsoft 文件"
description: "使用 Azure AD Application Proxy tooaccess 您的內部部署應用程式，透過 Microsoft 團隊。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>透過 Microsoft Teams 存取內部部署應用程式

Azure Active Directory 應用程式 Proxy 可讓您不論位置為何，單一登入 tooon 內部應用程式與 Microsoft 小組可在同一個地方共同作業工作。 整合 hello 兩個一起表示，您的使用者可以保持產能與隊友在任何情況下。 

使用者可以將雲端應用程式 tootheir 小組通道[使用索引標籤](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US)，但該 SharePoint 網站或計劃工具，它們都會使用時，會發生什麼事裝載在內部部署嗎？ 應用程式 Proxy 是 hello 解決方案。 它們可以新增應用程式使用的通道透過應用程式 Proxy tootheir 發佈 hello 它們一律 tooaccess 自己的應用程式從遠端使用的外部 Url 相同。 而且，因為應用程式 Proxy 會透過 Azure Active Directory，hello 相同單一登入體驗通訊進行驗證。


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>安裝 hello 應用程式 Proxy 連接器和發行您的應用程式

如果您還沒有這麼做，[設定租用戶的應用程式 Proxy 並安裝 hello 連接器](active-directory-application-proxy-enable.md)。 然後，[發佈內部部署應用程式](application-proxy-publish-azure-portal.md)以供遠端存取。 當您要發行 hello 應用程式時，請記下 hello 外部 URL，因為您的使用者將加入 hello 應用程式 tooTeams 時，需要這項資訊。

如果您已經擁有發行的應用程式，但不會記得其外部 Url，它們中查閱 hello [Azure 入口網站](https://portal.azure.com)。 登入，然後瀏覽過**Azure Active Directory** > **企業應用程式** > **所有應用程式**> 選取您的應用程式 >**應用程式 proxy**。

## <a name="add-your-app-tooteams"></a>新增應用程式 tooTeams

一旦您發行應用程式 Proxy 透過 hello 應用程式，可讓使用者知道，他們就可以將它新增為直接在其小組通道中的索引標籤。 請他們遵循下列三個步驟：

1. 瀏覽的 toohello 小組通道想 tooadd 此應用程式，然後選取 **+**  tooadd 索引標籤。

   ![選取 [新增索引標籤]](./media/application-proxy-teams/add-tab.png)

2. 選取**網站**hello 索引標籤選項。

   ![新增網站](./media/application-proxy-teams/website.png)

3. 指定 hello 索引標籤的名稱，並且設定 hello URL toohello 應用程式 Proxy 外部 URL。 

   ![設定索引標籤名稱和 URL](./media/application-proxy-teams/tab-name-url.png)

一旦有一個小組成員加入 hello 索引標籤，會出現在 hello 通道中的每個人。 任何擁有存取 toohello 應用程式的使用者取得他們的 Microsoft 團隊所用的 hello 認證使用的單一登入存取。 任何使用者沒有存取 toohello 應用程式的使用者會看到小組中的 hello 索引標籤，但會封鎖，直到您授與他們權限 toohello 在內部部署應用程式，並且 hello 的 hello 應用程式的 Azure 入口網站已發佈的版本。 

## <a name="next-steps"></a>後續步驟

- 了解如何太[發行內部部署 SharePoint 網站](application-proxy-enable-remote-access-sharepoint.md)應用程式 proxy。
- 設定您的應用程式 toouse[自訂網域](active-directory-application-proxy-custom-domains.md)為其外部 URL。 
