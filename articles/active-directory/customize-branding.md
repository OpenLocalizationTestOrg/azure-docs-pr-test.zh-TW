---
title: "登入頁面 hello Azure Active Directory aaaCustomize |Microsoft 文件"
description: "深入了解如何 tooadd 公司品牌 toohello Azure 登入頁面"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>快速入門： 新增公司品牌 tooyour 登入頁面，在 Azure AD 中
tooavoid 混淆的可能性，許多公司都想 tooapply 一致的外觀及操作所有 hello 網站和他們管理的服務。 Azure Active Directory (Azure AD) 這項功能可讓您提供 toocustomize hello 外觀 hello 登入頁面與您的公司標誌自訂色彩配置。 hello 登入頁面為 hello 頁面，會出現在您登入 tooOffice 365 或其他 web 應用程式使用 Azure AD 作為身分識別提供者。 您互動此頁面 tooenter 您的認證。

> [!NOTE]
> * 公司商標 toohello Premium 或 Basic 版的 Azure AD 中，您升級時，才可以使用，或有 Office 365 授權。 toolearn，如果您的授權類型的支援功能檢查 hello [Azure Active Directory 定價資訊頁面](https://azure.microsoft.com/pricing/details/active-directory/)。
> 
> * Azure Active Directory Premium 和 Basic 版本可供位於中國的客戶使用 hello Azure Active Directory 的全球執行個體。 Azure Active Directory Premium 和 Basic 版是目前不支援在中國的 21Vianet 所操作的 hello Microsoft Azure 服務中。 如需詳細資訊，請連絡我們在 hello [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。

## <a name="customizing-hello-sign-in-page"></a>自訂 hello 登入頁面

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

公司商標自訂會出現在 hello Azure AD 登入頁面上，當使用者存取租用戶特定 URL 這類[ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com)。

當使用者造訪泛型的 URL，例如 www.office.com 時，hello 登入頁面將不包含公司商標自訂項目，因為 hello 系統並不知道 hello 使用者是誰。 使用者輸入其使用者識別碼或選取使用者圖格之後，就會顯示公司商標。

> [!NOTE]
> * 您的網域名稱必須為 使用出現在 hello**網域**部分 hello Azure 入口網站中您已設定的商標。 如需詳細資訊，請參閱[新增自訂網域名稱](add-custom-domain.md)。
> * 登入頁面品牌不會延續 toohello 登入頁面上的個人 Microsoft 帳戶。 如果訪客或員工使用個人 Microsoft 帳戶登入時，他們的登入頁面並不會反映您組織的品牌 hello。


### <a name="banner-logo"></a>橫幅標誌 

說明 | 條件約束 | 建議
------- | ------- | ----------
hello 橫幅標誌 顯示 hello 登入與 hello 存取面板頁面上。<br>在 hello 登入頁面上，這會顯示 hello 使用者的組織是一旦決定後，通常之後輸入 hello 使用者名稱。  | 透明 JPG 或 PNG<br>最大高度：36 像素<br>最大寬度：245 像素 | 在這裡使用您組織的標誌。<br>使用透明的映像。 請勿假設 hello 背景為白色。<br>不要在 hello 映像中新增您的標誌周圍填補，或您的標誌會尋找不當比例的小型。

### <a name="username-hint"></a>使用者名稱提示   
說明 | 條件約束 | 建議
------- | ------- | ----------
此自訂 hello 使用者名稱 欄位中的 hello 提示文字。 | 向上 too64 字元的 Unicode 文字<br>僅限純文字 | 我們建議您不要設定此如果希望外部 tooyour 應用程式在您的組織 toosign guest 使用者。
            
### <a name="sign-in-page-text"></a>登入頁面文字   
說明 | 條件約束 | 建議
------- | ------- | ----------
這會出現在 hello hello 登入表單底部，而且可以使用的 toocommunicate 的其他資訊，例如 hello 電話號碼 tooyour 服務台或法律聲明。 | 向上 too256 字元的 Unicode 文字<br>僅純文字 (沒有連結或 HTML 標記) 

### <a name="sign-in-page-image"></a>登入頁面映像  
說明 | 條件約束 | 建議
------- | ------- | ----------
這會出現在 hello hello 登入頁面背景錨定的 toohello center hello 可檢視的空間，並將調整規模並且裁剪 toofill hello 瀏覽器視窗。  <br>在手機這類螢幕狹窄的裝置上，不會顯示此映像。<br>0.55 不透明的黑色遮罩會套用此映像透過我們的程式碼載入 hello 頁面時。 | JPG 或 PNG<br>映像尺寸：1920 x 1080 像素<br>檔案大小：&gt; 300 KB | <br>使用沒有強烈主題焦點的映像。 表單登入的不透明 hello 停留 hello 中心，這個影像的周圍會出現，並可涵蓋 hello 映像，依據 hello hello 瀏覽器視窗大小的任何部分。<br>保留 hello 檔案大小越小越可能 tooensure 快速載入時間。 

### <a name="background-color"></a>背景色彩
說明 | 條件約束 | 建議
------- | ------- | ----------
此色彩會使用來取代 hello 低頻寬連線的背景影像。 |   十六進位格式的 RGB 色彩 (範例：#FFFFFF | 我們建議使用 hello 主要色彩的 hello 橫幅標誌或您組織的色彩。

### <a name="show-option-tooremain-signed-in"></a>顯示選項 tooremain 登入
說明 | 條件約束 | 建議
------- | ------- | ----------
Azure AD 登入提供 hello 使用者 hello 選項 tooremain 時關閉並重新開啟瀏覽器登入。 使用此 toohide 該選項。<br>設定這太"No"toohide 此選項，從您的使用者。 | &nbsp; | 這不會影響工作階段存留期。<br>SharePoint Online 和 Office 2010 的某些功能會相依於無法 toochoose tooremain 登入的使用者。 如果您設定此 toobe 隱藏，使用者可能會看到 toosign 中其他和非預期的提示。

> [!NOTE]
> 所有元素都是選用的。 例如，如果您不指定任何背景影像橫幅標誌，hello 登入頁面會顯示 hello 目的地站台 (例如，Office 365) 您的標誌和 hello 背景影像。

## <a name="add-company-branding-tooyour-directory"></a>新增公司品牌 tooyour 目錄

1. 登入太[hello Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。

   ![開啟使用者管理](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. 在 hello**使用者和群組**刀鋒視窗中，選取**公司商標**。
4. 在 hello**使用者和群組-公司商標**刀鋒視窗中，選取 hello**編輯**命令。

    ![編輯自訂商標](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. 修改您想 toocustomize 的 hello 項目。 所有元素都是選用的。
6. 按一下 [儲存] 。

如您所做 toohello 登入頁面品牌 tooappear，它可能佔用 tooan 小時。

## <a name="add-language-specific-company-branding-tooyour-directory"></a>將語言特定公司商標 tooyour 目錄

1. 登入 toohello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。

   ![開啟使用者管理](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. 在 hello**使用者和群組**刀鋒視窗中，選取**公司商標**。
4. 在 hello**使用者和群組-公司商標**刀鋒視窗中，選取 hello**新增語言**命令。

    ![新增語言特定商標元素](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. 修改您想 toocustomize 的 hello 項目。 所有元素都是選用的。
6. 按一下 [儲存] 。

如您所做 toohello 登入頁面品牌 tooappear，它可能佔用 tooan 小時。

## <a name="next-steps"></a>後續步驟
本快速入門中，您學到如何 tooadd 公司商標 tooyour Azure AD 目錄。 

您可以使用下列連結 tooconfigure 中公司商標 hello 從 Azure AD Azure 入口網站的 hello。

> [!div class="nextstepaction"]
> [設定公司商標](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 