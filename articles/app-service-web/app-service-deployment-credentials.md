---
title: "應用程式服務的部署認證 aaaAzure |Microsoft 文件"
description: "了解如何 toouse hello Azure 應用程式服務的部署認證。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>設定 Azure App Service 的部署認證
[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 支援兩種認證類，用於[本機 Git 部署](app-service-deploy-local-git.md)和 [FTP/S 部署](app-service-deploy-ftp.md)。 這些不是 hello 與 Azure Active Directory 認證相同。

* **使用者層級認證**： 一組 hello 整個 Azure 帳戶的認證。 任何應用程式，任何訂用帳戶，hello Azure 帳戶中有權限 tooaccess，它可以是使用的 toodeploy tooApp 服務。 這些是您在設定的 hello 預設認證集**應用程式服務** > **&lt;app_name >** > **的部署認證**. 這也是 hello 預設會顯示在 hello 入口網站 GUI (例如 hello**概觀**和**屬性**應用程式[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources))。

    > [!NOTE]
    > 當您委派存取 tooAzure 資源透過角色型存取控制 (RBAC) 或共同管理員權限時，每個接收存取 tooan 應用程式的 Azure 使用者可以使用自己的個人使用者層級認證，直到已撤銷存取權。 這些部署認證不得與其他 Azure 使用者共用。
    >
    >

* **應用程式層級認證**︰一組用於單個 應用程式的認證。 它可以是使用的 toodeploy toothat 應用程式。 hello 認證的每個應用程式於應用程式建立時自動產生，而且位於 hello 應用程式發行設定檔。 您無法手動設定 hello 認證，但是您可以加以重設應用程式的任何時間。

    > [!NOTE]
    > 在訂單 toogive 有人存取 toothese 認證透過角色型存取控制 (RBAC)，您需要 toomake 它們參與者或更高版本上 hello Web 應用程式。 讀取器不允許 toopublish，，因此無法存取這些認證。
    >
    >

## <a name="userscope"></a>設定及重設使用者層級的認證

您可以在任何應用程式的[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)中，設定使用者層級認證。 無論哪個應用程式在您設定這些認證，它適用於 tooall 應用程式與 Azure 中的所有訂閱的帳戶。 

tooconfigure 使用者層級認證：

1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下 [應用程式服務] >  **&lt;any_app >** > **部署認證**。

    > [!NOTE]
    > 在 hello 入口網站中，您必須擁有至少一個應用程式，才能存取 hello 部署認證 刀鋒視窗。 不過，與 hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)，您可以設定沒有現有的應用程式的使用者層級認證。

2. 設定 hello 使用者名稱和密碼，然後再按一下**儲存**。

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

一旦您已經設定您的部署認證，您可以找到 hello *Git*部署應用程式中的使用者名稱**概觀**，

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

以及在應用程式的 [屬性] 中找到 「FTP」部署使用者名稱。

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Azure 不會顯示您的使用者層級部署密碼。 如果您忘記 hello 密碼時，您就無法再取回。 不過，您可以遵循本節中的 hello 步驟來重設您的認證。
>
>  

## <a name="appscope"></a>設定及重設應用程式層級的認證
App Service 中的每個應用程式，其應用程式層級的認證會儲存在 hello 中 XML 發行設定檔。

tooget hello 應用程式層級的認證：

1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下 [應用程式服務] >  **&lt;any_app >** > **概觀**。

2. 按一下 [...更多]  >  [取得發行設定檔]，便會開始下載 .PublishSettings 檔案。

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. 開啟 hello。PublishSettings 檔案，並尋找 hello `<publishProfile>` hello 屬性為`publishMethod="FTP"`。 然後取得其 `userName` 和 `password` 屬性。
這些是 hello 應用程式層級的認證。

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    類似 toohello 使用者層級的認證，hello FTP 部署使用者名稱的格式的 hello `<app_name>\<username>`，只是 hello Git 部署使用者名稱和`<username>`hello 前面沒有`<app_name>\`。

tooreset hello 應用程式層級的認證：

1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下 [應用程式服務] >  **&lt;any_app >** > **概觀**。

2. 按一下 [...更多]  >  [重設發行設定檔]。 按一下**是**tooconfirm hello 重設。

    hello 重設動作會使任何先前下載。PublishSettings 檔案。

## <a name="next-steps"></a>後續步驟

了解如何 toouse 這些認證 toodeploy 應用程式從[本機 Git](app-service-deploy-local-git.md)或使用[FTP/S](app-service-deploy-ftp.md)。
