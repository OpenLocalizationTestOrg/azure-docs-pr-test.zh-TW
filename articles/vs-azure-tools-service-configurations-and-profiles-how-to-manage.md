---
title: "aaaHow toomanage 服務組態和設定檔 |Microsoft 文件"
description: "深入了解如何與服務組態和設定檔組態檔 toowork |儲存 hello 部署環境的設定，以及發行雲端服務的設定。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>如何 toomanage 服務組態和設定檔
## <a name="overview"></a>概觀
當您發佈雲端服務時，Visual Studio 會將組態資訊儲存在兩種組態檔中：服務組態和設定檔。 服務組態 （.cscfg 檔） 儲存 Azure 雲端服務的 hello 部署環境設定。 Azure 會在管理雲端服務時使用這些組態檔。 在 hello 另一方面，設定檔 （.azurePubxml 檔案） 存放區發行雲端服務的設定。 這些設定會記錄您選擇的內容時使用 hello 發行精靈 中，並在本機將供 Visual Studio。 本主題說明如何 toowork 與這兩種類型的組態檔。

## <a name="service-configurations"></a>服務組態
您可以建立多個服務組態 toouse 每個部署環境。 例如，您可以建立 hello 本機環境 toorun，並針對生產環境中測試 Azure 應用程式與另一個服務組態的服務組態。

您可以根據需求來新增、刪除、重新命名和修改這些服務組態。 Hello 下列圖例所示，您可以從 Visual Studio 中，管理這些服務組態。

![管理服務組態](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

您也可以開啟 hello**管理組態**從 hello 角色屬性頁 對話方塊。 在 Azure 專案中，角色 tooopen hello 屬性開啟 hello 該角色的捷徑功能表，然後選擇**屬性**。 在 hello**設定**索引標籤上，依序展開 hello**服務組態**清單，然後再選取**管理**tooopen hello**管理組態** 對話方塊。

### <a name="tooadd-a-service-configuration"></a>tooadd 服務組態
1. 在 方案總管 中，開啟 hello hello Azure 專案的捷徑功能表，然後選取**管理組態**。
   
    hello**管理服務組態** 對話方塊隨即出現。
2. tooadd 服務組態，您必須建立一份現有的組態。 toodo，選擇您想 toocopy 從 hello 名稱清單，然後選取 hello 組態**建立複本**。
3. （選擇性） toogive hello 服務設定不同的名稱，從 hello 名稱清單中選擇 hello 新的服務組態，然後選取**重新命名**。 在 hello**名稱**文字方塊中，您想 toouse 此服務組態，然後選取型別 hello 名稱**確定**。
   
    名為 Serviceconfiguration.< 新服務組態檔。[新的名稱].cscfg toohello Azure 專案加入方案總管] 中。

### <a name="toodelete-a-service-configuration"></a>toodelete 服務組態
1. 在 方案總管 中，開啟 hello hello Azure 專案的捷徑功能表，然後選取**管理組態**。
   
    hello**管理服務組態** 對話方塊隨即出現。
2. toodelete 服務組態中，選擇 hello 設定您想從 hello toodelete**名稱**清單，然後選取 **移除**。 對話方塊隨即出現 tooverify 您想 toodelete 這項設定。
3. 選取 [刪除] 。
   
     hello 服務組態檔會從 hello Azure 專案方案總管 中移除。

### <a name="toorename-a-service-configuration"></a>toorename 服務組態
1. 在 方案總管開啟 hello hello Azure 專案的捷徑功能表，然後選取**管理組態**。
   
    hello**管理服務組態** 對話方塊隨即出現。
2. toorename 服務組態中，選擇 hello 新的服務組態從 hello**名稱**清單，然後再選取**重新命名**。 在 hello**名稱**文字方塊中，您希望 toouse 這個服務組態，，然後選取型別 hello 名稱**確定**。
   
    方案總管 中的 Azure 專案時，會在 hello 變更 hello hello 服務組態檔的名稱。

### <a name="toochange-a-service-configuration"></a>toochange 服務組態
* 如果您想 toochange 服務組態，請開啟您想 toochange hello Azure 的專案中，然後選取 hello 特定角色的 hello 捷徑功能表**屬性**。 請參閱[How to： 設定 Visual Studio 中的 Azure 雲端服務的 hello 角色](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service)如需詳細資訊。

