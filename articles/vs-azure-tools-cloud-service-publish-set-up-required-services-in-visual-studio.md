---
title: "aaaPrepare toopublish 或部署 Azure 應用程式從 Visual Studio |Microsoft 文件"
description: "了解雲端和儲存體帳戶服務的 hello 程序 tooset 和設定 Azure 應用程式。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>準備 tooPublish 或部署 Azure 應用程式從 Visual Studio
## <a name="overview"></a>概觀
您可以發行雲端服務專案之前，您必須設定下列服務的 hello:

* A**雲端服務**toorun 您 hello Azure 環境中的角色
* A**儲存體帳戶**toohello Blob、 佇列和表格服務提供存取。

使用下列程序 tooset 這些服務的 hello 並設定您的應用程式

## <a name="create-a-cloud-service"></a>建立雲端服務
toopublish 雲端服務 tooAzure，您必須先建立雲端服務，在 hello Azure 環境中執行您的角色。 您可以建立雲端服務中 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)hello > 一節所述， **toocreate 雲端服務，方法是使用 hello Azure 傳統入口網站**稍後在本主題中。 您也可以使用 hello 發佈精靈 」，在 Visual Studio 中建立雲端服務。

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate 雲端服務，方法是使用 Visual Studio
1. 開啟 hello hello Azure 專案的捷徑功能表並選擇 **發行**。

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. 如果您尚未登入，hello Microsoft 帳戶或與您 Azure 訂用帳戶相關聯的組織帳戶登入您的使用者名稱和密碼。
3. 選擇 hello**下一步**按鈕 tooadvance toohello**設定**頁面。

    ![發佈精靈一般設定](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. 在 hello**雲端服務**清單中，選擇**新建**。 hello**建立 Azure 服務**對話方塊隨即出現。
5. 輸入您的雲端服務的 hello 名稱。 hello 名稱 hello 服務 URL 的一部分，因此必須是全域唯一。 hello 名稱不區分大小寫。

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate 使用 hello Azure 傳統入口網站的雲端服務
1. 登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkId=253103)hello Microsoft 網站上。
2. （選擇性） toodisplay 一份雲端服務，您已經建立，請選擇左邊 hello hello 頁面 hello 雲端服務連結。
3. 選擇 hello  **+** 圖示 hello 左下角，，然後選擇 **雲端服務**hello 出現的功能表上。 有 [快速建立] 和 [自訂建立] 兩個選項的另一個畫面會隨即出現。 如果您選擇**快速建立**，您可以建立只是藉由指定其 URL 與 hello 區域它將實際託管的雲端服務。 如果選擇 [自訂建立]，則可藉由指定封裝 (.cspkg 檔)、組態 (.cscfg) 檔和憑證，立即發佈雲端服務。 如果您使用 hello 想 toopublish 您的雲端服務，不需要自訂建立**發行**命令中的 Azure 專案。 hello**發行**hello Azure 專案的捷徑功能表上的命令為止。
4. 選擇**快速建立**toolater 使用 Visual Studio 發行雲端服務。
5. 指定雲端服務的名稱。 hello 完整的 URL 會顯示下一個 toohello 名稱。
6. 在 [hello] 清單中，選擇 hello 大部分使用者所在地區。
7. 在 hello hello 視窗底部，選擇 hello**建立雲端服務**連結。

