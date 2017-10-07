---
title: "aaaGet 啟動使用儲存體總管 （預覽） |Microsoft 文件"
description: "使用儲存體總管管理 Azure 儲存體資源 (預覽)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>開始使用儲存體總管 (預覽)
## <a name="overview"></a>概觀
Azure 儲存體總管 （預覽） 是獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體資料。 在本文中，您會學習 hello 連線 tooand 管理您的 Azure 儲存體帳戶的各種方式。

![Microsoft Azure 儲存體 Explorer (預覽)][15]

## <a name="prerequisites"></a>必要條件
* [下載並安裝儲存體總管 (預覽)](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>連接 tooa 儲存體帳戶或服務
儲存體總管 （預覽） 提供數種方式 tooconnect toostorage 帳戶。 例如，您可以：
* 連接與您 Azure 訂用帳戶相關聯的 toostorage 帳戶。
* 從其他 Azure 訂用帳戶連接 toostorage 帳戶和服務所共用。
* 連接 tooand 管理使用 hello Azure 儲存體模擬器的本機儲存體。 

此外，您可以使用全球和國家 Azure 中的儲存體帳戶：

* [連接 Azure 訂用帳戶 tooan](#connect-to-an-azure-subscription)： 管理屬於 tooyour Azure 訂用帳戶的儲存體資源。
* [使用本機開發儲存體](#work-with-local-development-storage)： 管理使用 hello Azure 儲存體模擬器的本機儲存體。
* [附加 tooexternal 儲存體](#attach-or-detach-an-external-storage-account)： 管理屬於 tooanother Azure 訂用帳戶的儲存體資源，或已國家 （地區） 的 Azure 雲端 底下使用 hello 儲存體帳戶的名稱、 金鑰和端點。
* [使用 SAS 附加儲存體帳戶](#attach-storage-account-using-sas)： 管理屬於 tooanother Azure 訂用帳戶使用共用的存取簽章 (SAS) 存放裝置資源。
* [使用 SAS 會將服務附加](#attach-service-using-sas)： 管理使用 SAS 所屬 tooanother Azure 訂用帳戶特定的儲存體服務 （blob 容器、 佇列或資料表）。

## <a name="connect-tooan-azure-subscription"></a>連接 tooan Azure 訂用帳戶
> [!NOTE]
> 如果您沒有 Azure 帳戶，可以[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。
>
>

1. 在儲存體 Explorer (預覽) 中，選取 [Azure 帳戶設定] 。

    ![Azure 帳戶設定][0]

2. hello 左的窗格會顯示您已登入的所有 hello Microsoft 帳戶。 tooconnect tooanother 帳戶，請選取**將帳戶加入**，然後依照 hello 指示 toosign 使用至少一個有效的 Azure 訂閱相關聯的 Microsoft 帳戶。

    >[!NOTE]
    >目前不支援連接 toonational Azure （例如 Azure 德國、 Azure 政府和透過登入 Azure China）。 請參閱 hello"附加或卸離外部儲存體帳戶 」 一節以取得如何 tooconnect toonational Azure 儲存體帳戶。

3. 之後您已成功使用登入 Microsoft 帳戶，hello 左窗格中會填入 hello 與該帳戶相關聯的 Azure 訂用帳戶。 選取 hello Azure 訂用帳戶，您想 toowork，然後選取**套用**。 (選取**所有訂用帳戶**切換選取所有或無 hello 列出 Azure 訂用帳戶。)

    ![選取 Azure 訂用帳戶][3]  
    hello 左的窗格會顯示 hello 與 hello 選取 Azure 訂用帳戶相關聯的儲存體帳戶。

    ![已選取的 Azure 訂用帳戶][4]

## <a name="connect-tooan-azure-stack-subscription"></a>連接 tooan 堆疊 Azure 訂用帳戶

如需連接 tooan 堆疊 Azure 訂用帳戶資訊，請參閱[連接儲存體總管 tooan 堆疊 Azure 訂用帳戶](azure-stack/azure-stack-storage-connect-se.md)。

## <a name="work-with-local-development-storage"></a>使用本機開發儲存體
使用儲存體總管 （預覽），您可以對本機儲存體使用處理 hello Azure 儲存體模擬器。 這種方法可讓您撰寫的程式碼和測試儲存區，而不一定需要在 Azure 上部署儲存體帳戶，因為 hello 儲存體帳戶正在模擬的 hello Azure 儲存體模擬器。

> [!NOTE]
> 目前只適用於 Windows 支援 hello Azure 儲存體模擬器。
>
>

1. 在 hello 的儲存體總管 （預覽） 的左窗格中展開 hello **（本機及附加）** > **儲存體帳戶** > **（開發）**節點。

    ![本機開發節點][21]

2. 如果您尚未安裝 hello Azure 儲存體模擬器，您必須提示的 toodo 是透過資料列。 如果顯示 hello 資訊列，選取**最新版本的下載 hello**，然後再安裝 hello 模擬器。

    ![下載 Azure 儲存體模擬器提示字元][22]

3. Hello 模擬器安裝之後，您可以建立和使用本機 blob、 佇列和資料表。 toolearn toowork 與每個儲存體帳戶的型別，請參閱 hello 下列其中一種：

    * [管理 Azure Blob 儲存體資源](vs-azure-tools-storage-explorer-blobs.md)
    * 管理 Azure 檔案共用儲存體資源：敬請期待 
    * 管理 Azure 佇列儲存體資源：敬請期待 
    * 管理 Azure 表格儲存體資源：敬請期待 

## <a name="attach-or-detach-an-external-storage-account"></a>附加或卸離外部儲存體帳戶
使用儲存體總管 （預覽），您可以附加 tooexternal 儲存體帳戶，因此可以輕鬆地共用儲存體帳戶。 本章節將說明如何 tooattach too(and detach from) 外部儲存體帳戶。

### <a name="get-hello-storage-account-credentials"></a>取得 hello 儲存體帳戶認證
tooshare 外部儲存體帳戶，hello 該帳戶擁有者必須先取得 hello 帳戶 （帳戶名稱和金鑰） 的 hello 認證並再想 tooattach toothat （外部） 帳戶的 hello 人員分享相關資訊。 您可以藉由 hello 下列取得 hello 儲存體帳戶認證，透過 hello Azure 入口網站：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 選取 [瀏覽] 。

3. 選取 [儲存體帳戶] 。

4. 在 hello**儲存體帳戶**刀鋒視窗中，選取所需的 hello 儲存體帳戶。

5. 在 hello**設定**hello 刀鋒視窗選取儲存體帳戶中，選取**存取金鑰**。

    ![存取金鑰選項][5]

6. 在 hello**存取金鑰**刀鋒視窗，複製 hello**儲存體帳戶名稱**和**key1**附加 toohello 儲存體帳戶時使用的值。

    ![存取金鑰][6]

### <a name="attach-tooan-external-storage-account"></a>附加 tooan 外部儲存體帳戶
tooattach tooan 外部儲存體帳戶，您需要 hello 帳戶名稱和金鑰。 hello < Get hello 儲存體帳戶認證 > 一節說明這些值從 tooobtain hello Azure 入口網站的方式。 不過，在 hello 入口網站，hello 帳戶金鑰稱為**key1**。 因此在儲存體總管 （預覽） 要求的帳戶金鑰時，您輸入 hello **key1**值。

1. 在儲存體總管 （預覽） 中，選取**tooAzure 存放裝置連線**。

    ![連接 tooAzure 儲存體選項][23]

2. 在 hello**連接 tooAzure 儲存體**對話方塊方塊中，指定 hello 帳號金鑰 (hello **key1** hello Azure 入口網站中的值)，然後選取**下一步**。

    > [!NOTE]
    > 國家 （地區) 在 Azure 上，您可以從儲存體帳戶輸入 hello 儲存體連接字串。 例如，tooconnect tooAzure 德國儲存體帳戶，請輸入連接字串類似 toohello 下列： 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >您可以取得 hello 連接字串從 hello Azure 入口網站中 hello 相同方式中所述 hello 「 取得 hello 儲存體帳戶認證 」 一節。

    ![連接 tooAzure 儲存對話方塊][24]

3. 在 hello**附加外部儲存體**對話方塊中的，在 hello**帳戶名稱**方塊、 輸入 hello 儲存體帳戶名稱，指定所需的設定，，然後選取**下一步**。

    ![連結外部儲存體對話方塊][8]

4. 在 hello**連接摘要**對話方塊方塊中，確認 hello 資訊。 如果您想要 toochange 任何項目，選取**回**並重新輸入所需的 hello 設定。 

5. 選取 [ **連接**]。

6. 已成功連接之後，會顯示 hello 外部儲存體帳戶**（外部）**附加 toohello 儲存體帳戶名稱。

    ![結果的連接 tooan 外部儲存體帳戶][9]

### <a name="detach-from-an-external-storage-account"></a>從外部儲存體帳戶卸離
1. 以滑鼠右鍵按一下您想 toodetach，，然後選取 hello 外部儲存體帳戶**卸離**。

    ![中斷與儲存體選項的連結][10]

2. 在 hello 確認訊息中，選取 **是**tooconfirm hello 中斷連結，從 hello 外部儲存體帳戶。

## <a name="attach-a-storage-account-by-using-an-sas"></a>使用 SAS 連結儲存體帳戶
[SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md)讓 hello 而不需要 tooprovide Azure 訂用帳戶認證授與的暫時存取 tooa 儲存體帳戶的 Azure 訂用帳戶管理員。

tooillustrate 此案例中，讓我們說該使用者 a 是系統管理員的 Azure 訂用帳戶，而且 UserA 想 tooallow UserB tooaccess 有限的時間以特定的權限的儲存體帳戶：

1. UserA 會產生 SAS （組成 hello hello 儲存體帳戶的連接字串） 特定的時間週期並以 hello 所需的權限。

2. UserA 共用 hello 與 hello 人 (在我們的範例使用者 b)，並想要存取 toohello 儲存體帳戶的 SAS。  

3. 使用者 b 會使用儲存體總管 （預覽） tooattach toohello 帳戶屬於 tooUserA 使用 hello 提供 SAS。

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>您想要 tooshare hello 帳戶取得 SAS
1. 在儲存體總管 （預覽） 中，以滑鼠右鍵按一下 hello 儲存體帳戶共用，然後再選取您想**取得共用存取簽章**。

    ![取得 SAS 內容功能表選項][13]

2. 在 hello**共用存取簽章**對話方塊方塊中，指定 hello 時間範圍，以及您想要用於 hello 帳戶，然後選取的權限**建立**。

    ![取得 SAS 對話方塊][14]  
    hello**共用存取簽章** 對話方塊隨即開啟並顯示 hello SAS。

3. 下一步 toohello**連接字串**，選取**複製**toocopy 它 toohello 剪貼簿，然後選取**關閉**。

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>使用 hello SAS 附加 toohello 共用帳戶
1. 在儲存體總管 （預覽） 中，選取**tooAzure 存放裝置連線**。

    ![連接 tooAzure 儲存體選項][23]

2. 在 hello**連接 tooAzure 儲存體**對話方塊中，指定 hello 連接字串，然後再選取**下一步**。

    ![連接 tooAzure 儲存對話方塊][24]

3. 在 hello**連接摘要**對話方塊方塊中，確認 hello 資訊。 toomake 變更選取**回**，然後輸入您想要的 hello 設定。 

4. 選取 [ **連接**]。

5. 附加之後，會顯示 hello 儲存體帳戶**(SAS)**附加 toohello 您提供的帳戶名稱。

    ![使用 SAS 附加的 tooan 帳戶的結果][17]

## <a name="attach-a-service-by-using-an-sas"></a>使用 SAS 連結服務
hello < 使用 SAS 附加儲存體帳戶 > 一節將說明如何為 Azure 訂用帳戶系統管理員可以授與的暫時存取 tooa 儲存體帳戶產生及共用 SAS hello 儲存體帳戶。 同樣地，可以針對儲存體帳戶內的特定服務 (Blob 容器、佇列或資料表) 產生 SAS。  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>產生 SAS，使您想 tooshare hello 服務
在此情況下，服務可以是 Blob 容器、佇列或資料表。 toogenerate hello SAS 列出的服務，請參閱：

* [取得 blob 容器的 SAS hello](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* 取得檔案共用中的 hello SAS:*即將推出*
* 取得佇列中的 hello SAS:*即將推出*
* 取得資料表中的 hello SAS:*即將推出*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>附加服務，方法是使用 hello SAS toohello 共用帳戶
1. 在儲存體總管 （預覽） 中，選取**tooAzure 存放裝置連線**。

    ![連接 tooAzure 儲存體選項][23]

2. 在 hello**連接 tooAzure 儲存體**對話方塊中，指定 hello SAS URI，然後再選取**下一步**。

    ![連接 tooAzure 儲存對話方塊][24]

3. 在 hello**連接摘要**對話方塊方塊中，確認 hello 資訊。 toomake 變更選取**回**，然後輸入您想要的 hello 設定。 

4. 選取 [ **連接**]。

5. 附加之後，hello 新附加的服務下顯示 hello **(服務 SAS)**節點。

    ![使用 SAS 附加 tooa 共用服務的結果][20]

## <a name="search-for-storage-accounts"></a>搜尋儲存體帳戶
如果您有一長串的儲存體帳戶時，快速 toolocate 特定儲存體帳戶是在 hello hello 左窗格頂端 toouse hello 搜尋 方塊。

當您輸入 hello [搜尋] 方塊中，hello 左窗格中會顯示符合您輸入向上 toothat 點 hello 搜尋值的 hello 儲存體帳戶。 例如，搜尋所有儲存體帳戶名稱包含**tarcher** hello 下列螢幕擷取畫面所示：

![儲存體帳戶搜尋][11]

## <a name="next-steps"></a>後續步驟
* [使用儲存體總管 (預覽) 來管理 Azure Blob 儲存體資源](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
