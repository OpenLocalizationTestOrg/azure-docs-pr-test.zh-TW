---
title: "aaaHow toocreate 及部署雲端服務 |Microsoft 文件"
description: "深入了解如何 toocreate 及部署雲端服務在 Azure 中使用 hello 快速建立 方法。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>如何 tooCreate 及部署雲端服務
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-how-to-create-deploy-portal.md)
> * [Azure 傳統入口網站](cloud-services-how-to-create-deploy.md)
> 
> 

hello Azure 傳統入口網站提供兩種方式，讓您 toocreate 及部署雲端服務：**快速建立**和**自訂建立**。

本主題說明如何 toouse hello 快速建立新的雲端服務的方法 toocreate，然後使用**上傳**tooupload 和部署在 Azure 中的雲端服務封裝。 當您使用這個方法時，hello Azure 傳統入口網站可完成所有需求，您隨時可以使用方便的連結。 如果您準備好 toodeploy 您的雲端服務，您在建立時，您可以在 hello 使用**自訂建立**。

> [!NOTE]
> 如果您計劃 toopublish 雲端服務從 Visual Studio Team Services (VSTS)，使用**快速建立**，然後再設定從 VSTS 發行**快速入門**或 hello 儀表板。
> 
> 

## <a name="concepts"></a>概念
為雲端應用程式服務在 Azure 中的順序 toodeploy 中必須有三個元件：

* **服務定義**  
  hello 雲端服務定義檔 (.csdef) 定義 hello 服務模型，包括角色的 hello 數目。
* **服務組態**  
  hello 雲端服務組態檔 (.cscfg) 提供 hello 雲端服務和個別的角色，包括 hello 角色執行個體數目的組態設定。
* **服務封裝**  
  hello 服務封裝 (.cspkg) 包含 hello 應用程式程式碼和組態和 hello 服務定義檔。

您可以進一步了解這些以及 toocreate 封裝[這裡](cloud-services-model-and-package.md)。

## <a name="prepare-your-app"></a>準備您的應用程式
您可以部署雲端服務之前，您必須建立 hello 雲端服務封裝 (.cspkg)，從應用程式程式碼和雲端服務組態檔 (.cscfg)。 hello Azure SDK 提供工具來準備這些必要的部署檔案。 您可以從 hello 安裝 hello SDK [Azure 下載](https://azure.microsoft.com/downloads/)頁面上，在想 toodevelop hello 語言中應用程式程式碼。

三個雲端服務功能需要特別組態，您才能匯出服務封裝：

* 如果您想 toodeploy 雲端服務使用安全通訊端層 (SSL) 進行資料加密[設定您的應用程式](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files)ssl。
* 如果您想 tooconfigure 遠端桌面連線 toorole 執行個體，[設定 hello 角色](cloud-services-role-enable-remote-desktop.md)遠端桌面。
* 如果您想 tooconfigure 監視您的雲端服務的詳細資訊，請啟用 Azure 診斷 hello 雲端服務。 *最小監視*（監視層級 hello 預設值） 會使用從 hello 的主機作業系統的角色執行個體 （虛擬機器） 收集的效能計數器。 「 詳細資訊監視 * 會收集內部 hello 角色執行個體 tooenable 進一步分析應用程式處理期間發生的問題的效能資料為基礎的其他度量。 toofind 出 tooenable Azure 診斷，請參閱[在 Azure 中啟用診斷](cloud-services-dotnet-diagnostics.md)。

toocreate 具有 web 角色或背景工作角色部署的雲端服務，您必須[建立 hello 服務封裝](cloud-services-model-and-package.md#servicepackagecspkg)。

## <a name="before-you-begin"></a>開始之前
* 如果您尚未安裝 hello Azure SDK，請按一下**安裝 Azure SDK** tooopen hello [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後下載 hello SDK hello 慣用 toodevelop 您的程式碼的語言。 (您將有機會 toodo this 更新版本。)
* 如果任何角色執行個體需要憑證，請建立 hello 憑證。 雲端服務需要含有私密金鑰的 .pfx 檔。 您可以[上載 hello 憑證 tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)當您建立並部署 hello 雲端服務。
* 如果您計劃 toodeploy hello 雲端服務 tooan 同質群組，建立 hello 同質群組。 您可以使用同質群組 toodeploy，您的雲端服務和其他 Azure 服務 toohello 相同區域中的位置。 您可以建立 hello hello 同質群組**網路**hello Azure 傳統入口網站，在 [hello] 區域**同質群組**頁面。

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>作法：使用「快速建立」建立雲端服務
1. 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **新增**>**計算**>**雲端服務**>**快速建立**。
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. 在**URL**，輸入子網域名稱 toouse hello 公用 URL 中用來存取您在生產部署中的雲端服務。 生產部署的 hello URL 格式如下： http://*myURL*。.cloudapp.net。
3. 在**地區或同質群組**，選取 hello 地理區域或同質群組 toodeploy hello 的雲端服務。 如果您想要 toodeploy 您雲端服務 toohello 選取同質群組與區域內的其他 Azure 服務相同的位置。
4. 按一下 [建立雲端服務] 。
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    您可以監視 hello hello 訊息區域底部 hello hello 視窗中的 hello 程序的狀態。
   
    hello**雲端服務**區域隨即開啟，與 hello 顯示新雲端服務。 當 hello 狀態變更時 tooCreated 時，建立雲端服務已順利完成。
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>作法：上傳雲端服務的憑證
1. 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**憑證**。
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. 按一下 [上傳憑證] 或 [上傳]。
3. 在**檔案**，使用**瀏覽**tooselect hello 憑證 （.pfx 檔案）。
4. 在**密碼**，輸入 hello hello 憑證私密金鑰。
5. 按一下 [確定]  \(勾選記號)。
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    您可以觀賞 hello 進度 hello 上傳中 hello 訊息區域，如下所示。 Hello 上傳完成時，hello 憑證會新增 toohello 資料表。 Hello 訊息區域中，按一下 [確定] tooclose hello 訊息。
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>作法：部署雲端服務
1. 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**儀表板**。
2. 按一下 [上傳新的生產部署] 或 [上傳]。
3. 在**部署標籤**，輸入 hello 新部署，例如 MyCloudServicev4 的名稱。
4. 在**封裝**，使用**瀏覽**tooselect hello 服務封裝檔 (.cspkg) toouse。
5. 在**組態**，使用**瀏覽**tooselect hello 服務設定檔 (.cscfg) toouse。
6. 如果只有一個執行個體包含的任何角色 hello 雲端服務，選取 hello**即使一個或多個角色包含單一執行個體部署**核取方塊 tooenable hello 部署 tooproceed。
   
    如果每個角色都有至少兩個執行個體 azure 只可以在維護和服務更新期間保證 99.95%存取 toohello 雲端服務。 如有需要您可以加入其他角色執行個體上 hello**標尺**頁面之後 hello 雲端服務部署。 如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。
7. 按一下**確定**（勾選記號） toobegin hello 雲端服務部署。
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    您可以監視 hello hello 訊息區域中的 hello 部署狀態。 按一下 [確定] toohide hello 訊息。
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>確認部署是否成功完成
1. 按一下 [儀表板] 。
   
    hello 狀態應顯示 hello 服務是**執行**。
2. 在下**快速概覽**，按一下 hello 站台 URL tooopen 您網頁瀏覽器中的雲端服務。
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>後續步驟
* [雲端服務的一般設定](cloud-services-how-to-configure.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。
* [管理您的雲端服務](cloud-services-how-to-manage.md)。
* 設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。

