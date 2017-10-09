---
title: "aaaHow toocreate 雲端的 Azure RemoteApp 集合 |Microsoft 文件"
description: "了解如何儲存資料中的 Azure RemoteApp 部署 toocreate hello Azure 雲端。"
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
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>如何 toocreate 雲端的 Azure RemoteApp 集合
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

[Azure RemoteApp 收藏](remoteapp-collections.md)分成兩種： 

* 雲端：完全位於 Azure 中。 可以在 hello 雲端中選擇 toosave 所有資料 (因此僅限雲端的集合) 或 tooconnect 您集合 tooa VNET 及儲存那里資料。   
* 混合式： 包含虛擬網路內部存取-對於這需要 hello 使用 Azure AD 和內部部署 Active Directory 環境。

本教學課程會引導您建立雲端集合的 hello 程序。 共有四個步驟： 

1. 建立 Azure RemoteApp 集合。
2. 選擇性地設定目錄同步處理。 如果您使用 Azure AD + Active Directory 中，您有 toosynchronize 使用者、 連絡人和密碼從內部部署 Active Directory tooyour Azure AD 租用戶。
3. 發佈應用程式。
4. 設定使用者存取。

**開始之前**

Toodo hello 下列建立 hello 集合之前，您需要：

* [註冊](https://azure.microsoft.com/services/remoteapp/) Azure RemoteApp。 
* 收集您想要 toogrant 存取的 hello 使用者的相關資訊。 這可以是使用者 Microsoft 帳戶資訊或 Active Directory 工作帳戶資訊。
* 此程序假設您是其中一個進行 toouse 一個 hello 範本提供的映像做為您的訂用帳戶的一部分或您已經上傳您想要 toouse hello 範本映像。 如果您需要 tooupload 不同的範本映像，您可以從 hello 範本映像頁面執行。 只要按一下**上傳範本映像**遵循 hello 精靈中的 hello 步驟。 
* 需要 toouse hello Office 365 ProPlus 映像嗎？ 請在 [這裡](remoteapp-officesubscription.md)查看資訊。
* 想 tooprovide 自訂應用程式或 LOB 程式？ 請建立新的 [映像](remoteapp-imageoptions.md) ，並在您的雲端部署中加以使用。
* 找出您是否需要 tooconnect tooa VNET。 如果您選擇 tooconnect tooa VNET，請確定它符合 hello[大小的指導方針](remoteapp-vnetsizing.md)和它[可以連接 tooRemoteApp](remoteapp-vnet.md)。 簽出 hello [VNET 規劃的發行項](remoteapp-planvnet.md)如需詳細資訊。
* 如果您使用 VNET，決定是否要讓 toojoin 它 tooyour 本機 Active Directory 網域。

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>步驟 1：建立雲端集合 - 不論是否有 VNET
使用 hello 下列步驟會太**建立雲端專屬集合**:

1. 在 hello 管理入口網站中，移至 toohello RemoteApp 頁面。
2. 按一下 [新增] > [快速建立]。
3. 輸入收藏的名稱，然後選取區域。
4. 選擇您想 toouse-標準或基本 hello 計劃。
5. 選擇此集合的 hello 範本 toouse。 
   
    **提示：** RemoteApp 訂用帳戶隨附[範本映像](remoteapp-images.md)包含 Office 365 或 Office 2013 （用於試用） 程式，一些發佈 （例如 Word)，其他人已準備 toopublish。 您也可以建立新的 [映像](remoteapp-imageoptions.md) ，並在您的雲端部署中加以使用。
6. 按一下 [建立 RemoteApp 收藏] 。
   
    **重要事項：**它最多可能需要 too30 分鐘 tooprovision 您的集合。

您的 Azure RemoteApp 集合建立後，按兩下 hello hello 集合名稱。 這會顯示 hello**快速入門**頁面-這是您完成設定 hello 集合。

使用 hello 下列步驟 toocreate **cloud + VNET 集合**:

