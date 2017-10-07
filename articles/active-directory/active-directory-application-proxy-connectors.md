---
title: "aaaClassic 入口網站的 Azure AD 應用程式 Proxy 連接器 |Microsoft 文件"
description: "涵蓋如何 toocreate 和管理的 Azure AD 應用程式 Proxy 連接器群組。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>使用連接器群組在個別的網路和位置上發佈應用程式
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-application-proxy-connectors-azure-portal.md)
> * [Azure 傳統入口網站](active-directory-application-proxy-connectors.md)
>
>

連接器群組可用於多種不同狀況，包括：

* 具有多個互連資料中心的網站。 在此情況下，您想讓 tookeep 盡流量 hello 資料中心內儘可能因為跨資料中心的連結是高度耗費資源而變慢。 您可以部署中每個資料中心 tooserve 只有 hello 應用程式位於 hello 資料中心內的連接器。 這種方式跨資料中心連結降到最低，並提供完全透明的經驗 tooyour 使用者。
* 管理不屬於 hello 主要公司網路的隔離網路上安裝的應用程式。 您可以使用連接器群組 tooinstall 專用連接器隔離的網路 tooalso 隔離的應用程式 toohello 網路上。
* 對於應用程式安裝在 IaaS 雲端存取，連接器群組提供常見服務 toosecure hello 存取 tooall hello 應用程式。 連接器群組不在您的公司網路上建立其他相依性或片段 hello 應用程式體驗。 連接器可安裝在每個雲端資料中心，而且只為此網路中的應用程式提供服務。 您可以安裝數個連接器 tooachieve 高可用性。
* 多樹系環境中特定連接器部署每個樹系及設定 tooserve 特定應用程式的支援。
* 連接器群組可用於災害復原站台 tooeither 偵測容錯移轉，或做為備份的 hello 主要站台。
* 連接器群組也可以是使用的 tooserve 來自單一租用戶的多個公司。

## <a name="prerequisite-create-your-connectors"></a>必要條件︰建立連接器
toogroup 的連接器，[安裝多個連接器](active-directory-application-proxy-enable.md)，然後將其命名並將它們群組。 最後您擁有 tooassign 它們 toospecific 應用程式。

## <a name="step-1-create-connector-groups"></a>步驟 1：建立連接器群組
您可以建立任意數量的連接器群組。 連接器群組建立為 hello Azure 傳統入口網站中完成。

1. 選取您的目錄，然後按一下 [設定] 。  
    ![應用程式 Proxy [設定] 螢幕擷取畫面 - 按一下 [管理連接器群組]](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. 在應用程式 Proxy 下按一下**管理連接器群組**並建立連接器群組為 hello 群組指定的名稱。  
    ![應用程式 Proxy 連接器群組螢幕擷取畫面 - 為新群組命名](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>步驟 2： 指派連接器 tooyour 群組
一旦建立 hello 連接器群組時，移動 hello 連接器 toohello 適當的群組。

1. 在 [應用程式 Proxy] 底下，按一下 [管理連接器]。
2. 在下**群組**，選取您想要針對每個連接器的 hello 群組。 可能需要向上 too10 分鐘 toobecome hello 連接器 hello 新群組中的使用中。  
    ![應用程式 Proxy 連接器螢幕擷取畫面 - 從下拉式功能表中選取群組](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>步驟 3： 將應用程式指派 tooyour 連接器群組
hello 最後一個步驟是 tooset 提供每個應用程式 toohello 連接器群組。

1. 在 hello Azure 傳統入口網站，在您目錄中，選取 hello 應用程式，您要讓 tooassign toohello 群組，然後按一下**設定**。
2. 在下**連接器群組**，選取您想在 hello 應用程式 toouse hello 群組。 這項變更會立即套用。  
    ![應用程式 Proxy 連接器群組螢幕擷取畫面 - 從下拉式功能表中選取群組](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>另請參閱
* [啟用應用程式 Proxy](active-directory-application-proxy-enable.md)
* [啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)
* [啟用條件式存取](active-directory-application-proxy-conditional-access.md)
* [使用應用程式 Proxy 疑難排解您遇到的問題](active-directory-application-proxy-troubleshoot.md)

如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)
