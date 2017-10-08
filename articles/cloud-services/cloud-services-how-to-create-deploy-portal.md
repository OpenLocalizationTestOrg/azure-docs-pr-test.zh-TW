---
title: "aaaHow toocreate 及部署雲端服務 |Microsoft 文件"
description: "深入了解如何 toocreate 及部署雲端服務使用 hello Azure 入口網站。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>如何 toocreate 及部署雲端服務
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-how-to-create-deploy-portal.md)
> * [Azure 傳統入口網站](cloud-services-how-to-create-deploy.md)
>
>

hello Azure 入口網站提供兩種方式，讓您 toocreate 及部署雲端服務：*快速建立*和*自訂建立*。

這篇文章說明如何 toouse hello 快速建立新的雲端服務的方法 toocreate，然後使用**上傳**tooupload 和部署在 Azure 中的雲端服務封裝。 當您使用這個方法時，hello Azure 入口網站可完成所有需求，您隨時可以使用方便的連結。 如果您準備好 toodeploy 您的雲端服務，您在建立時，您可以在 hello 同時使用自訂建立。

> [!NOTE]
> 如果您計劃 toopublish 雲端服務從 Visual Studio Team Services (VSTS)，使用 快速建立，，然後設定 VSTS 發行從 hello Azure 快速入門 」 或 「 hello 儀表板。 如需詳細資訊，請參閱[所使用 Visual Studio Team Services 的持續傳遞 tooAzure][TFSTutorialForCloudService]，或 hello 的說明，請參閱**快速入門**頁面。
>
>

## <a name="concepts"></a>概念
三個元件為必要的 toodeploy 為 Azure 中雲端服務的應用程式：

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

* 如果您想 toodeploy 雲端服務使用安全通訊端層 (SSL) 進行資料加密[設定您的應用程式](cloud-services-configure-ssl-certificate-portal.md#modify)ssl。
* 如果您想 tooconfigure 遠端桌面連線 toorole 執行個體，[設定 hello 角色](cloud-services-role-enable-remote-desktop-new-portal.md)遠端桌面。
* 如果您想 tooconfigure 監視您的雲端服務的詳細資訊，請啟用 Azure 診斷 hello 雲端服務。 *最小監視*（監視層級 hello 預設值） 會使用從 hello 的主機作業系統的角色執行個體 （虛擬機器） 收集的效能計數器。 *詳細資訊監視*收集 hello 角色執行個體 tooenable 進一步分析的應用程式處理期間發生的問題中的效能資料為基礎的其他度量。 toofind 出 tooenable Azure 診斷，請參閱[在 Azure 中啟用診斷](cloud-services-dotnet-diagnostics.md)。

toocreate 具有 web 角色或背景工作角色部署的雲端服務，您必須[建立 hello 服務封裝](cloud-services-model-and-package.md#servicepackagecspkg)。

## <a name="before-you-begin"></a>開始之前
* 如果您尚未安裝 hello Azure SDK，請按一下**安裝 Azure SDK** tooopen hello [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後下載 hello SDK hello 慣用 toodevelop 您的程式碼的語言。 (您將有機會 toodo this 更新版本。)
* 如果任何角色執行個體需要憑證，請建立 hello 憑證。 雲端服務需要含有私密金鑰的 .pfx 檔。 當您建立並部署 hello 雲端服務，您可以上傳 hello 憑證 tooAzure。

## <a name="create-and-deploy"></a>建立和部署
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下**新增 > 計算**，然後向下 tooand 按一下捲動**雲端服務**。

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. 在新的 hello**雲端服務**刀鋒視窗中，輸入的值為 hello **DNS 名稱**。
4. 建立新的 [資源群組]  或選取現有的資源群組。
5. 選取 [位置] 。
6. 按一下 [封裝] 。 這會開啟 hello**將套件上傳**刀鋒視窗。 填寫 hello 必要欄位。 如果您的任一個角色包含單一執行個體，請確定核取 [即使一個或多個角色包含單一執行個體，也要部署]  。
7. 請確定已選取 [開始部署]  。
8. 按一下**確定**以關閉 hello**將套件上傳**刀鋒視窗。
9. 如果您沒有任何憑證 tooadd，按一下**建立**。

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>上傳憑證
如果您的部署套件[設定 toouse 憑證](cloud-services-configure-ssl-certificate-portal.md#modify)，您現在可以上傳 hello 憑證。

1. 選取**憑證**，在 hello**將憑證加入**刀鋒視窗中，選取 hello SSL 憑證.pfx 檔案，然後再提供 hello**密碼**hello 憑證
2. 按一下**附加憑證**，然後按一下**確定**上 hello**將憑證加入**刀鋒視窗。
3. 按一下**建立**上 hello**雲端服務**刀鋒視窗。 當 hello 部署已達到 hello**準備**狀態，您可以繼續 toohello 接下來的步驟。

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>確認部署是否成功完成
1. 按一下 hello 雲端服務執行個體。

    hello 狀態應顯示 hello 服務是**執行**。
2. 在下**Essentials**，按一下 hello**網站 URL** tooopen 您的雲端服務 web 瀏覽器中。

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>後續步驟
* [雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。
* [管理您的雲端服務](cloud-services-how-to-manage-portal.md)。
* 設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。