## <a name="create-a-storage-account"></a>建立儲存體帳戶
儲存體帳戶提供 toohello Blob、 佇列和表格服務的存取。 您可以建立儲存體帳戶使用 Visual Studio 或 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkId=253103)。

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate 使用 Visual Studio 的儲存體帳戶
1. 在**方案總管 中**，開啟 hello hello 的捷徑功能表**儲存體** 節點，然後選擇 **建立儲存體帳戶**。

    ![建立新的 Azure 儲存體帳戶](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. 選取或輸入下列資訊在 hello hello 新儲存體帳戶的 hello**建立儲存體帳戶** 對話方塊。

   * hello Azure 訂用帳戶 toowhich 想 tooadd hello 儲存體帳戶。
   * 您要新增儲存體帳戶 hello toouse hello 名稱。
   * hello 地區或同質群組 （例如美國西部或東亞）。
   * hello 類型的複寫想 toouse hello 儲存體帳戶，例如 異地備援。
3. 當您完成時，選擇**建立**.hello 新儲存體帳戶會出現在 hello**儲存體**清單中**伺服器總管**。

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate 使用 hello Azure 傳統入口網站的儲存體帳戶
1. 登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkId=253103)hello Microsoft 網站上。
2. （選擇性） tooview 儲存體帳戶中，選擇 hello**儲存體**hello hello hello 頁面的左方面板中的連結。
3. 在 hello hello 頁面的左下角，選擇 hello  **+** 圖示。
4. 在 hello 出現的功能表，選擇 **儲存體**，然後選擇 **快速建立**。
5. 提供給 hello 儲存體帳戶會在唯一的 url 的名稱。
6. 提供名稱給您的雲端服務。 hello 完整的 URL 會顯示下一個 toohello 名稱。
7. 在 hello 的地區清單，選擇大部分使用者所在的區域。
8. 指定是否要讓 tooenable 地理複寫。 如果您啟用地理複寫，您的資料將儲存在多個實體位置 tooreduce hello 遺失的可能性。 這項功能，讓存放裝置更耗費資源，但您可以藉由啟用地理位置，當您建立 hello 儲存體帳戶，而不是稍後加入 hello 功能降低 hello 成本。 如需詳細資訊，請參閱 [異地複寫](http://go.microsoft.com/fwlink/?LinkId=253108)。
9. 在 hello hello 視窗底部，選擇 hello**建立儲存體帳戶**連結。

建立儲存體帳戶之後，您會看到 hello Url，您可以使用 tooaccess 資源中每個 hello Azure 儲存體服務，並也為您的帳戶 hello 主要和次要存取金鑰。 您可以使用這些金鑰 tooauthenticate 對 hello 儲存體服務提出的要求。

> [!NOTE]
> hello 次要存取金鑰提供的 hello 相同存取 tooyour 為 hello 主要存取金鑰的儲存體帳戶，且會產生備份為您的主要存取金鑰被盜用。 此外，建議您定期重新產生存取金鑰。 您可以修改連接字串設定 toouse hello 次要索引鍵時重新產生 hello 主索引鍵，則您可以修改它 toouse hello 重新產生主索引鍵時重新產生 hello 次要金鑰。
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>設定您的應用程式的 toouse 服務 hello 儲存體帳戶提供
您必須設定存取儲存體服務 toouse hello Azure 儲存體服務所建立的任何角色。 toodo，您可以使用多個服務組態，Azure 專案。 根據預設，兩者都會建立在您的 Azure 專案中。 藉由使用多個服務組態，您可以使用相同的連接字串中您的程式碼，但每個服務組態中有不同的連接字串值的 hello。 例如，使用一個服務組態 toorun，並使用在本機的 hello Azure 儲存體模擬器和不同的服務組態 toopublish 應用程式偵錯應用程式 tooAzure。 如需服務組態的詳細資訊，請參閱 [使用多個服務組態設定 Azure 專案](vs-azure-tools-multiple-services-project-configurations.md)。

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>tooconfigure hello 儲存體帳戶您應用程式 toouse 服務提供
1. 在 Visual Studio 中開啟您的 Azure 方案。 在 [方案總管] 中，開啟 Azure 專案存取 hello 儲存體服務中的 hello 每個角色的捷徑功能表並選擇**屬性**。 Hello hello 角色名稱的頁面會顯示 hello Visual Studio 編輯器中。 hello 頁面會顯示 hello hello 欄位**組態** 索引標籤。
2. 在 hello hello 角色的屬性頁，選擇 **設定**。
3. 在 hello**服務組態**清單中，選擇您想 tooedit hello hello 服務組態名稱。 如果您想 toomake 變更 tooall 的 hello 這個角色的服務組態，您可以選擇**所有組態**。  如需有關如何 tooupdate 服務組態的詳細資訊，請參閱 hello 節**管理儲存體帳戶的連接字串**hello 主題[設定 Visual Studio 中的 Azure 雲端服務的 hello 角色](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify 任何連接字串設定中，選擇 hello **...** 下一個 toohello 設定 按鈕。 hello**建立儲存體連接字串** 對話方塊隨即出現。
5. 在下**連接使用**，選擇 hello**訂用帳戶**選項。
6. 在 hello**訂用帳戶**清單中，選擇您的訂用帳戶。 如果訂閱 hello 清單不包含您想要的其中一個 hello，選擇 hello**下載發行設定**連結。
7. 在 hello**帳戶名稱**清單中，選擇您的儲存體帳戶名稱。 Azure Tools 會使用 hello.publishsettings 檔案自動取得儲存體帳戶認證。 儲存體帳戶認證，手動 toospecify 選擇 hello**手動輸入的認證**選項，然後再繼續此程序。 您可以從 hello 取得您的儲存體帳戶名稱及主要金鑰[Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。 如果您不想 toospecify 您的儲存體帳戶設定手動選擇 hello**確定**按鈕 tooclose hello 對話方塊。
8. 選擇 hello**輸入儲存體帳戶**認證連結。
9. 在 hello**帳戶名稱**方塊中，輸入 hello 您的儲存體帳戶名稱。

   > [!NOTE]
   > 登入 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，然後選擇 [hello**儲存體**] 按鈕。 hello 入口網站會顯示儲存體帳戶清單。 如果您選擇帳戶，其頁面就會開啟。 您可以從這個頁面複製 hello hello 儲存體帳戶名稱。 如果您使用舊版的 hello 傳統入口網站，您的儲存體帳戶的 hello 名稱會出現在 hello**儲存體帳戶**檢視。 toocopy 這命名時，反白顯示在 hello**屬性**這個視窗檢視，，然後選擇 hello Ctrl + C 鍵。 Visual studio，toopaste hello 名稱，請選擇 hello**帳戶名稱**文字] 方塊中，然後選擇 [hello Ctrl + V 鍵。
   >
   >
10. 在 hello**帳戶金鑰**方塊中，輸入您的主要金鑰，或複製並貼上它 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
     toocopy 此索引鍵：

    1. 在 hello hello 適當的儲存體帳戶的 hello 頁面底部，選擇 [hello**管理金鑰**] 按鈕。
    2. 在 hello**管理存取金鑰**頁面、 選取 hello 主要存取金鑰的 hello 文字，然後選擇 hello Ctrl + C 鍵。
    3. Azure Tools 中將 hello 金鑰貼至 hello**帳戶金鑰**方塊。
    4. 您必須選取其中一個 hello 遵循選項 toodetermine hello 服務存取 hello 儲存體帳戶的方式：

       * **使用 HTTP**。 這是 hello 標準選項。 例如： `http://<account name>.blob.core.windows.net`。
       * **使用 HTTPS** ，以確保連線安全無虞。 例如： `https://<accountname>.blob.core.windows.net`。
       * **指定自訂端點**為每個 hello 三個服務。 然後您可以將這些端點輸入特定服務的 hello hello 欄位。

         > [!NOTE]
         > 如果您建立自訂端點，您可以建立更複雜的連接字串。 當您使用這個字串格式時，您可以指定包含您已註冊儲存體帳戶以 hello Blob 服務的自訂網域名稱的儲存體服務端點。 也您可以授與存取只有 tooblob 透過共用的存取簽章的單一容器中的資源。 如需有關如何 toocreate 自訂端點，請參閱[設定 Azure 儲存體連接字串](storage/common/storage-configure-connection-string.md)。
         >
         >
11. toosave 這些變更的連接字串，選擇 hello**確定**按鈕，然後選擇 hello**儲存**hello 工具列上的按鈕。 您儲存這些變更之後，您可以使用程式碼中取得 hello 值，這個連接字串的[GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx)。 當您發行應用程式 tooAzure 時，選擇包含 hello 連接字串 hello Azure 儲存體帳戶的 hello 服務組態。 發行您的應用程式之後，請確認 hello 應用程式的運作，如預期般對 hello Azure 儲存體服務

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解發行應用程式 tooAzure 從 Visual Studio，請參閱[發行雲端服務使用 hello Azure Tools](vs-azure-tools-publishing-a-cloud-service.md)。