## <a name="make-different-setting-combinations-by-using-profiles"></a>使用設定檔製作不同的設定組合
使用設定檔，您可以自動填滿 hello**發行精靈**與不同的用途的不同設定組合。 例如，您可有一個設定檔用於偵錯，另一個設定檔用於發行組建。 在此情況下，您**偵錯**設定檔會有**IntelliTrace**啟用，而且 hello**偵錯**組態選取，而您**發行**設定檔會有**IntelliTrace**停用而且 hello**發行**選取的組態。 您也可以使用不同的設定檔 toodeploy 使用不同的儲存體帳戶的服務。

當您第一次執行 hello 的 hello 精靈時，會建立預設的設定檔。 Visual Studio 將 hello 設定檔儲存的檔案中，以副檔名為.azurePubXml，它會加入 tooyour Azure 專案的 hello**設定檔**資料夾。 如果您手動指定不同的選擇，日後執行 hello 精靈時，會自動更新 hello 檔案。 執行下列程序的 hello 之前，您應該已經發行您的雲端服務至少一次。

### <a name="tooadd-a-profile"></a>tooadd 設定檔
1. 開啟 Azure 專案，hello 捷徑功能表，然後選取**發行**。
2. 下一步 toohello **profile 當做目標**清單中，選取 hello**儲存設定檔**按鈕，為 hello 遵循圖所示。 這會為您建立設定檔。
   
    ![建立新的設定檔](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. 建立 hello 設定檔之後，請選取**< 管理... >**在 hello **profile 當做目標**清單。
   
    hello**管理設定檔**出現對話方塊，請為 hello 遵循圖所示。
   
    ![管理設定檔對話方塊](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. 在 hello**名稱**清單中，選擇 設定檔，並選取**建立副本**。
5. 選擇 hello**關閉** 按鈕。
   
    hello 新設定檔會出現在 hello 目標設定檔清單。
6. 在 hello **profile 當做目標**清單，您剛建立的選取 hello 設定檔。 hello 發行精靈 設定值隨即填入您所選取的 hello 設定檔 hello 選項。
7. 選取 hello**上一步**和**下一步**按鈕 toodisplay hello 發行精靈的每一頁，然後以自訂此設定檔的 hello 設定。 如需相關資訊，請參閱 [發佈 Azure 應用程式精靈](http://go.microsoft.com/fwlink/p/?LinkID=623085) 。
8. 您完成自訂 hello 設定之後，請選取**下一步**toogo 後 toohello 設定 頁面。 hello 設定檔會儲存時使用這些設定發行 hello 服務，或如果您選取**儲存**的設定檔的 下一步 toohello 清單。

### <a name="toorename-or-delete-a-profile"></a>toorename 或刪除設定檔
1. 開啟 Azure 專案，hello 捷徑功能表，然後選取**發行**。
2. 在 hello **profile 當做目標**清單中，選取**管理**。
3. 在 hello**管理設定檔**對話方塊中，選取 hello 設定檔，您想 toodelete，，然後選取**移除**。
4. 在出現 hello 確認對話方塊中，選取**確定**。
5. 選取 [關閉] 。

### <a name="toochange-a-profile"></a>toochange 設定檔
1. 開啟 Azure 專案，hello 捷徑功能表，然後選取**發行**。
2. 在 hello **profile 當做目標**清單，您想 toochange 選取 hello 設定檔。
3. 選取 hello**上一步**和**下一步**toodisplay 的每一頁 hello 發行精靈，然後變更 hello 設定您想要的按鈕。 如需相關資訊，請參閱 [發佈 Azure 應用程式精靈](http://go.microsoft.com/fwlink/p/?LinkID=623085) 。
4. 您完成變更 hello 設定之後，請選取**下一步**toogo 後 toohello**設定**頁面。
5. （選擇性） 選取**發行**toopublish hello 雲端服務使用 hello 新設定。 如果您不想的 toopublish 關閉您的雲端服務，這次，並且在 hello 發行精靈，Visual Studio 會詢問您是否要讓 toosave hello 變更 toohello 設定檔。

## <a name="next-steps"></a>後續步驟
請參閱有關設定 Azure 專案，從 Visual Studio 的其他部分 toolearn[設定 Azure 專案](http://go.microsoft.com/fwlink/p/?LinkID=623075)

