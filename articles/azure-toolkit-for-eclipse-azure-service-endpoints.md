---
title: "aaaAzure 服務端點"
description: "描述在 hello Azure Toolkit for Eclipse 中的 hello Azure 服務端點設定。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Azure 服務端點
Azure 服務端點會判斷您的應用程式是否已部署的 tooand hello 全域 Azure 平台所管理，Azure 由 21Vianet in China 或私人 Azure 平台運作。 hello**服務端點**對話方塊可讓您的服務端點想 toouse toospecify。 tooopen hello**服務端點**對話方塊中的，在 Eclipse 中，按一下**視窗**，按一下 **喜好設定**，依序展開**Azure**，然後按一下**服務端點**。 設定 hello**作用中設定**欄位會決定目前的工作區中的哪一種 Azure 服務端點會用於 hello Azure 專案。

hello 下列範例示範 hello**服務端點**對話方塊。

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>tooset hello 服務端點
在 hello**服務端點**對話方塊中，下列動作的 hello 的其中一個執行：

* 如果您想 toouse hello 全域 Azure 平台，從 hello**作用中設定**下拉式清單中選取**windowsazure.com**按一下**確定**。

* 如果您想的 toouse Azure 由 21Vianet in China 從 hello 運作**作用中設定**下拉式清單中選取**windowsazure.cn （中國）**按一下**確定**。

* 如果您想 toouse 私人 Azure 平台：

  1. 按一下 [ **編輯**]。

  2. 會開啟一個對話方塊，通知您該 hello**服務端點**會關閉對話方塊，並將開啟 hello 喜好設定設定檔。 按一下 [確定] 。

  3. 在 hello preferencesets.xml 檔案中，建立新`preferenceset`項目。 這個新的項目，對於建立`name`， `blob`， `management`，`portalURL`和`publishsettings`屬性，然後新增其對應 tooyour 私人 Azure 平台的值。 您可以使用 hello 值提供給現有的 hello`preferenceset`做為範本的項目。 **請注意**: hello 值為 hello`blob`屬性必須包含"blob"hello URL 中的 hello 文字。

  4. 儲存並關閉 preferencesets.xml。

  5. 重新開啟 hello**服務端點**對話方塊。

  6. 從 hello**作用中設定**下拉式清單中，選取 hello 作用中設定您建立，然後按一下**確定**。

  7. 一旦您已建立私人 Azure 平台`preferenceset`項目，您可以按一下 hello 變更 hello 指派值 tooit**編輯**按鈕在 hello**服務端點**對話方塊。 如有需要，也可以建立多個私人 Azure 平台 `preferenceset` 元素。

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
