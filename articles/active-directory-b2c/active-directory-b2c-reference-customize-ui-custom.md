---
title: "Azure Active Directory B2C： 參考： 自訂 hello 與自訂原則的使用者之旅 UI |Microsoft 文件"
description: "Azure Active Directory B2C 自訂原則的主題"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>自訂 hello 與自訂原則的使用者之旅 UI

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> 本文是自訂 UI 的運作方式以及如何 tooenable B2C 自訂原則，使用與 hello 身分識別體驗架構的進階的描述


順暢的使用者體驗是任何「企業對客戶」解決方案的成功關鍵。 流暢的使用者體驗，是指體驗，不論是否在裝置或瀏覽器，其中無法透過我們的服務的使用者之旅辨別 hello 客戶服務，他們使用的。

## <a name="understand-hello-cors-way-for-ui-customization"></a>了解自訂 UI 的 hello CORS 方法

Azure AD B2C 可讓您 toocustomize hello 的外觀及操作的使用者經驗 (UX) 上 hello 可以潛在服務和 Azure AD B2C 顯示透過您的自訂原則的各個頁面。

基於這個目的，Azure AD B2C，請執行您的消費者瀏覽器中的程式碼，並使用 hello 現代的標準方法[跨原始資源共用 (CORS)](http://www.w3.org/TR/cors/) tooload 自訂內容與您在自訂原則中指定的特定 URLtoopoint tooyour HTML5/CSS 範本。 CORS 是像網頁 toobe 要求從起始 hello 資源 hello 網域之外的另一個定義域上的字型，可讓受限制的資源的機制。

比較 toohello 舊傳統方式，由 hello 方案，其中提供有限的文字和影像，其中配置和風格的有限的控制項提供前置 toomore 比困難 tooachieve 順暢的體驗，hello CORS 所擁有範本頁面方法支援 HTML5 和 CSS，並可讓您：

- 裝載 hello 內容和 hello 方案會將其控制項使用用戶端指令碼。
- 完整控制版面配置與風格的每個像素。

您可以適當地製作 HTML5/CSS 檔案來提供任意數量的內容頁面。

> [!NOTE]
> 基於安全性理由，JavaScript hello 使用目前被封鎖進行自訂。 需要 toounblock JavaScript 中，使用 Azure AD B2C 租用戶的自訂網域名稱。

在每個您 HTML5/CSS 的範本，您可以提供*錨點*元素，其對應所需的 toohello `<div id=”api”>` hello HTML 或 hello 內容頁面中做為以下說明的項目。 Azure AD B2C 要求所有內容頁面都必須有這個特定 div。

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Azure AD B2C 相關內容的 hello 頁面將會插入到這個 div，hello hello 頁面其餘部分時，係 toocontrol。 hello Azure AD B2C 的 JavaScript 程式碼在您的內容中提取，並將 HTML 插入至這個特定的 div 項目。 Azure AD B2C 會插入下列控制項做為適當的 hello： 帳戶選擇器控制項、 登入控制項、 多因素 （目前電話型） 控制項和屬性集合控制項。 Azure AD B2C 可確保並確認所有 hello 控制項 HTML5 相容且可存取，而且所有 hello 控制項可以完全都樣式，將無法回復控制版本。

hello 合併的內容最後會顯示為 hello 動態文件 tooyour 取用者。

hello 上述的 tooensure 如預期般運作，您必須：

- 確保內容符合 HTML5 規範且可供存取
- 確保內容伺服器已啟用 CORS。
- 透過 HTTPS 提供內容。
- 對所有連結和 CSS 內容使用絕對 URL，例如 https://yourdomain/content。

> [!TIP]
> hello 您正在裝載您的內容的站台的 tooverify 啟用 CORS，而且測試 CORS 要求時，您可以使用 hello 網站 http://test-cors.org/。 感謝您 toothis 站台，您可以直接傳送嗨 CORS 要求 tooa 遠端伺服器 (tootest 支援 CORS，則為)，或傳送嗨 CORS 要求 tooa 測試伺服器 (tooexplore CORS 的某些功能)。

> [!TIP]
> hello 網站 http://enable-cors.org/ 也構成超過 CORS 上實用的資源。

這 toothis CORS 為基礎的方法，hello 使用者後來會有應用程式和由 Azure AD B2C hello 頁面之間的一致體驗。

## <a name="create-a-storage-account"></a>建立儲存體帳戶

做為必要條件，您需要 toocreate 儲存體帳戶。 您將需要 Azure 訂用帳戶 toocreate Azure Blob 儲存體帳戶。 您可以註冊免費的試用版，在 hello [Azure 網站](https://azure.microsoft.com/en-us/pricing/free-trial/)。

1. 開啟瀏覽工作階段並瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。
2. 使用您的系統管理認證來登入。
3. 按一下 [新增] > [資料 + 儲存體] > [儲存體帳戶]。  此時會開啟 [建立儲存體帳戶] 刀鋒視窗。
4. 在**名稱**，提供 hello 儲存體帳戶名稱，例如*contoso369b2c*。 這個值會稍後稱為太*storageAccountName*。
5. 挑選 hello 適當的選擇定價層、 hello 資源群組和 hello 訂閱 hello。 請確定您擁有 hello **Pin tooStartboard**選項處於選取狀態。 按一下 [建立] 。
6. 返回 toohello 開始面板，然後按一下您剛才建立的 hello 儲存體帳戶。
7. 在 hello**服務**區段中，按一下**Blob**。 [Blob 服務] 刀鋒視窗隨即開啟。
8. 按一下 [+容器]。
9. 在**名稱**，提供 hello 容器的名稱，例如*b2c*。 這個值會是稍後參考的 tooas *containerName*。
9. 選取**Blob**為 hello**存取類型**。 按一下 [建立] 。
10. 您所建立的 hello 容器會出現在 hello 清單上 hello **Blob 服務刀鋒視窗**。
11. 關閉 hello **Blob**刀鋒視窗。
12. 在 [hello**儲存體帳戶] 刀鋒視窗**，按一下 hello**金鑰**圖示。 [存取金鑰] 刀鋒視窗隨即開啟。  
13. 請記下的 hello 值**key1**。 此值稍後會指稱為 key1。

## <a name="downloading-hello-helper-tool"></a>下載 hello helper 工具

1.  下載 hello helper 工具，從[GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip)。
2.  儲存 hello *B2C AzureBlobStorage-用戶端 master.zip*在本機電腦上的檔案。
3.  擷取的 hello B2C AzureBlobStorage-用戶端 master.zip 檔案在本機磁碟，例如在 hello hello 內容**UI 自訂套件**資料夾。 這會在其底下建立 B2C-AzureBlobStorage-Client-master 資料夾。
4.  開啟該資料夾，並以擷取 hello 封存檔 hello 內容*B2CAzureStorageClient.zip*內。

## <a name="upload-hello-ui-customization-pack-sample-files"></a>上傳 hello UI 自訂套件的範例檔案

1.  使用 Windows 檔案總管，瀏覽 toohello 資料夾*B2C AzureBlobStorage-用戶端主要*位於 hello *UI 自訂套件*hello 前一節中建立資料夾。
2.  執行 hello *B2CAzureStorageClient.exe*檔案。 這個程式只需將上傳您指定 tooyour 儲存體帳戶，並啟用 CORS 存取這些檔案的 hello 目錄中的所有 hello 檔案。
3.  請在提示出現時指定︰a.  hello 您的儲存體帳戶名稱， *storageAccountName*，例如*contoso369b2c*。
    b.  hello 主要存取金鑰，您的 azure blob 儲存體， *key1*，例如*contoso369b2c*。
    c.  hello 您的儲存體 blob 儲存體容器名稱， *containerName*，例如*b2c*。
    d.  hello hello 路徑*入門套件*例如範例檔案， *...\B2CTemplates\wingtiptoys*。

如果您遵循上述步驟 hello，hello HTML5 和 CSS 檔案的 hello *UI 自訂套件*hello 虛構公司**wingtiptoys**現在會指向 tooyour 儲存體帳戶。  您可以確認 hello 內容具有已正確地上載的 hello Azure 入口網站中開啟 hello 相關的容器刀鋒視窗。 或者，您可以確認 hello 內容具有已上傳的正確存取 hello 頁面從瀏覽器。 如需詳細資訊，請參閱[Azure Active Directory B2C： 協助程式工具使用 toodemonstrate hello 頁面使用者介面 (UI) 的自訂功能](active-directory-b2c-reference-ui-customization-helper-tool.md)。

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>請確定 hello 儲存體帳戶已啟用的 CORS

是 CORS （跨原始資源共用） 必須在您的 Azure AD B2C Premium tooload 端點上啟用您的內容。 這是因為比 hello 網域 Azure AD B2C Premium 服務 hello 頁面上，從您的內容裝載在不同的網域。

hello 存放您要裝載您的內容已啟用，CORS 的 tooverify 繼續執行步驟的 hello:

1. 開啟瀏覽工作階段並瀏覽 toohello 頁面*unified.html*使用 hello 的儲存體帳戶中，其位置的完整 URL `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`。 例如，https://contoso369b2c.blob.core.windows.net/b2c/unified.html。
2. 瀏覽 toohttp://test-cors.org。這個網站可讓您 tooverify hello 您要的使用的已啟用 CORS。  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. 在**遠端 URL**，適用於您 unified.html 內容中，輸入 hello 完整的 URL，然後按一下**傳送要求**。
4. 請確認該 hello 中的輸出 hello**結果**區段包含*XHR 狀態： 200*。 這表示 CORS 已啟用。
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
hello 儲存體帳戶現在應該會包含名為的 blob 容器*b2c*在我們的圖例中，其中包含 hello hello 中的下列 wingtiptoys 範本*入門套件*。

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

hello 下表描述 HTML5 頁面上方的 hello hello 用途。

| HTML5 範本 | 說明 |
|----------------|-------------|
| phonefactor.html | 此頁面可作為 Multi-Factor Authentication 頁面的範本。 |
| resetpassword.html | 此頁面可作為忘記密碼頁面的範本。 |
| selfasserted.html | 此頁面可作為社交帳戶註冊頁面、本機帳戶註冊頁面或本機帳戶登入頁面的範本。 |
| unified.html | 此頁面可作為統一之註冊或登入頁面的範本。 |
| updateprofile.html | 此頁面可作為設定檔更新頁面的範本。 |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>新增連結 tooyour HTML5/CSS 範本 tooyour 使用者旅程

您可以藉由直接編輯自訂原則中加入連結 tooyour HTML5/CSS 範本 tooyour 使用者之旅。

hello 自訂 HTML5/CSS 範本 toouse 使用者旅程中的有 toobe 可用於這些使用者皆的內容定義的清單中指定。 基於這個目的，選擇性 *<ContentDefinitions>*  XML 項目必須宣告在 hello  *<BuildingBlocks>* 自訂原則 XML 檔的區段。

hello 以下表格說明 hello 組 hello Azure AD B2C 識別經驗引擎和 hello 型的頁數相關 toothem 所辨識的內容定義識別碼。

| 內容定義識別碼 | 說明 |
|-----------------------|-------------|
| api.error | **錯誤頁面**。 在發生例外狀況或錯誤時，系統會顯示此頁面。 |
| api.idpselections | **識別提供者選取頁面**。 此頁面包含一份 hello 使用者的提供者在登入時，可以選擇從身分識別。 這些提供者是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶 (以電子郵件地址或使用者名稱為基礎)。 |
| api.idpselections.signup | **用於註冊的識別提供者選取**。 此頁面包含身分識別提供者，hello 使用者可以選擇在註冊期間的清單。 這些提供者是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶 (以電子郵件地址或使用者名稱為基礎)。 |
| api.localaccountpasswordreset | **忘記密碼頁面**。 此頁面包含表單 hello 使用者具有 toofill tooinitiate 重設其密碼。  |
| api.localaccountsignin | **本機帳戶登入頁面**。 此頁面包含登入表單 hello 使用者 toofill 時有本機帳戶為基礎的電子郵件地址或使用者名稱登入。 hello 表單可以包含文字輸入的方塊和密碼項目 方塊中。 |
| api.localaccountsignup | **本機帳戶註冊頁面**。 此頁面包含註冊表單 hello 使用者 toofill 中有註冊的電子郵件地址或使用者名稱為基礎的本機帳戶時。 hello 表單可以包含不同的輸入的控制項，例如文字輸入的方塊、 密碼輸入方塊、 選項按鈕、 單一選取下拉式清單方塊中和多重選取的核取方塊。 |
| api.phonefactor | **Multi-Factor Authentication 頁面**。 在此頁面上，使用者可以在註冊或登入期間驗證其電話號碼 (使用文字或語音)。 |
| api.selfasserted | **社交帳戶註冊頁面**。 此頁面包含註冊表單 hello 使用者具有 toofill 中從社交身分識別提供者，例如 Facebook 或 Google + 時使用的現有登入帳戶。 此頁面是類似 toohello 社交帳戶註冊頁面與 hello 例外狀況的 hello 密碼項目欄位上方。 |
| api.selfasserted.profileupdate | **設定檔更新頁面**。 此頁面包含表單 hello 則該使用者可以使用 tooupdate 其設定檔。 此頁面是類似 toohello 社交帳戶註冊頁面與 hello 例外狀況的 hello 密碼項目欄位上方。 |
| api.signuporsignin | **統一的註冊或登入頁面**。  此頁面可處理使用者的註冊和登入，這些使用者可使用企業識別提供者、社交識別提供者 (例如 Facebook 或 Google+) 或本機帳戶。

## <a name="next-steps"></a>後續步驟
[參考： 了解如何自訂原則以 hello 身分識別體驗架構 B2C 中工作](active-directory-b2c-reference-custom-policies-understanding-contents.md)
