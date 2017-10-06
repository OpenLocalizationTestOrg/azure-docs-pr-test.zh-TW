---
title: "aaaConfigure Azure 堆疊上的應用程式服務的部署來源 |Microsoft 文件"
description: "服務管理員該如何為 Azure Stack 上的 App Service 設定部署來源 (Git、GitHub、BitBucket、DropBox 和 OneDrive)"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 2eaf0a7f4b6e52d64a302000c1dd3c3eb5d6a6ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-sources"></a>設定部署來源

Azure Stack 上的 App Service 支援從多個原始檔控制提供者進行隨選部署。  此功能可讓應用程式開發人員 toobe 無法 toodeploy 直接從其原始檔控制儲存機制。  若要為租用戶 toobe 無法 tooconfigure App Service tooconnect tootheir 儲存機制、 系統管理員必須先設定 hello Azure 堆疊上的應用程式服務之間的整合和 hello 原始檔控制提供者。  hello 原始檔控制提供者支援，此外 toolocal Git，如下：

* GitHub
* BitBucket
* OneDrive
* DropBox

## <a name="view-deployment-sources-in-app-service-administration"></a>檢視 App Service 管理中的部署來源

1. Hello 服務系統管理員身分登入 toohello Azure 堆疊系統管理入口網站 (https://adminportal.local.azurestack.external)。
2. 瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。![App Service 資源提供者管理][1]
3. 按一下 [原始檔控制組態]。  這裡您會看到所有設定的部署來源 hello 清單。
    ![App Service 資源提供者管理原始檔控制組態][2]

## <a name="configure-github"></a>設定 GitHub

> [!NOTE]
> 需要 GitHub 帳戶 toocomplete 這項工作。  您可能希望 toouse 帳戶，您的組織，而不是個人的帳戶。

1. 登入 tooGitHub，瀏覽 toohttps://www.github.com/settings/developers 並按一下**註冊新的應用程式** ![GitHub-註冊新的應用程式][3]
2. 輸入 [應用程式名稱]，例如，Azure Stack 上的 App Service
3. 輸入 hello**首頁 URL**。  **hello 首頁 URL 必須是 hello Azure 堆疊入口網站位址**例如-https://portal.local.azurestack.external
4. 輸入 [應用程式描述]
5. 輸入 hello**授權回呼 URL**。  在預設 Azure 堆疊部署中，hello Url 是 hello 表單 https://portal.local.azurestack.external/tokenauthorize，如果您在不同的網域取代下執行網域中的為 azurestack.local ![GitHub-註冊新的應用程式以填入的值][4]
6. 按一下 [註冊應用程式]。  您現在會以頁面清單 hello**用戶端識別碼**和**用戶端密碼**hello 應用程式。
    ![GitHub - 已完成的應用程式註冊][5]
7.  在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。 
8.  瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。 
9. 按一下 [原始檔控制組態]。
10. 複製並貼上 hello**用戶端識別碼**和**用戶端密碼**hello 對應輸入方塊中的 GitHub。
11. 按一下 [儲存] 。
12. 如果您不想 tooconfigure 任何其他的部署來源，繼續太[的管理角色排程修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。


## <a name="configure-bitbucket"></a>設定 BitBucket

> [!NOTE]
> 這項工作需要 BitBucket 帳戶 toocomplete。  您可能希望 toouse 帳戶，您的組織，而不是個人的帳戶。

1. 登入 tooBitBucket 並瀏覽過**整合**您帳戶![BitBucket 儀表板-整合][7]
2. 按一下 [存取管理] 底下的 [OAuth] 與 [新增取用者] ![BitBucket 新增 OAuth 取用者][8]
3. 輸入**名稱**hello 取用者，例如 Azure 堆疊上的應用程式服務
4. 輸入**描述**hello 應用程式
5. 輸入 hello**回呼 URL**。  在預設 Azure 堆疊部署中，回呼 Url hello 處於 hello 表單 https://portal.local.azurestack.external/TokenAuthorize，如果您在不同的網域取代下執行網域中的為 azurestack.local。  hello Url 必須遵循此處所列的 BitBucket 整合 toosucceed hello 大小寫。
6. 輸入 hello **URL** -此 Url 應 hello Azure 堆疊入口網站 URL，例如 https://portal.local.azurestack.external
7. 選取 hello**權限**必要**儲存機制**:**讀取** **Webhook**:**讀取和寫入**
8. 按一下 [儲存] 。  您現在可以看到這個新的應用程式，以及 hello**金鑰**和**密碼**下**OAuth 取用者**。
    ![BitBucket 應用程式清單][9]
9.  在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。 
10.  瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。 
11. 按一下 [原始檔控制組態]。
12. 複製並貼上 hello**金鑰**到 hello**用戶端識別碼**輸入的方塊和**密碼**到 hello**用戶端密碼**是 bitbucket 適用的輸入的方塊。
13. 按一下 [儲存] 。
14. 如果您不想 tooconfigure 任何其他的部署來源，繼續太[的管理角色排程修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。

## <a name="configure-onedrive"></a>設定 OneDrive

> [!NOTE]
> 目前不支援商務用 OneDrive 帳戶。  您需要 Microsoft 帳戶連結 tooa OneDrive 帳戶 toocomplete toohave 這項工作。  您可能希望 toouse 帳戶，您的組織，而不是個人的帳戶。

1. 瀏覽 toohttps://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm 並使用您的 Microsoft 帳戶登入。
2. 按一下 [我的應用程式] 底下的 [新增應用程式]
![OneDrive 應用程式][10]
3. 輸入**名稱**hello 新應用程式註冊，請輸入**Azure 堆疊上的應用程式服務**，然後按一下**建立應用程式**
4. hello 下一個畫面會列出新的應用程式的 hello 屬性。 記錄 hello**應用程式識別碼**
![OneDrive 應用程式屬性][11]
5. 在下**應用程式密碼**按一下**產生新的密碼**和記錄 hello**產生新密碼**-這是您的應用程式密碼。
> [!NOTE]
> 記下確定 toomake hello 新密碼不是可擷取當您在此階段按一下 [確定]。
6. 在 [平台] 下，按一下 [新增平台]，然後選取 [網站]
7. 輸入 hello**重新導向 URI**。  在預設 Azure 堆疊部署中，重新導向 URI hello 處於 hello 表單 https://portal.local.azurestack.external/tokenauthorize，如果您在不同的網域取代下執行網域中的為 azurestack.local ![OneDrive 應用程式-加入 Web 平台][12]
8. 設定 hello **Microsoft Graph 權限** - **委派的權限**
    - **Files.ReadWrite.AppFolder**
    - **User.Read**  
      ![OneDrive 應用程式 - Graph 權限][13]
10. 按一下 [儲存] 。
11.  在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。 
12.  瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。 
13. 按一下 [原始檔控制組態]。
14. 複製並貼上 hello**應用程式識別碼**到 hello**用戶端識別碼**輸入的方塊和**密碼**到 hello**用戶端密碼**輸入的方塊OneDrive。
15. 按一下 [儲存] 。
16. 如果您不想 tooconfigure 任何其他的部署來源，繼續太[的管理角色排程修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。

## <a name="configure-dropbox"></a>設定 DropBox

> [!NOTE]
> 您需要 toohave DropBox 帳戶 toocomplete 這項工作。  您可能希望 toouse 帳戶，您的組織，而不是個人的帳戶。

1. 瀏覽 toohttps://www.dropbox.com/developers/apps 和使用您的 DropBox 帳戶登入
2. 按一下 **建立應用程式** 
![Dropbox 應用程式][14]
3. 選取 [DropBox API]
4. 設定 hello 存取層級太**應用程式的資料夾**
5. 輸入應用程式的**名稱**。
![Dropbox 應用程式註冊][15]
6. 按一下 [建立應用程式]。  您現在會看到與頁面列出 hello 設定 hello 應用程式包括**應用程式金鑰**和**應用程式秘鑰**。
7. 檢查 hello**應用程式資料夾名稱**設定得**Azure 堆疊上的應用程式服務**
8. 設定 hello **OAuth 2 重新導向 URI**按一下**新增**。  在預設 Azure 堆疊部署中，重新導向 URI hello 處於 hello 表單 https://portal.local.azurestack.external/tokenauthorize，如果您在不同的網域取代下執行網域中的為 azurestack.local ![Dropbox 應用程式組態][16]
9.  在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。 
10.  瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。 
11. 按一下 [原始檔控制組態]。
12. 複製並貼上 hello**應用程式金鑰**到 hello**用戶端識別碼**輸入的方塊和**應用程式秘鑰**到 hello**用戶端密碼**輸入的方塊DropBox。
13. 按一下 [儲存] 。
14. 如果您不想 tooconfigure 任何其他的部署來源，繼續太[的管理角色排程修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。

## <a name="schedule-repair-of-management-roles"></a>排程管理角色的修復
為了讓更新 hello hello 組態中的 hello 設定不同的部署來源 toobe 套用，hello 管理角色需要 toobe 修復。  此程序以確保已正確套用 hello 組態值和 hello 設定部署來源進行可用 tootenants。

1. 在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。
2. 瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。
3. 按一下 [原始檔控制組態]
4. 複製並貼上 hello**用戶端識別碼**和**用戶端密碼**hello 對應輸入方塊中的 GitHub。
5. 按一下 [儲存] 
6. 按一下 [角色]
7. 按一下 [管理伺服器]
8. 按一下 [全部修復]，然後選取 [是]。  這項作業排程的所有管理伺服器 toocomplete hello 整合修復。  hello 修復作業是 managed 的 toominimize 停機時間。
    ![App Service 資源提供者管理 - 角色 - 管理伺服器全部修復][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin.png
[2]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-source-control-configuration.png
[3]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-developer-applications.png
[4]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-populated.png
[5]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-complete.png
[6]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-roles-management-server-repair-all.png
[7]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-dashboard.png
[8]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer.png
[9]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer-complete.png
[10]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-applications.png
[11]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-registration.png
[12]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-platform.png
[13]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-graph-permissions.png
[14]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-applications.png
[15]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-registration.png
[16]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-configuration.png
