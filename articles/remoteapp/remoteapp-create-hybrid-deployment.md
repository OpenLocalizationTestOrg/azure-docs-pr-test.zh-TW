---
title: "aaaHow toocreate Azure RemoteApp 的混合式集合 |Microsoft 文件"
description: "深入了解如何 toocreate tooyour 內部網路連線的 RemoteApp 的部署。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>如何 toocreate Azure RemoteApp 的混合式集合
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 收藏分成兩種：

* 雲端：完全位於 Azure 中。 可以在 hello 雲端中選擇 toosave 所有資料 (因此僅限雲端的集合) 或 tooconnect 您集合 tooa VNET 及儲存那里資料。   
* 混合式： 包含虛擬網路內部存取-對於這需要 hello 使用 Azure AD 和內部部署 Active Directory 環境。

不知道您需要什麼嗎? 請查看 [Azure RemoteApp 需要何種集合](remoteapp-collections.md)。

本教學課程會引導您建立混合式集合的 hello 程序。 有八個步驟：

1. 決定[映像](remoteapp-imageoptions.md)toouse 集合。 您可以建立自訂映像，或使用其中一個 hello Microsoft 映像包含您訂用帳戶。
2. 設定虛擬網路。 簽出 hello [VNET 規劃](remoteapp-planvnet.md)和[sizing](remoteapp-vnetsizing.md)資訊。
3. 建立收藏。
4. 聯結集合 tooyour 本機網域。
5. 加入範本映像 tooyour 集合。
6. 設定目錄同步處理。 Azure RemoteApp 需要您與 Azure Active Directory 的其中一個 1） 設定 Azure Active Directory 同步作業以 hello 密碼同步處理選項或 2） 設定 Azure Active Directory 同步作業不含 hello 密碼同步處理選項，但使用的網域是整合同盟的 tooAD FS。 簽出 hello [Active Directory 與 RemoteApp 的組態資訊](remoteapp-ad.md)。
7. 發佈 RemoteApp 應用程式。
8. 設定使用者存取。

**開始之前**

Toodo hello 下列建立 hello 集合之前，您需要：

