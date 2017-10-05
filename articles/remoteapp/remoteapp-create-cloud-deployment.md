---
title: "如何建立 Azure RemoteApp 的雲端收藏 | Microsoft Docs"
description: "了解如何建立將資料儲存在 Azure 雲端中的 Azure RemoteApp 部署。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 52d5a073c0de42a77cd7163bf402ed2cdf598d95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-cloud-collection-of-azure-remoteapp"></a>如何建立 Azure RemoteApp 的雲端收藏
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

[Azure RemoteApp 收藏](remoteapp-collections.md)分成兩種： 

* 雲端：完全位於 Azure 中。 您可以選擇在雲端儲存所有資料 (也就是僅限雲端的集合) 或將您的集合連線到 VNET，並於該處儲存資料。   
* 混合式：包含可內部存取的虛擬網路，這需要使用 Azure AD 和內部部署的 Active Directory 環境。

本教學課程將逐步引導您完成建立雲端收藏的程序。 共有四個步驟： 

1. 建立 Azure RemoteApp 集合。
2. 選擇性地設定目錄同步處理。 如果您使用 Azure AD + Active Directory，就必須將使用者、連絡人和密碼從您的內部部署 Active Directory 同步處理至 Azure AD 租用戶。
3. 發佈應用程式。
4. 設定使用者存取。

**開始之前**

在建立收藏之前，您必須執行下列作業：

* [註冊](https://azure.microsoft.com/services/remoteapp/) Azure RemoteApp。 
* 收集您想授與存取權之使用者的相關資訊。 這可以是使用者 Microsoft 帳戶資訊或 Active Directory 工作帳戶資訊。
* 此程序假設您將使用您的訂閱隨附的範本映像之一，或是您已上傳所要使用的範本映像。 如果您需要上傳不同的範本映像，您可以從 [範本映像] 頁面執行此作業。 只要按一下 [上傳範本映像]  ，然後遵循精靈中的步驟即可。 
* 想要使用 Office 365 ProPlus 的映像嗎？ 請在 [這裡](remoteapp-officesubscription.md)查看資訊。
* 想提供自訂應用程式或 LOB 程式？ 請建立新的 [映像](remoteapp-imageoptions.md) ，並在您的雲端部署中加以使用。
* 了解您是否需要連接到 VNET。 如果您選擇連接到 VNET，請確定它是否符合[調整大小的指導方針](remoteapp-vnetsizing.md)，以及它是否[可以連接到 RemoteApp](remoteapp-vnet.md)。 如需詳細資訊，請參閱 [VNET 規劃文章 ](remoteapp-planvnet.md)。
* 如果您使用 VNET，請決定是否要將它聯結至本機 Active Directory 網域。

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>步驟 1：建立雲端集合 - 不論是否有 VNET
請使用下列步驟 **建立純雲端集合**：

1. 在 Azure 管理入口網站中，移至 RemoteApp 頁面。
2. 按一下 [新增] > [快速建立]。
3. 輸入收藏的名稱，然後選取區域。
4. 選擇您要使用的方案 - 標準或基本。
5. 選擇要用於此收藏的範本。 
   
    **提示：** 您的 RemoteApp 訂閱會隨附於包含 Office 365 或 Office 2013 (供試用) 程式的 [範本映像](remoteapp-images.md) ，其中有些程式已發佈 (例如 Word)，有些即將發佈。 您也可以建立新的 [映像](remoteapp-imageoptions.md) ，並在您的雲端部署中加以使用。
6. 按一下 [建立 RemoteApp 收藏] 。
   
    **重要：** 佈建收藏最多可能需要 30 分鐘。

建立了 Azure RemoteApp 集合之後，請按兩下集合的名稱。 這時會顯示 [快速入門]  頁面，您可以在這裡完成設定集合。

請使用下列步驟建立 **雲端 + VNET 集合**：

1. 在管理入口網站中，前往 [Azure RemoteApp] 頁面。
2. 按一下 [新增] > [使用 VNET 建立]。
3. 輸入收藏的名稱。
4. 選擇您要使用的方案 - 標準或基本。
5. 選擇您已經建立的 VNET。 不知道該怎麼做？ 這些步驟目前都在 [混合式](remoteapp-create-hybrid-deployment.md) 主題中。
6. 決定您是否要將集合聯結至網域。 如果是，您需要使用 AD Connect 來整合 Azure AD 及 Active Directory 環境。 這涵蓋在 **步驟 2**中。
7. 按一下 [建立 RemoteApp 收藏] 。

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>步驟 2：設定 Active Directory 目錄同步處理 (選用)
如果您要使用 Active Directory，則必須在 Azure Active Directory 與您的內部部署 Active Directory 之間進行目錄同步處理，RemoteApp 才能將使用者、連絡人和密碼同步處理至您的 Azure Active Directory 租用戶。 如需規劃資訊，請參閱 [設定 Azure RemoteApp 的 Active Directory](remoteapp-ad.md) 。 您也可以直接移至 [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) 以取得資訊。

## <a name="step-3-publish-apps"></a>步驟 3：發佈應用程式
Azure RemoteApp 應用程式就是您提供給使用者的應用程式或程式。 此程式位於您為收藏上傳的範本映像中。 當使用者存取應用程式時，應用程式看起來會像是在本機環境中執行，但其實是在 Azure 中的虛擬機器中執行。 

您必須先發佈應用程式，您的使用者才能存取應用程式 – 發佈應用程式可讓您的使用者透過遠端桌面用戶端存取應用程式。

您可以將多個應用程式發佈到自己的 Azure RemoteApp 集合。 請在發佈頁面中按一下 [發佈]  來新增程式。 您可以從範本映像的 [開始]  功能表發佈，或藉由為 App 指定範本映像的路徑來發佈。 如果您選擇從 [開始]  功能表新增，請選擇要發佈的應用程式。 如果您選擇提供應用程式的路徑，請提供應用程式的名稱，以及應用程式在範本映像上的安裝路徑。

## <a name="step-4-configure-user-access"></a>步驟 4：設定使用者存取
您已經建立集合，現在您必須新增可使用您遠端資源的使用者。 如果您使用 Active Directory，則您要給予存取權的使用者，必須存在於與您用來建立此集合的訂用帳戶相關聯的 Active Directory 租用戶中。

1. 在 [快速入門] 頁面上，按一下 [Configure user access] 。 
2. 輸入工作帳戶 (來自於 Active Directory)，或是您要為其授與存取權的 Microsoft 帳戶。
   
   **注意：** 
   
   請確定您使用 *user@domain.com* 格式。
   
   如果您的收藏中使用 Office 365 ProPlus，您必須為使用者使用 Active Directory 身分識別。 這有助於驗證授權。 
3. 在驗證使用者之後，按一下 [儲存] 。

## <a name="next-steps"></a>後續步驟
您已經成功建立並部署了自己的 Azure RemoteApp 雲端收藏。 下一個步驟是要讓使用者下載並安裝遠端桌面用戶端。 您可以在 Azure RemoteApp 的 [快速啟動] 頁面上找到用戶端的 URL。 接著，請讓使用者登入用戶端，並存取您所發佈的應用程式。

### <a name="help-us-help-you"></a>幫我們來協助您
您知道除了評比這篇文章以及在下面留言以外，您可以變更文件本身嗎？ 有所遺漏？ 有所錯誤？ 我是否撰寫了令人混淆的內容？ 向上捲動並按一下 [在 GitHub 上編輯]  以進行變更 - 系統會顯示這些變更以供我們檢閱，而我們簽核後，您就會在這裡看到您所進行的變更和改良。

