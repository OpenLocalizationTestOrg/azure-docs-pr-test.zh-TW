---
title: "如何建立和部署雲端服務 | Microsoft Docs"
description: "了解如何在 Azure 中使用「快速建立」方法來建立和部署雲端服務。"
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
ms.openlocfilehash: 2a2172a78bfd3ac923edbc9de366b035629dd27b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a>如何建立和部署雲端服務
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-how-to-create-deploy-portal.md)
> * [Azure 傳統入口網站](cloud-services-how-to-create-deploy.md)
> 
> 

Azure 傳統入口網站提供兩種方法讓您建立和部署雲端服務：**快速建立**和**自訂建立**。

本主題說明如何使用「快速建立」方法建立新的雲端服務，然後使用 [上傳] 來上傳雲端服務封裝並在 Azure 中加以部署。 當您使用這個方法時，Azure 傳統入口網站會在過程中提供便利的連結，讓您完成所有要求。 如果您準備在建立雲端服務時加以部署，可以同時使用 [自訂建立] 進行這兩項作業。

> [!NOTE]
> 如果您計劃從 Visual Studio Team Services (VSTS) 發佈您的雲端服務，請使用 [快速建立]，然後從 [快速啟動] 或儀表板設定 VSTS 發佈。
> 
> 

## <a name="concepts"></a>概念
需要三個元件才能部署應用程式成為 Azure 中的雲端服務：

* **服務定義**  
  雲端服務定義檔 (.csdef) 定義服務模型，包括角色數目。
* **服務組態**  
  雲端服務組態檔 (.cscfg) 提供雲端服務和個別角色的組態設定，包括角色執行個體數。
* **服務封裝**  
  服務封裝 (.cspkg) 包含應用程式程式碼和組態以及服務定義檔。

您可以在 [這裡](cloud-services-model-and-package.md)深入了解這些內容，以及如何建立封裝。

## <a name="prepare-your-app"></a>準備您的應用程式
您部署雲端服務之前，必須先從應用程式程式碼和雲端服務組態檔 (.cscfg) 建立雲端服務封裝 (.cspkg)。 Azure SDK 提供準備這些必要部署檔案的工具。 您可以從 [Azure 下載](https://azure.microsoft.com/downloads/) 頁面安裝 SDK，使用您偏好的語言開發應用程式程式碼。

三個雲端服務功能需要特別組態，您才能匯出服務封裝：

* 如果您要部署使用安全通訊端層 (SSL) 進行資料加密的雲端服務，請針對 SSL [設定應用程式](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) 。
* 如果您要設定角色執行個體的遠端桌面連線，請 [設定遠端桌面的角色](cloud-services-role-enable-remote-desktop.md) 。
* 如果您要設定雲端服務的詳細資訊監視，請啟用雲端服務的 Azure 診斷。 *最小監視* (預設監視層級) 使用從角色執行個體 (虛擬機器) 的主機作業系統收集的效能計數器。 「詳細資訊監視」會按照角色執行個體內的效能資料收集其他度量，以便進一步分析應用程式處理期間發生的問題。 若要了解如何啟用 Azure 診斷，請參閱 [啟用 Azure 診斷](cloud-services-dotnet-diagnostics.md)(英文)。

若要使用 Web 角色或背景工作角色的部署來建立雲端服務，您必須 [建立服務封裝](cloud-services-model-and-package.md#servicepackagecspkg)。

## <a name="before-you-begin"></a>開始之前
* 如果您尚未安裝 Azure SDK，請按一下 [安裝 Azure SDK] 開啟 [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後依照您偏好使用的程式碼開發語言下載 SDK。 (您稍後將有機會這麼做。)
* 如果任何角色執行個體需要憑證，請建立憑證。 雲端服務需要含有私密金鑰的 .pfx 檔。 您建立並部署雲端服務時，可以 [將憑證上傳至 Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 。
* 如果您計劃將雲端服務部署至同質群組，請建立同質群組。 您可以使用同質群組，將雲端服務和其他 Azure 服務部署到區域中的同一個位置。 在 Azure 傳統入口網站的 [網路] 區域中，您可以在 [同質群組] 頁面上建立同質群組。

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>作法：使用「快速建立」建立雲端服務
1. 在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，按一下 [新增]>[計算]>[雲端服務]>[快速建立]。
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. 在 [URL] 中，輸入要在公用 URI 中使用的子網域名稱，以存取生產部署中的雲端服務。 生產部署的 URL 格式是：http://*myURL*.cloudapp.net。
3. 在 [區域] 或 [同質群組] 中，選取要將雲端服務部署到其中的地理區域或同質群組。 如果您要將雲端服務部署到區域中其他 Azure 服務所在的同一個位置，請選取同質群組。
4. 按一下 [建立雲端服務] 。
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    您可以在視窗底端的訊息區域監視程序的狀態。
   
    [雲端服務]  區域隨即開啟，其中顯示新的雲端服務。 狀態變更為 [已建立] 時，表示雲端服務建立成功完成。
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>作法：上傳雲端服務的憑證
1. 在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，依序按一下 [雲端服務]、雲端服務的名稱及 [憑證]。
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. 按一下 [上傳憑證] 或 [上傳]。
3. 在 [檔案] 中，使用 [瀏覽] 選取憑證 (.pfx 檔)。
4. 在 [密碼] 中，輸入憑證的私密金鑰。
5. 按一下 [確定]  \(勾選記號)。
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    您可以在訊息區域查看上傳的進度，如下所示。 上傳完成時，憑證將新增至資料表中。 在訊息區域中，按一下 [確定] 關閉訊息。
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>作法：部署雲端服務
1. 在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，依序按一下 [雲端服務]、雲端服務的名稱及 [儀表板]。
2. 按一下 [上傳新的生產部署] 或 [上傳]。
3. 在 [部署標籤] 中，輸入新部署的名稱，例如，MyCloudServicev4。
4. 在 [封裝] 中，使用 [瀏覽] 選取要使用的服務封裝檔 (.cspkg)。
5. 在 [組態] 中，使用 [瀏覽] 選取要使用的服務組態檔 (.cscfg)。
6. 如果雲端服務將包含只有一個執行個體的任何角色，請選取 [Deploy even if one or more roles contain a single instance]  核取方塊，讓部署繼續進行。
   
    如果每個角色至少有兩個執行個體，Azure 只能保證在維護和服務更新期間存取雲端服務的成功率為 99.95%。 若有需要，您可以在部署雲端服務後，在 [Scale]  頁面上新增其他角色執行個體。 如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。
7. 按一下 [確定]  \(核取記號) 開始雲端服務部署。
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    您可以在訊息區域監視部署的狀態。 按一下 [確定] 以隱藏訊息。
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>確認部署是否成功完成
1. 按一下 [儀表板] 。
   
    狀態應該會顯示服務為 [正在執行] 。
2. 在 [quick glance] 下，按一下網站 URL，在網頁瀏覽器中開啟您的雲端服務。
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>後續步驟
* [雲端服務的一般設定](cloud-services-how-to-configure.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。
* [管理您的雲端服務](cloud-services-how-to-manage.md)。
* 設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。

