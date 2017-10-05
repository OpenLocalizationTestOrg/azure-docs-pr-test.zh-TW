---
title: "Azure 儲存體帳戶清單"
description: "使用 Azure Toolkit for Eclipse 來管理您的儲存體帳戶設定"
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
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a>Azure 儲存體帳戶清單
Azure 儲存體帳戶可讓下載位置用於您的 JDK、應用程式伺服器和任意元件，以及在使用快取時用於儲存狀態。 Eclipse 維護一份已知儲存體帳戶清單，可供 Eclipse 工作區中的專案使用。 若要在 Eclipse 內開啟用來管理該清單的 [儲存體帳戶] 對話方塊，請依序按一下 [視窗] 和 [喜好設定]，展開 [Azure]，然後按一下 [儲存體帳戶]。

下圖顯示 [儲存體帳戶]  對話方塊。

![][ic719496]

您也可以在使用儲存體帳戶的下列對話方塊上，從 [帳戶]  連結開啟這個對話方塊：

* [伺服器組態] 對話方塊的 [JDK] 索引標籤。
* [伺服器組態] 對話方塊的 [伺服器] 索引標籤。
* [加入元件]  對話方塊。
* [快取]  屬性對話方塊。

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a>使用發行設定檔匯入您的儲存體帳戶
1. 在 [儲存體帳戶] 對話方塊中，按一下 [從發佈設定檔匯入]。

2. (如果您已將發行設定檔儲存至本機電腦，則略過這個步驟)。在 [匯入訂用帳戶資訊] 對話方塊中，按一下 [下載發佈設定檔]。 如果您尚未登入 Azure 帳戶，系統會提示您登入。 然後會提示您儲存 Azure 發行設定檔 (您可以忽略登入頁面上所顯示的產生指示，這是由 Azure 入口網站提供給 Visual Studio 使用者的指示)。請將其儲存至本機電腦。

3. 同樣在 [匯入訂用帳戶資訊] 對話方塊中，按一下 [瀏覽] 按鈕，選取您先前在本機儲存的發佈設定檔，然後按一下 [開啟]。

4. 按一下 [確定] 關閉 [匯入訂用帳戶資訊] 對話方塊。

## <a name="to-create-a-new-storage-account"></a>建立新的儲存體帳戶
1. 在 [儲存體帳戶] 對話方塊中，按一下 [新增]。

2. 在 [新增儲存體帳戶] 對話方塊中，按一下 [新增]。

3. 在 [新增儲存體帳戶]  對話方塊中，指定下列值：

   * 儲存體帳戶名稱。

   * 儲存體帳戶的位置。

   * 儲存體帳戶的描述。

   * 儲存體帳戶所屬的訂用帳戶。

4. 按一下 [確定] 關閉 [新增儲存體帳戶] 對話方塊。

建立儲存體帳戶可能需要幾分鐘的時間。 建立後，請按一下 [確定] 關閉 [新增儲存體帳戶] 對話方塊，新的儲存體帳戶會新增至可用的儲存體帳戶清單。

## <a name="to-add-an-existing-storage-account-to-the-list"></a>將現有的儲存體帳戶加入清單中
1. 如果您還沒有 Azure 儲存體帳戶，請遵循上一節＜建立新的儲存體帳戶＞  中所列的步驟，建立一個帳戶。 (您也可以在 [Azure 管理入口網站][Azure Management Portal]中建立新的儲存體帳戶)。

2. 在 [儲存體帳戶] 對話方塊中，按一下 [新增]。

3. 在 [新增儲存體帳戶] 對話方塊中，輸入 [名稱] 和 [存取金鑰] 的值。 這必須是現有 Azure 儲存體帳戶的帳戶名稱和存取金鑰。 請使用 [Azure 管理入口網站][Azure Management Portal]的 [儲存體] 區段，來檢視您的儲存體帳戶名稱和金鑰。 您的 [加入儲存體帳戶]  對話方塊將會類似如下。
   
   ![][ic719497]

4. 按一下 [確定] 關閉 [新增儲存體帳戶] 對話方塊。

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a>修改儲存體帳戶以使用新的存取金鑰
1. 在 [儲存體帳戶] 對話方塊中，按一下您要編輯的儲存體帳戶，然後按一下 [編輯]。

2. 在 [編輯儲存體帳戶存取金鑰] 對話方塊中，修改 [存取金鑰] 值。

3. 按一下 [確定] 關閉 [編輯儲存體帳戶存取金鑰] 對話方塊。

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a>從 Eclipse 所維護的清單中移除儲存體帳戶
1. 在 [儲存體帳戶] 對話方塊中，按一下您要編輯的儲存體帳戶，然後按一下 [移除]。

2. 出現提示時，按一下 [確定]  以移除儲存體帳戶。

> [!NOTE]
> 透過 [儲存體帳戶] 對話方塊移除儲存體帳戶，只會將其從可在 Eclipse 中檢視的儲存體帳戶清單中移除， 而不會從您的 Azure 訂用帳戶中移除此儲存體帳戶。 此外，當 Eclipse 重新載入您訂用帳戶的詳細資料之後，該儲存體帳戶可能會再次出現於清單中。
> 
> 

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[安裝適用於 Eclipse 的 Azure 工具組][Installing the Azure Toolkit for Eclipse] 

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

如需有關如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
