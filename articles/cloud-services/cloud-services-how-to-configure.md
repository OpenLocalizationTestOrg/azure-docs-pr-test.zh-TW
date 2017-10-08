---
title: "aaaHow tooconfigure 雲端服務 （傳統入口網站） |Microsoft 文件"
description: "了解 tooconfigure 雲端服務在 Azure 中的方式。 了解 tooupdate hello 雲端服務組態和設定遠端存取 toorole 執行個體。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>如何 tooConfigure 雲端服務
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-how-to-configure-portal.md)
> * [Azure 傳統入口網站](cloud-services-how-to-configure.md)
> 
> 

您可以在 hello Azure 傳統入口網站中設定雲端服務的 hello 最常使用的設定。 或者，如果您喜歡 tooupdate 組態檔直接下載服務組態檔 tooupdate 」，然後上傳與 hello 組態變更的 hello 更新檔案和更新 hello 雲端服務。 無論如何，hello 組態更新推入 tooall 角色執行個體。

hello Azure 傳統入口網站也可讓您太[Azure 雲端服務中的角色啟用遠端桌面連線](cloud-services-role-enable-remote-desktop.md)

Azure 才能確保服務 99.95%的可用性期間 hello 組態更新如果您有針對每個角色至少兩個角色執行個體。 可讓一個虛擬機器 tooprocess 用戶端要求而正在更新其他 hello。 如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。

## <a name="change-a-cloud-service"></a>變更雲端服務
1. 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**設定**。
   
    ![Configuration Page](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    在 [hello**設定**] 頁面上，您可以設定監視之後，更新角色設定，並選擇 hello 客體作業系統和角色執行個體的系列。 
2. 在**監視**，監視層級 tooVerbose 組 hello 或最小，並設定所需的詳細資訊監視 hello 診斷連接字串。
3. 對於服務角色 （根據角色分組），您可以更新 hello 下列設定：
   
    * **設定**修改 hello 中所指定的其他組態設定的 hello 值*ConfigurationSettings* hello 服務組態 (.cscfg) 檔的項目。

    * **憑證**  
        變更用於 SSL 加密為角色的 hello 憑證指紋。 toochange 憑證，您必須先上傳 hello 新憑證 (在 hello**憑證**頁面)。 接著，更新顯示 hello 角色設定中的 hello 憑證字串中的 hello 指紋。
4. 在**作業系統**，您可以變更 hello 作業系統系列或版本，角色執行個體，或選擇**自動**tooenable 的 hello 目前作業系統版本的自動更新。 hello 作業系統設定套用 tooweb 角色和背景工作角色，但不是會影響虛擬機器。
   
    在部署期間，hello 最新的作業系統版本安裝在所有角色執行個體，而且 hello 作業系統預設會自動更新。 
   
    如果您需要針對您在不同的作業系統版本上的雲端服務 toorun 因為相容性需求，所以您的程式碼中，您可以選擇的作業系統系列和版本。 當您選擇使用特定作業系統版本時，就會暫停作業系統自動更新為 hello 雲端服務。 您將需要 tooensure hello 作業系統接收更新。
   
    如果您解決所有應用程式具有 hello 最新的作業系統版本的相容性問題，您可以啟用作業系統自動更新設定 hello 作業系統版本太**自動**。 
   
    ![OS Settings](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave 您的組態設定，並將其推送 toohello 角色執行個體，請按一下**儲存**。 (按一下**捨棄**toocancel hello 變更。)**儲存**和**捨棄**變更設定之後才加入 toohello 命令列。

## <a name="update-a-cloud-service-configuration-file"></a>更新雲端服務組態檔
1. 下載雲端服務組態檔 (.cscfg) hello 目前的組態。 在 hello**設定**hello 雲端服務頁面上，按一下**下載**。 然後按一下 **儲存**，或按一下**存**toosave hello 檔案。
2. 更新 hello 服務組態檔之後，請上傳，並套用 hello 組態更新：
   
   1. 在 hello**設定**頁面上，按一下**上傳**。
      
       ![Upload Configuration](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. 在**組態檔**，使用**瀏覽**tooselect hello 更新.cscfg 檔案。
   3. 如果您的雲端服務包含只有一個執行個體的任何角色，選取 hello**套用設定，即使一個或多個角色包含單一執行個體**核取方塊的 hello 角色 tooproceed tooenable hello 組態更新。
      
       除非每個角色都定義至少兩個執行個體，否則 Azure 無法保證雲端服務在服務組態更新期間至少有 99.95% 的可用性。 如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。
   4. 按一下 [確定]  \(勾選記號)。 

## <a name="next-steps"></a>後續步驟
* 了解如何太[部署雲端服務](cloud-services-how-to-create-deploy.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。
* [管理您的雲端服務](cloud-services-how-to-manage.md)。
* [啟用 Azure 雲端服務中角色的遠端桌面連線](cloud-services-role-enable-remote-desktop.md)
* 設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。