1. 在 hello 管理入口網站中，移至 toohello Azure RemoteApp 頁面。
2. 按一下 [新增] > [使用 VNET 建立]。
3. 輸入收藏的名稱。
4. 選擇您想 toouse-標準或基本 hello 計劃。
5. 選擇您已經建立的 VNET hello。 不知道如何 toodo 的嗎？ 現在，hello 步驟都在 hello[混合式](remoteapp-create-hybrid-deployment.md)主題。
6. 決定是否要 toojoin 集合 tooyour 網域。 如果是，您需要 toouse AD Connect toointegrate Azure AD 和 Active Directory 環境。 這涵蓋在 **步驟 2**中。
7. 按一下 [建立 RemoteApp 收藏] 。

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>步驟 2：設定 Active Directory 目錄同步處理 (選用)
如果您想 toouse Active Directory 時，Azure RemoteApp 需要 Azure Active Directory 與您在內部部署 Active Directory toosynchronize 使用者、 連絡人和密碼 tooyour Azure Active Directory 租用戶之間的目錄同步作業。 如需規劃資訊，請參閱 [設定 Azure RemoteApp 的 Active Directory](remoteapp-ad.md) 。 您也可以直接太[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/)資訊。

## <a name="step-3-publish-apps"></a>步驟 3：發佈應用程式
Hello 應用程式或程式 tooyour 使用者提供的 Azure RemoteApp 應用程式。 它位於您上傳 hello 集合 hello 範本映像。 使用者存取應用程式、 hello 應用程式出現 toorun 在其本機環境中，但是它實際上正在 Azure 中的虛擬機器。 

您的使用者可以存取應用程式之前，您需要 toopublish 它們 – 發行應用程式可讓您的使用者存取 hello 應用程式透過 hello 遠端桌面用戶端。

您可以發行多個應用程式 tooyour Azure RemoteApp 集合。 從 hello 發行] 頁面上，按一下 [**發行**tooadd 程式。 您可以發行從 hello**啟動**功能表的 hello 範本映像，或藉由指定 hello 路徑 hello hello 應用程式的範本映像上。 如果您選擇 tooadd hello**啟動**功能表上，選擇 hello 應用程式 toopublish。 如果您選擇 tooprovide hello 路徑 toohello 應用程式，提供 hello 應用程式和 hello 路徑 toowhere 它安裝在 hello 範本映像的名稱。

## <a name="step-4-configure-user-access"></a>步驟 4：設定使用者存取
既然您已建立您的集合，您會需要您希望 toobe 無法 toouse 遠端資源 tooadd hello 使用者。 如果您使用 Active Directory，您提供存取 tooneed tooexist hello Active Directory 租用戶中的與訂閱相關聯 hello 您 hello 使用者使用 toocreate 這個集合。

1. 從 hello 快速入門] 頁面上，按一下 [**設定使用者存取**。 
2. 輸入 hello （從 Active Directory) 的工作帳戶或 Microsoft 帳戶，您想要針對 toogrant 存取。
   
   **注意：** 
   
   請確定您使用 hello  *user@domain.com* 格式。
   
   如果您使用 Office 365 ProPlus 集合中，您必須為您的使用者使用 hello Active Directory 身分識別。 這有助於驗證授權。 
3. Hello 使用者驗證之後，按一下**儲存**。

## <a name="next-steps"></a>後續步驟
您已經成功建立並部署了自己的 Azure RemoteApp 雲端收藏。 hello 下一個步驟是的 toohave 使用者下載及安裝 hello 遠端桌面用戶端。 您可以在 hello Azure RemoteApp 快速入門 頁面上找到 hello 用戶端 hello URL。 然後，有使用者登入 hello 用戶端，並存取您發行的 hello 應用程式。

### <a name="help-us-help-you"></a>幫我們來協助您
您知道在加法 toorating 這份文件並進行註解下下方，讓您可以變更 toohello 文章本身嗎？ 有所遺漏？ 有所錯誤？ 我是否撰寫了令人混淆的內容？ 向上捲動，然後按一下  **GitHub 上編輯**toomake 變更-這些是 toous 供檢閱，並接著，我們登入它們，就會看到您的變更與改進這裡。

