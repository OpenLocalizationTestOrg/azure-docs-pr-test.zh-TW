---
title: "aaaWhat 是 Azure RemoteApp 嗎？ | Microsoft Docs"
description: "深入了解如何透過 Azure RemoteApp tooshare 應用程式及資源 tooany 裝置。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>什麼是 Azure RemoteApp？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 帶來 hello 在內部部署 Microsoft RemoteApp 程式，支援遠端桌面服務、 tooAzure hello 功能。 Azure RemoteApp 可協助您提供安全、 遠端存取 tooapplications 從許多不同的使用者裝置。 Azure RemoteApp 基本上 hello 雲端中裝載非持續性的終端機伺服器工作階段，且您 toouse 它們並分享您的使用者。

Azure RemoteApp 幾乎可讓您在任何裝置上與使用者共用應用程式和資源。 這表示我們會負責處理 hello 硬體和調整 toomeet 使用者要求，我們會裝載在 hello 雲端中，應用程式。 您只需要 toodo 是上傳您想 tooshare，，然後使用者 toouse 那些應用程式的 hello 應用程式。 [使用者取得 tookeep 自己的裝置](remoteapp-clients.md)，而您管理透過 hello Azure 入口網站的所有項目。 您甚至可以 hello 使用您的公司認證，讓您確保 hello 安全性應用程式和資料。

請閱讀更多有關 Azure RemoteApp 的詳細資訊，或者如果我們已經說服您，請 [立即試用](https://azure.microsoft.com/services/remoteapp/)。

有關於 Azure RemoteApp 的問題嗎？ 請查看我們的 [常見問題集](remoteapp-faq.md)。

Azure RemoteApp 屬於 hello [Microsoft 虛擬桌面基礎結構](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx)。

**新功能！** 想深入了解 Azure RemoteApp toolearn 嗎？ 或準備大規模 toovalidate Azure RemoteApp 嗎？ 加入我們每週[詢問 hello 專家網路研討會](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website)。

## <a name="azure-remoteapp-collections"></a>Azure RemoteApp 收藏
[Azure RemoteApp 收藏](remoteapp-collections.md)分成兩種：

* A**雲端集合**裡，並將程式的資料儲存在 hello 雲端。 使用者可以使用其 Microsoft 帳戶或與 Azure Active Directory 同步處理或同盟的公司認證進行登入，以存取應用程式。
  
    雲端集合時選擇您想要 tooshare hello 應用程式不需要連接 tooany 資源貴公司的私人網路 （例如，透過 VPN 裝置）。 如果 hello 應用程式會使用資源 hello 網際網路，放在 OneDrive 或 Azure 中，在雲端集合可以使用。 它也是 hello 最快速 toocreate。
* A**混合式集合**裡，並將資料儲存在 hello Azure 雲端，但也可讓使用者存取資料和儲存在您的區域網路上的資源。 使用者可以使用與 Azure Active Directory 同步處理或同盟的公司認證進行登入，以存取應用程式。
  
    如果您需要連接 tooresources 貴公司的私人網路上，選擇混合式集合。 例如，如果 hello 應用程式需要存取 tooone hello 以下的：
  
  * 位於內部網路上的檔案伺服器
  * Quicken
  * 防火牆後面的資料庫
    
    這是普遍適用的大型公司具有許多不可以是其私人網路上的資源移動 toohello 雲端。

hello 不同集合有不同的選項，包括網路，因此找出[哪一個集合](remoteapp-collections.md)最適合您。 

### <a name="updating-your-collection"></a>升級收藏
其中一個 hello hello 混合式部署和雲端集合之間的主要差異是如何處理軟體更新。 與雲端集合 hello 預先安裝 Office 365 ProPlus 或 Office 2013 映像，您沒有任何更新 tooworry。 hello 服務會維護本身，並持續、 tooboth 應用程式和 hello 作業系統中推出的更新。

混合式集合，以及使用自訂的範本映像之雲端集合，您需負責維護 hello 映像和應用程式。 對於已加入網域的映像，您可以使用 Windows Update、群組原則或 System Center 等工具控制更新。

更新您的自訂範本映像之後，您上傳新映像 toohello hello Azure 雲端，然後再更新 hello 集合 toouse hello 新映像。 (您可以從 hello Azure RemoteApp**快速入門**頁面上，或 hello 儀表板。)

如需詳細資訊，請參閱 [更新您的收藏](remoteapp-update.md) 。

## <a name="supported-remoteapp-clients"></a>支援的 RemoteApp 用戶端
Mac、 iOS 和 Android 上 hello RemoteApp 用戶端應用程式，適用於 Windows 和 Windows RT 以及 hello Microsoft 遠端桌面應用程式支援 azure RemoteApp。 您的使用者可以使用其行動裝置上的這些應用程式，或計算裝置 tooaccess hello 新的 Azure RemoteApp 程式。

請參閱[存取您的應用程式在 Azure RemoteApp](remoteapp-clients.md) hello 用戶端的相關詳細資訊。

## <a name="next-steps"></a>後續步驟
快！ 立即試用！ 這些文章可幫助您開始使用 Azure RemoteApp：

* [Azure RemoteApp 需要何種集合？](remoteapp-collections.md)
* [建立 Azure RemoteApp 映像](remoteapp-imageoptions.md)
* [如何 toocreate 雲端的 Azure RemoteApp 集合](remoteapp-create-cloud-deployment.md)
* [如何 toocreate Azure RemoteApp 的混合式集合](remoteapp-create-hybrid-deployment.md)
* [Azure RemoteApp 中的授權如何運作？](remoteapp-licensing.md)
* [使用 Azure RemoteApp 的最佳作法](remoteapp-bestpractices.md)
* [Azure RemoteApp 常見問題集](remoteapp-faq.md)

### <a name="help-us-help-you"></a>幫我們來協助您
您知道在加法 toorating 這份文件並進行註解下下方，讓您可以變更 toohello 文章本身嗎？ 有所遺漏？ 有所錯誤？ 我是否撰寫了令人混淆的內容？ 向上捲動，然後按一下  **GitHub 上編輯**或**編輯**toomake 變更-這些是 toous 供檢閱，並接著，我們登入它們，就會看到您的變更與改進這裡。