* [註冊](https://azure.microsoft.com/services/remoteapp/) Azure RemoteApp。
* 建立使用者帳戶在 Active Directory toouse，為 hello Azure RemoteApp 服務帳戶。 限制此帳戶的 「 hello 」 權限，讓它只會將機器 toohello 網域。
* 收集內部部署網路的相關資訊：IP 位址資訊和 VPN 裝置詳細資料。
* 安裝 hello [Azure PowerShell](/powershell/azure/overview)模組。
* 收集您想要 toogrant 存取的 hello 使用者的相關資訊。 您將需要 hello Azure Active Directory 使用者主體名稱 (例如， name@contoso.com) 為每個使用者。 請確定 Azure AD 之間的 UPN 是否符合該 hello 和 Active Directory。
* 選擇範本映像。 Azure RemoteApp 範本映像包含 hello 應用程式和程式的 toopublish 為您的使用者。 如需詳細資訊，請參閱 [Azure RemoteApp 映像選項](remoteapp-imageoptions.md) 。
* 需要 toouse hello Office 365 ProPlus 映像嗎？ 請在 [這裡](remoteapp-officesubscription.md)查看資訊。
* [設定 RemoteApp 的 Azure Active Directory](remoteapp-ad.md)。

## <a name="step-1-set-up-your-virtual-network"></a>步驟 1：設定虛擬網路
您可以部署使用現有 Azure 虛擬網路的混合式集合，也可以建立新的虛擬網路。 虛擬網路可讓您的使用者透過 RemoteApp 遠端資源存取您本機網路上的資料。 使用 Azure 虛擬網路可讓您收集直接網路存取 tooother Azure 服務和虛擬機器部署 toothat 虛擬網路。

請確定您檢閱 hello [VNET 規劃](remoteapp-planvnet.md)和[VNET 大小](remoteapp-vnetsizing.md)之前您建立 VNET 時的資訊。

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>建立 Azure VNET，並將其加入 tooyour Active Directory 部署
首先，建立 [虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。 這會對 hello**網路**hello Azure 入口網站中的索引標籤。 您需要 tooconnect 您虛擬網路 toohello 是已同步處理的 tooyour Azure Active Directory 租用戶的 Active Directory 部署。

請參閱[建立虛擬網路使用 Azure 入口網站 hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)如需詳細資訊。

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>確定您的虛擬網路已經為 Azure RemoteApp 準備就緒
請在建立集合之前，先確定您的虛擬網路已準備就緒。 您可以執行下列 hello 來驗證：

1. 建立 Azure 虛擬機器內 hello hello 您剛建立 remoteapp 的虛擬網路子網路。
2. 使用遠端桌面 tooconnect toohello 虛擬機器。 (按一下 [連線] )。
3. 將其聯結 toohello toouse 需 RemoteApp 的相同 Active Directory 部署。

有作用嗎？ 您的虛擬網路和子網路已針對 Azure RemoteApp 準備就緒！

您可以找到更多資訊建立 Azure 虛擬機器，並使用遠端桌面連接 toothem[這裡](https://msdn.microsoft.com/library/azure/jj156003.aspx)。

## <a name="step-2-create-an-azure-remoteapp-collection"></a>步驟 2：建立 Azure RemoteApp 集合
1. 在 hello [Azure 入口網站](http://manage.windowsazure.com)，移至 toohello Azure RemoteApp 頁面。
2. 按一下 [新增] > [使用 VNET 建立]。
3. 輸入收藏的名稱。
4. 選擇您想 toouse-標準或基本 hello 計劃。
5. 選擇您的 VNET 從 hello 下拉式清單，然後您的子網路。
6. 選擇 toojoin 它 tooyour 網域。
7. 按一下 [建立 RemoteApp 收藏] 。

您的 Azure RemoteApp 集合建立後，按兩下 hello hello 集合名稱。 這會顯示 hello**快速入門**頁面-這是您完成設定 hello 集合。

發生錯誤了嗎？ 簽出 hello[疑難排解資訊的混合式集合](remoteapp-hybridtrouble.md)。

## <a name="step-3-link-your-collection-toohello-local-domain"></a>步驟 3： 連結集合 toohello 本機網域
1. 在 hello**快速入門**頁面上，按一下**加入本機網域**。
2. 新增 hello Azure RemoteApp 服務帳戶 tooyour 本機 Active Directory 網域。 您必須 hello 網域名稱、 組織單位、 服務帳戶使用者名稱和密碼。
   
    這是 hello 您收集的資訊，如果您依照中的 hello 步驟[的 Azure RemoteApp 設定 Active Directory](remoteapp-ad.md)。

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>步驟 4： 連結 tooan Azure RemoteApp 映像
Azure RemoteApp 範本映像包含您想要 tooshare 與使用者的 hello 程式。 您可以建立新[範本映像](remoteapp-imageoptions.md)或連結 tooan 現有映像 （其中一個已匯入或上傳 tooAzure RemoteApp）。 您也可以將連結的 hello Azure RemoteApp tooone[範本映像](remoteapp-images.md)包含 Office 365 或 Office 2013 （用於試用） 程式。

如果您要上傳 hello 新映像，您需要 tooenter hello 名稱，然後選擇 hello hello 映像的位置。 在 hello hello 精靈的下一個頁面上，將看到的 PowerShell cmdlet-複製組，並執行這些 cmdlet，從提升權限 Windows PowerShell 提示 tooupload hello 指定映像。

如果您要連結 tooan 現有範本映像，則您只需要指定 hello 映像名稱、 位置及相關聯的 Azure 訂用帳戶。

## <a name="step-5-configure-active-directory-directory-synchronization"></a>步驟 5：設定 Active Directory 目錄同步處理
Azure RemoteApp 需要您與 Azure Active Directory 的其中一個 1） 設定 Azure Active Directory 同步作業以 hello 密碼同步處理選項或 2） 設定 Azure Active Directory 同步作業不含 hello 密碼同步處理選項，但使用的網域是整合同盟的 tooAD FS。

請參閱 [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) - 本文會協助您以 4 個步驟設定目錄整合。

如需規劃資訊和詳細步驟，請參閱 [目錄同步處理藍圖](http://msdn.microsoft.com//library/azure/hh967642.aspx) 。

## <a name="step-6-publish-apps"></a>步驟 6：發佈應用程式
Hello 應用程式或程式 tooyour 使用者提供的 Azure RemoteApp 應用程式。 它位於您上傳 hello 集合 hello 範本映像。 當使用者存取應用程式時，它會出現在其本機環境中，toorun，但實際上在 Azure 中執行。

您的使用者可以存取應用程式之前，您需要 toopublish 它們 – 這可讓使用者存取 hello 應用程式透過 hello 遠端桌面用戶端。

您可以發行多個應用程式 tooyour 集合。 從 hello 發行] 頁面上，按一下 [**發行**tooadd 應用程式。 您可以發行從 hello**啟動**功能表的 hello 範本映像，或藉由指定 hello 路徑 hello hello 應用程式的範本映像上。 如果您選擇 tooadd hello**啟動**功能表上，選擇 hello 程式 tooadd。 如果您選擇 tooprovide hello 路徑 toohello 應用程式，提供 hello 應用程式和 hello 路徑 toowhere 它安裝在 hello 範本映像的名稱。

## <a name="step-7-configure-user-access"></a>步驟 7：設定使用者存取
既然您已建立您的集合，您會需要您希望 toobe 無法 toouse 遠端資源 tooadd hello 使用者。 hello，提供存取 tooneed tooexist hello Active Directory 租用戶中的與訂閱相關聯 hello 您使用的使用者 toocreate 這個 Azure RemoteApp 集合。

1. 從 hello 快速入門] 頁面上，按一下 [**設定使用者存取**。
2. 輸入 hello （從 Active Directory) 的工作帳戶或 Microsoft 帳戶，您想要針對 toogrant 存取。
   
   **注意：**
   
   請確定您使用 hello  *user@domain.com* 格式。
   
   如果您使用 Office 365 ProPlus 集合中，您必須為您的使用者使用 hello Active Directory 身分識別。 這有助於驗證授權。
3. 一旦 hello 使用者進行驗證，按一下 **儲存**。

## <a name="next-steps"></a>後續步驟
您已經成功建立並部署了自己的 Azure RemoteApp 混合式集合。 hello 下一個步驟是的 toohave 使用者下載及安裝 hello 遠端桌面用戶端。 您可以在 hello Azure RemoteApp 快速入門 頁面上找到 hello 用戶端 hello URL。 然後，有使用者登入 hello 用戶端，並存取您發行的 hello 應用程式。

### <a name="help-us-help-you"></a>幫我們來協助您
您知道在加法 toorating 這份文件並進行註解下下方，讓您可以變更 toohello 文章本身嗎？ 有所遺漏？ 有所錯誤？ 我是否撰寫了令人混淆的內容？ 向上捲動，然後按一下  **GitHub 上編輯**toomake 變更-這些是 toous 供檢閱，並接著，我們登入它們，就會看到您的變更與改進這裡。

