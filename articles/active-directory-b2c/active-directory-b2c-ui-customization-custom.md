---
title: "使用自訂原則來自訂 UI - Azure AD B2C | Microsoft Docs"
description: "了解如何在 Azure AD B2C 中使用自訂原則時自訂使用者介面 (UI)。"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Azure Active Directory B2C︰在自訂原則中設定 UI 自訂

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

完成本文之後，您將擁有一個具備您的品牌和外觀的註冊和登入自訂原則。 使用 Azure Active Directory B2C (Azure AD B2C)，您會得到幾乎已滿控制 hello HTML 和 CSS 內容，顯示 toousers。 當您使用自訂原則時，您設定自訂 UI XML 中而不是使用 hello Azure 入口網站中的控制項。 

## <a name="prerequisites"></a>必要條件

開始之前，請完成[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。 您應該有一個使用本機帳戶來註冊和登入的有效自訂原則。

## <a name="page-ui-customization"></a>頁面 UI 自訂

使用 hello 頁面 UI 自訂功能，您可以自訂 hello 外觀及操作的任何自訂的原則。 您也可以維護應用程式與 Azure AD B2C 之間的品牌和視覺一致性。

運作方式如下：Azure AD B2C 會在客戶的瀏覽器中執行程式碼並使用稱為[跨原始資源共用 (CORS)](http://www.w3.org/TR/cors/) 的新式方法。 首先，使用自訂 HTML 內容的 hello 自訂原則中指定的 URL。 Azure AD B2C 合併以 hello HTML 內容，是從您的 URL 載入然後顯示 hello 頁面 toohello 客戶的 UI 項目。

## <a name="create-your-html5-content"></a>建立您的 HTML5 內容

建立 hello 標題中的 HTML 內容與您的產品品牌名稱。

1. 複製下列 HTML 程式碼片段的 hello。 它是語式正確空項目與 HTML5 呼叫* \<d i v id ="api 」\>\</div\> *位於 hello *\<主體\>*標記。 此元素表示 Azure AD B2C 內容所在 toobe 插入。

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >基於安全性理由，JavaScript hello 使用目前被封鎖進行自訂。

2. 在文字編輯器中，貼 hello 複製程式碼片段，然後再將 hello 檔案儲存為*自訂 ui.html*。

## <a name="create-an-azure-blob-storage-account"></a>建立 Azure Blob 儲存體帳戶

>[!NOTE]
> 在本文中，我們使用 Azure Blob 儲存體 toohost 我們的內容。 您可以選擇 toohost web 伺服器上，您的內容，但您必須[web 伺服器上啟用 CORS](https://enable-cors.org/server.html)。

toohost 此 HTML 內容，在 Blob 儲存體，請勿遵循 hello:

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 [hello**中樞**功能表上，選取**新增** > **儲存體** > **儲存體帳戶**。
3. 輸入儲存體帳戶的 [名稱]。
4. [部署模型] 可保持為 [資源管理員]。
5. 變更**帳戶種類**太**Blob 儲存體**。
6. [效能] 可保持為 [標準]。
7. [複寫] 可保持為 [RA-GRS]。
8. [存取層] 可保持為 [經常性存取]。
9. [儲存體服務加密] 可保持為 [已停用]。
10. 選取儲存體帳戶的 [訂用帳戶]。
11. 建立**資源群組**，或選取現有的資源群組。
12. 選取 hello**地理位置**儲存體帳戶。
13. 按一下**建立**toocreate hello 儲存體帳戶。  
    Hello 部署完成之後，hello**儲存體帳戶**刀鋒視窗會自動開啟。

## <a name="create-a-container"></a>建立容器

toocreate 公用容器中 Blob 儲存體，請勿 hello 遵循：

1. 按一下 hello**概觀**] 索引標籤。
2. 按一下 [容器]。
3. 在 [名稱] 中，輸入 **$root**。
4. 設定**存取類型**太**Blob**。
5. 按一下**$root** tooopen hello 新容器。
6. 按一下 [上傳] 。
7. 按一下資料夾圖示，hello 下一步太**選取檔案**。
8. 跳過**自訂 ui.html**，這您先前在 hello[自訂分頁 UI](#the-page-ui-customization-feature) > 一節。
9. 按一下 [上傳] 。
10. 選取您上傳的 hello 自訂 ui.html blob。
11. 下一步太**URL**，按一下 [**複製**。
12. 在瀏覽器中，貼上 hello 複製 URL，並移 toohello 站台。 如果無法存取 hello 站台，請確定 hello 容器存取類型會設定太**blob**。

## <a name="configure-cors"></a>設定 CORS

設定跨原始資源共用的 Blob 儲存體，藉由 hello 下列：

>[!NOTE]
>使用我們的範例 HTML 和 CSS 內容想 tootry 出 hello UI 自訂功能？ 我們已提供[簡單的協助程式工具](active-directory-b2c-reference-ui-customization-helper-tool.md)，讓您上傳我們的範例內容，並在您的 Blob 儲存體帳戶上設定。 如果您使用 hello 工具，跳過[修改註冊或登入自訂原則](#modify-your-sign-up-or-sign-in-custom-policy)。

1. 在 hello**儲存體**刀鋒視窗底下**設定**，開啟**CORS**。
2. 按一下 [新增] 。
3. 針對 [允許的來源]，輸入星號 (\*)。
4. 在 [hello**允許指令動詞**下拉式清單中，同時選取**取得**和**選項**。
5. 針對 [允許的標頭]，輸入星號 (\*)。
6. 針對 [公開的標頭]，輸入星號 (\*)。
7. 針對 [最長使用期限 (秒)]，輸入 **200**。
8. 按一下 [新增] 。

## <a name="test-cors"></a>測試 CORS

驗證，您可以藉由下列 hello:

1. 移 toohello[測試 cors.org](http://test-cors.org/)網站，然後按一下 [貼上的 hello URL 在 hello**遠端 URL**方塊。
2. 按一下 [傳送要求]。  
    如果您收到錯誤，請確定您的 [CORS 設定](#configure-cors)正確無誤。 您也可能需要 tooclear 您的瀏覽器快取，或按下 Ctrl + Shift + P 開啟 inprivate 瀏覽工作階段。

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>修改您的註冊或登入自訂原則

在最上層的 hello * \<TrustFrameworkPolicy\> *標記中，您應該會發現* \<BuildingBlocks\> *標記。 Hello 內* \<BuildingBlocks\> *標記，加入* \<ContentDefinitions\> *藉由複製下列範例中的 hello 的標記。 取代*your_storage_account* hello 的儲存體帳戶的名稱。

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>上傳更新的自訂原則

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，[切換至您的 Azure AD B2C 租用戶的 hello 內容](active-directory-b2c-navigate-to-b2c-context.md)，然後開啟 [hello **Azure AD B2C**刀鋒視窗。
2. 按一下 [所有原則]。
3. 按一下 [上傳原則]。
4. 上傳`SignUpOrSignin.xml`以 hello * \<ContentDefinitions\> *您先前加入的標記。

## <a name="test-hello-custom-policy-by-using-run-now"></a>使用測試 hello 自訂原則**立即執行**

1. 在 [hello **Azure AD B2C**刀鋒視窗中，跳過**所有原則**。
2. 選取您上傳，hello 自訂原則，然後按一下 hello**立即執行**] 按鈕。
3. 您應該能夠 toosign 向上使用電子郵件地址。

## <a name="reference"></a>參考

您可以在此找到 UI 自訂的範例範本：

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

hello sample_templates/wingtip 資料夾包含下列 HTML 檔案的 hello:

| HTML5 範本 | 說明 |
|----------------|-------------|
| phonefactor.html | 使用此檔案作為多重要素驗證頁面的範本。 |
| resetpassword.html | 使用此檔案作為忘記密碼頁面的範本。 |
| selfasserted.html | 使用此檔案作為社交帳戶註冊頁面、本機帳戶註冊頁面或本機帳戶登入頁面的範本。 |
| unified.html | 使用此檔案作為統一註冊或登入頁面的範本。 |
| updateprofile.html | 使用此檔案作為統一註冊或登入頁面的範本。 |

在 [hello[修改註冊或登入自訂原則區段](#modify-your-sign-up-or-sign-in-custom-policy)，設定 hello 內容定義`api.idpselections`。 hello 的整組內容定義辨識 hello Azure AD B2C 身分識別體驗架構以及其描述的識別碼是下表中的 hello:

| 內容定義識別碼 | 說明 | 
|-----------------------|-------------|
| api.error | **錯誤頁面**。 在發生例外狀況或錯誤時，系統會顯示此頁面。 |
| api.idpselections | **識別提供者選取頁面**。 此頁面包含一份 hello 使用者的提供者在登入時，可以選擇從身分識別。 這些選項是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶。 |
| api.idpselections.signup | **用於註冊的識別提供者選取**。 此頁面包含身分識別提供者，hello 使用者可以選擇在註冊期間的清單。 這些選項是企業識別提供者、社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶。 |
| api.localaccountpasswordreset | **忘記密碼頁面**。 此頁面包含表單 hello 使用者必須完成的 tooinitiate 密碼重設。  |
| api.localaccountsignin | **本機帳戶登入頁面**。 此頁面包含登入表單，可供使用以電子郵件地址或使用者名稱為基礎的本機帳戶進行登入。 hello 表單可以包含文字輸入的方塊和密碼項目] 方塊中。 |
| api.localaccountsignup | **本機帳戶註冊頁面**。 此頁面包含登入表單，可供註冊以電子郵件地址或使用者名稱為基礎的本機帳戶。 hello 表單可以包含各種輸入的控制項的詳細資訊，例如輸入的文字方塊、 密碼輸入方塊、 選項按鈕、 單一選取下拉式清單方塊中和多重選取的核取方塊。 |
| api.phonefactor | **Multi-Factor Authentication 頁面**。 在此頁面上，使用者可以在註冊或登入期間驗證其電話號碼 (藉由使用文字或語音)。 |
| api.selfasserted | **社交帳戶註冊頁面**。 此頁面包含使用者在使用社交識別提供者 (例如 Facebook 或 Google+) 的現有帳戶註冊時必須填妥的註冊表單。 此頁面是類似 toohello 前面社交帳戶註冊] 頁面上，除了 hello 密碼項目欄位。 |
| api.selfasserted.profileupdate | **設定檔更新頁面**。 此頁面包含表單，使用者可以使用 tooupdate 其設定檔。 此頁面是類似 toohello 社交帳戶註冊] 頁面上，除了 hello 密碼項目欄位。 |
| api.signuporsignin | **統一的註冊或登入頁面**。 此頁面會處理這兩個 hello 註冊和登入的使用者可以使用企業身分識別提供者，社交身分識別提供者，例如 Facebook 或 Google + 或本機帳戶。  |

## <a name="next-steps"></a>後續步驟

如需有關可自訂之 UI 元素的其他資訊，請參閱[內建原則 UI 自訂參考指南](active-directory-b2c-reference-ui-customization.md)。
