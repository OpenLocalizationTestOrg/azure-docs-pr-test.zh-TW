---
title: "aaaAzure 儲存體帳戶清單"
description: "管理您使用 hello Azure Toolkit for Eclipse 的儲存體帳戶設定"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Azure 儲存體帳戶清單
Azure 儲存體帳戶可讓下載位置 toobe 用於您的 JDK、 應用程式伺服器和任意元件，以及使用快取時儲存狀態。 Eclipse 會維護一份您 Eclipse 工作區中的可用 tooyour 專案已知的儲存體帳戶。 tooopen hello**儲存體帳戶**對話方塊中，也就是使用的 toomanage 的清單，在 Eclipse 中，按一下**視窗**，按一下 **喜好設定**，依序展開**Azure**，然後按一下**儲存體帳戶**。

hello 下列範例示範 hello**儲存體帳戶**對話方塊。

![][ic719496]

此對話方塊也可以從開啟**帳戶**連結上使用儲存體帳戶，例如 hello 下列對話方塊：

* hello **JDK**  索引標籤的 hello**伺服器組態**對話方塊。
* hello**伺服器** 索引標籤的 hello**伺服器組態**對話方塊。
* hello**加入元件**對話方塊。
* hello**快取**屬性 對話方塊。

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>您的儲存體帳戶使用 tooimport 的發行設定檔
1. 在 [hello**儲存體帳戶**] 對話方塊中，按一下**從 PUBLISH-SETTINGS 檔案匯入**。

2. （如果略過此步驟中已儲存發行設定檔案 tooyour 本機電腦。）在 hello**匯入訂用帳戶資訊** 對話方塊中，按一下 **下載發行設定檔案**。 如果尚未登入您的 Azure 帳戶，您將會提示的 toolog 中。 然後系統會提示您 toosave Azure 發行設定檔。 （您可以忽略 hello hello 登入頁面-上顯示的結果指示他們所提供的 hello Azure 入口網站和適用於 Visual Studio 使用者。）將它儲存 tooyour 本機電腦。

3. 仍在 hello**匯入訂用帳戶資訊** 對話方塊中，按一下 hello**瀏覽**按鈕、 選取 hello 發行設定檔，您先前儲存在本機，，然後按一下**開啟**.

4. 按一下**確定**tooclose hello**匯入訂用帳戶資訊**對話方塊。

## <a name="toocreate-a-new-storage-account"></a>toocreate 新的儲存體帳戶
1. 在 [hello**儲存體帳戶**] 對話方塊中，按一下**新增**。

2. 在 [hello**新增儲存體帳戶**] 對話方塊中，按一下**新增**。

3. Hello 內**新儲存體帳戶** 對話方塊中，指定的 hello 下列值：

   * 儲存體帳戶名稱。

   * Hello 儲存體帳戶的位置。

   * Hello 儲存體帳戶的描述。

   * 所屬 hello 訂用帳戶 toowhich hello 儲存體帳戶。

4. 按一下**確定**tooclose hello**新儲存體帳戶**對話方塊。

可能需要您建立的儲存體帳戶 toobe 幾分鐘的時間。 建立之後，請按一下**確定**tooclose hello**新增儲存體帳戶** 對話方塊中，新的儲存體帳戶將會新增 toohello 可用的儲存體帳戶清單。

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>tooadd 現有的儲存體帳戶 toohello 清單
1. 如果您還沒有 Azure 儲存體帳戶，來建立 hello 步驟中列出 hello **toocreate 新的儲存體帳戶區段**上方。 (或者，您可以建立新的儲存體帳戶在 hello [Azure 管理入口網站][Azure Management Portal]。)

2. 在 [hello**儲存體帳戶**] 對話方塊中，按一下**新增**。

3. Hello 內**新增儲存體帳戶** 對話方塊中，輸入的值**名稱**和**便捷鍵**。 hello 帳戶名稱和存取金鑰必須是現有的 Azure 儲存體帳戶。 使用 hello**儲存體**區段 hello [Azure 管理入口網站][ Azure Management Portal] tooview 儲存體帳戶名稱和金鑰。 您**新增儲存體帳戶**對話方塊看起來類似 toohello 下列。
   
   ![][ic719497]

4. 按一下**確定**tooclose hello**新增儲存體帳戶**對話方塊。

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>新的存取金鑰的儲存體帳戶 toouse toomodify
1. 在 [hello**儲存體帳戶**] 對話方塊中，按一下您想 tooedit，然後按一下 hello 儲存體帳戶**編輯**。

2. 在 [hello**編輯儲存體帳戶存取金鑰**] 對話方塊中，修改 hello**便捷鍵**值。

3. 按一下**確定**tooclose hello**編輯儲存體帳戶存取金鑰**對話方塊。

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>在 Eclipse 中維護的 tooremove hello 清單中的儲存體帳戶
1. 在 [hello**儲存體帳戶**] 對話方塊中，按一下您想 tooedit，然後按一下 hello 儲存體帳戶**移除**。

2. 按一下**確定**時提示的 tooremove hello 儲存體帳戶。

> [!NOTE]
> 移除 hello 儲存體帳戶，透過 hello**儲存體帳戶**對話方塊只會移除它從 hello 可在 Eclipse 內檢視的儲存體帳戶清單。 它不會從 Azure 訂用帳戶移除 hello 儲存體帳戶。 此外，hello 儲存體帳戶可能會再次出現在清單中後 Eclipse 重新載入您訂用帳戶的 hello 詳細資料。
> 
> 

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
