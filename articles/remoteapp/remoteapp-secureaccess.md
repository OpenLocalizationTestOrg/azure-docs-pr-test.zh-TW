---
title: "aaaSecuring 存取 tooAzure RemoteApp，及 |Microsoft 文件"
description: "使用 Azure Active Directory 中的條件式存取，了解如何安全存取 tooAzure RemoteApp"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>保護存取 tooAzure RemoteApp，和更新版本
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

本文章中我們會提供系統管理員如何設定從 hello 終端使用者，透過 Azure RemoteApp，且結尾受保護的資源，例如 SQL 資料庫或另一個應用程式後端的安全存取通道的概觀。 hello 目標是 toomake 確定從 hello 控制 Azure RemoteApp 環境，而不是從其他位置，只可以存取只有授權的使用者會議 hello 預期條件可以存取遠端應用程式，和的 hello 安全後端。

有 3 hello 系統管理員必須在 toolook 的主要區域：

![Azure RemoteApp 條件式存取的考量](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

閱讀資訊及回答 toothese 問題。

## <a name="who-can-access-hello-collection"></a>誰可以存取 hello 集合？
hello 管理員選擇 hello 使用者可以存取遠端 hello 集合中的應用程式。 您可以使用 Azure Active Directory (Azure AD) 的公司或學校帳戶 (先前稱為「組織帳戶」) 或 Microsoft 帳戶 (例如 @outlook.com)。 大部分的企業案例使用 Azure AD 帳戶。它們可讓您使用稍後討論的條件式存取功能，也是唯一的選擇 hello 已加入網域的集合。 hello 文章的 hello 其餘部分會假設您正在使用 Azure AD 帳戶與 Azure RemoteApp。

**我們已完成的工作：**

使用 Azure AD 帳戶 toocontrol 存取 tooAzure RemoteApp 讓我們兩件事：

1. 我們一定會知道誰可以存取應用程式，我們已發佈，且這些應用程式存取任何後端連接至 hello。
2. 我們控制 hello 基礎 Azure AD，讓我們可以建立和刪除使用者帳戶、 設定密碼原則，使用多因素驗證等等。 

## <a name="how-is-hello-collection-accessed-from-where"></a>如何存取 hello 集合？ 是從哪裡進行存取的？
通常系統管理員想要存取公用網際網路的環境，例如 Azure RemoteApp toodefine 原則。 例如，他們想 tooensure 存取 hello 環境的 hello 公司網路外部的使用者具有 toogain toouse multi-factor authentication (MFA) 的存取;或可能應該封鎖完全。

Azure RemoteApp 系統管理員可以使用其 Azure RemoteApp 環境的 hello 功能可透過 Azure AD Premium tooset 條件式存取原則。 他們也可以使用豐富的報表和警示功能 toomonitor hello 環境正在存取的方式。

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>如何設定 「 條件式存取的 Azure RemoteApp tooset
我們會透過範例案例進行 toowalk (hello Azure RemoteApp 管理員想 tooblock 存取 toohello 環境，當使用者 hello 公司網路外部時）。

> [!NOTE]
> 我們假設您已升級 Azure AD toohello Premium 層，且您已建立至少一個 Azure RemoteApp 集合。
> 
> 

1. 在 Azure 入口網站中按一下 [hello **Active Directory** ] 索引標籤。然後按一下您想要 tooconfigure hello 目錄。
   
   請記住： 條件式存取是目錄的您，而不是目錄的 Azure RemoteApp 的屬性，因此 hello 目錄層級會完成所有設定。 這也表示您需要 toobe hello 目錄管理員 toomake 這些變更。
2. 按一下**應用程式**，然後按一下 **Microsoft Azure RemoteApp** tooset 條件式存取。 請注意，您可以個別為目錄中的每個「軟體即服務」應用程式設定條件式存取。
   ![設定 Azure RemoteApp 的條件式存取](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. 在 hello**設定**索引標籤上，設定**啟用存取規則**tooON。
   ![啟用 Azure RemoteApp 的存取規則](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. 您現在可以設定不同的規則，並選擇人員 tooapply 至：
   
   1. 選擇**封鎖存取不在工作時**toocompletely 可防止使用者存取您指定的 hello 網路環境之外的 Azure RemoteApp。
   2. 按一下 [hello] 選項底下 toodefine hello IP 位址範圍構成 「 受信任的網路 」。 此範圍以外的所有位址將會遭到拒絕。
5. 測試您的組態啟動 hello Azure RemoteApp 用戶端，從您所指定的 hello 範圍之外的 IP 位址。 在使用 Azure AD 認證登入之後，您應該會看到如下的訊息：

![存取遭到拒絕的 tooAzure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>未來的條件式存取功能
hello Azure Active Directory 團隊正在進行條件式存取的新功能。 系統管理員都能 toocreate 新類型的網路位置基礎規則以外的規則。 Hello 新功能的公開預覽版應該很快就可使用。

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>Toomonitor 如何存取 tooAzure RemoteApp
與條件式存取功能很不錯 toouse 是 hello Azure Active Directory Premium 的報告功能。 您可以使用報表 toomonitor 正在存取您的環境，以及偵測任何可疑的活動。

例如，請參閱 hello 多少次一樣它存取 Azure RemoteApp 的 hello 使用者名稱和時間。

1. 在 Azure 入口網站中，按一下 [Active Directory] ，然後按一下您的目錄。
2. 移 toohello**報表** 索引標籤。
3. 從 hello 報告清單中選取**應用程式使用情形**下**整合應用程式**。
   
   您會看到 Azure RemoteApp 的一些彙總統計資料。 
   ![彙總的 Azure RemoteApp 存取統計資料](./media/remoteapp-secureaccess/ra-accessstats.png)
4. 按一下 hello 應用程式 tooreveal 存取 Azure RemoteApp 的使用者資訊。
   ![Azure RemoteApp 的使用者存取統計資料](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>摘要
您可以設定存取規則 tooAzure RemoteApp （和其他軟體即服務應用程式可透過 Azure AD） 與 Azure Active Directory Premium。 規則是目前限制的 toonetwork 位置基礎的原則，但將在未來的 hello 擴充 tooother 企業管理的層面。

Azure AD Premium 也提供報告和監視功能，可進一步擴充 hello 控制項 hello 管理員有透過其 Azure RemoteApp 環境。

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>如何確定我的安全資源只能從 Azure RemoteApp 環境進行存取？
這篇文章的上一節我們著重於保護存取 toohello Azure RemoteApp 環境。 我們已完成，藉由選擇允許存取的 hello 使用者，以及設定存取規則 toofurther 控制如何使用 hello 服務。

Azure RemoteApp 部署的常見案例是 hello 遠端應用程式需要 toocommunicate 與後端資源，例如 SQL 資料庫。 此資源裝載在內部 （例如公司網路中） 或 （例如在 Azure IaaS) 中的 hello 雲端中。 系統管理員通常會想 toomake 確定由透過 Azure RemoteApp 部署的應用程式以及不例如直接在使用者的電腦上執行，且透過公用網際網路存取的應用程式，只可以存取 hello 後端資源。 Hello 集中管理及安全的環境，因此，使用者應與互動的 hello 唯一路徑 hello 後端資源，通常會看到 azure RemoteApp。

hello 解決方法是 tooplace 兩者 hello Azure RemoteApp 環境，並且在 hello 安全資源 hello 相同 Azure 虛擬網路 (VNET)。 如果 hello 資源是在不同的站台，您可以建立站對站 VPN 連線，例如 toocreate VNet 跨距 hello Azure 資料中心和 hello 客戶在內部部署環境。

Azure RemoteApp 支援兩種集合部署類型，您可以在其中提供您自己的 VNET：

* 非加入網域的： hello 應用程式中會有"的視野"hello 的其他資源 hello VNET。 比方說，這可以是使用的 tooconnect 應用程式 tooa SQL 資料庫使用 SQL 驗證 （應用程式會驗證 hello 使用者直接針對 hello 資料庫）
* 加入網域： hello Azure RemoteApp 所使用的虛擬機器是聯結的 tooa hello VNET 中的網域控制站。 Hello 應用程式需要 tooauthenticate 順序 tooget 存取 tooa 後端資源中的 Windows 網域控制站時，這非常有用。
  ![Azure RemoteApp 中已加入網域的集合](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>如何 toocreate Azure 與我的內部部署環境之間的安全連線
有數個組態選項可供用來連接 Azure 和內部部署環境。 Hello 選項的概觀，這裡會提供。

與 Azure RemoteApp 一起您首先，需要 tooconfigure VNet，然後再將它使用 hello 建立程序的集合。 

## <a name="hello-complete-solution"></a>hello 完整的解決方案
hello 圖會顯示 hello 完整的解決方案，我們有內建安全存取通道 hello 終端使用者，透過 Azure RemoteApp (ARA)，從 hello 後端資源。
![保護 Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png)在階段 1 我們選取 [使用者] hello 和建立存取規則會控制 ARA 如何存取。 在 hello 面範例中我們僅允許存取工作從 hello 公司網路的使用者。 不相容的使用者將不會無法 tooaccess hello ARA 環境。
階段 2 中我們公開 hello 後端資源只能透過我們控制 hello VNet 或 VPN 組態。 Azure RemoteApp 已放置於 hello 相同 VNet。 hello 最終結果是只可以透過 hello ARA 環境存取 hello 的資源。

