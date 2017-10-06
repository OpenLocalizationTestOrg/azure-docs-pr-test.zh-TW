---
title: "Azure Active Directory B2C︰頁面 UI 自訂協助程式工具 | Microsoft Docs"
description: "協助程式工具用於 Azure Active Directory B2C toodemonstrate hello 頁 UI 自訂功能"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>Azure Active Directory B2C： 協助程式工具使用 toodemonstrate hello 頁面使用者介面 (UI) 的自訂功能
本文是附屬 toohello[主要 UI 自訂發行項](active-directory-b2c-reference-ui-customization.md)B2C Azure Active Directory (Azure AD) 中。 hello 下列步驟說明如何 tooexercise hello 使用我們提供的範例 HTML 和 CSS 內容的頁面 UI 自訂功能。

## <a name="get-an-azure-ad-b2c-tenant"></a>取得 Azure AD B2C 租用戶
您可以自訂任何項目之前，您需要太[取得 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)如果您還沒有其中一個。

## <a name="create-a-sign-up-or-sign-in-policy"></a>建立註冊或登入原則
hello 範例內容我們提供了可以在使用的 toocustomze 兩頁[註冊或登入的原則](active-directory-b2c-reference-policies.md): hello[統一的登入頁面](active-directory-b2c-reference-ui-customization.md)和 hello[自我判斷提示的屬性頁面上](active-directory-b2c-reference-ui-customization.md). [建立註冊或登入原則](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy)時，新增本機帳戶 (電子郵件地址)、Facebook、Google 和 Microsoft 做為 **身分識別提供者**。 這些是 hello 我們的範例 HTML 內容將會接受的 IDPs。  如果您想要的話，也可以新增這些 IDP 的子集。

## <a name="register-an-application"></a>註冊應用程式
您將需要[註冊應用程式](active-directory-b2c-app-registration.md)中您 B2C 租用戶，可以使用的 tooexecute 您的原則。 註冊您的應用程式之後, 您有幾個選項，您可以使用 tooactually 執行您的註冊原則：

* 建置一個快速入門應用程式列在 hello 「 開始使用 > 一節中的 hello Azure AD B2C[簽署及登入您的應用程式的取用者](active-directory-b2c-overview.md#get-started)。
* 使用預先建置的 hello [Azure AD B2C 遊樂場](https://aadb2cplayground.azurewebsites.net)應用程式。 如果您選擇 toouse hello 遊樂場，您必須使用 hello B2C 租用戶中註冊應用程式**重新導向 URI** `https://aadb2cplayground.azurewebsites.net/`。
* 使用 hello**立即執行**按鈕上您的原則中 hello [Azure 入口網站](https://portal.azure.com/)。

## <a name="customize-your-policy"></a>自訂您的原則
您需要 toofirst toocustomize hello 的外觀與您的原則，建立使用 Azure AD B2C hello 特定慣例的 HTML 和 CSS 檔案。 您接著可以上傳您靜態內容 tooa 公開可用的位置，讓 Azure AD B2C 可以存取它。 這可以是您自己專屬的 Web 伺服器、Azure Blob 儲存體、Azure 內容傳遞網路，或任何其他的靜態資源裝載提供者。 hello 唯一的需求是您的內容是透過 HTTPS 與可存取使用 CORS。 一旦您已公開您 hello 網站上的靜態內容，您可以編輯您的原則 toopoint toothis 位置及內容 tooyour 客戶，以便於出現。 hello[主要 UI 自訂發行項](active-directory-b2c-reference-ui-customization.md)詳細說明 hello Azure AD B2C 自訂功能的運作方式。

基於 hello 本教學課程中，我們已經建立一些範例內容，並裝載在 Azure Blob 儲存體上。 hello 範例內容是我們的虛構公司，「 Wingtip Toys 」 hello 佈景主題中的基本自訂。 tootry 它在您自己的原則，請遵循下列步驟：

1. 登入 tooyour 租用戶上 hello [Azure 入口網站](https://portal.azure.com/)並瀏覽 toohello B2C 功能刀鋒視窗。
2. 按一下 [註冊或登入原則]，然後按一下您的原則 (例如 "b2c\_1\_sign\_up\_sign\_in")。
3. 依序按一下 [頁面 UI 自訂] 和 [統一的註冊或登入頁面]。
4. 切換 hello**使用自訂網頁**太切換**是**。 在 [hello**自訂網頁 URI**欄位中，輸入`https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`。 按一下 [確定] 。
5. 按一下 [本機帳戶註冊頁面]。 切換 hello**使用自訂範本**太切換**是**。 在 [hello**自訂網頁 URI**欄位中，輸入`https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`。
6. 重複相同步驟 hello 的 hello**社交帳戶註冊頁面**。
   按一下**確定**兩次 tooclose hello UI 自訂的刀鋒視窗。
7. 按一下 [儲存] 。

現在可以試試您自訂的原則。 如果您想要的但您也只需按一下 hello，您可以使用您自己的應用程式或 hello Azure AD B2C 遊樂場**立即執行**hello 原則] 刀鋒視窗中命令。 在 [hello] 下拉式清單方塊選取您的應用程式，然後選擇 hello 適當重新導向 URI。 按一下 hello**立即執行**] 按鈕。 新的瀏覽器索引標籤隨即開啟，並且您可以執行透過 hello 註冊您的應用程式，以就地 hello 新內容的使用者體驗 ！

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>上傳 hello 範例內容 tooAzure Blob 儲存體
如果您想要 toouse Azure Blob 儲存體 toohost 網頁內容，您可以建立您自己的儲存體帳戶，並使用我們 B2C 協助程式工具 tooupload 檔案。

### <a name="create-a-storage-account"></a>建立儲存體帳戶
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下 [+新增]  >  [資料 + 儲存體]  >  [儲存體帳戶]。 您將需要 Azure 訂用帳戶 toocreate Azure Blob 儲存體帳戶。 您可以註冊免費的試用版，在 hello [Azure 網站](https://azure.microsoft.com/pricing/free-trial/)。
3. 提供**名稱**hello 儲存體帳戶 (例如，"contoso") 和挑選 hello 適當的選擇**定價層**，**資源群組**和**訂用帳戶**。 請確定您擁有 hello **Pin tooStartboard**選項處於選取狀態。 按一下 [建立] 。
4. 返回 toohello 開始面板，然後按一下您剛才建立的 hello 儲存體帳戶。
5. 在 [hello**摘要**區段中，按一下**容器**，然後按一下 [ **+ 加**。
6. 提供**名稱**hello 容器 (例如，"b2c 」) 並選取**Blob**為 hello**存取類型**。 按一下 [確定] 。
7. 您所建立的 hello 容器會出現在 hello 清單上 hello **Blob**刀鋒視窗。 請記下的 hello 容器; hello URL例如，它看起來應該類似太`https://contoso.blob.core.windows.net/b2c`。 關閉 hello **Blob**刀鋒視窗。
8. Hello 儲存體帳戶] 刀鋒視窗，按一下 [**金鑰**記下的 hello hello 值**儲存體帳戶名稱**和**主要存取金鑰**欄位。

> [!NOTE]
> [主要存取金鑰] 是重要的安全性認證。
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>下載 hello 協助程式工具和範例檔案
您可以下載 hello [Azure Blob 儲存體協助程式工具和範例檔案的.zip 檔](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip)複製從 GitHub 或：

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

此儲存機制包含 `sample_templates\wingtip` 目錄，其中含有範例 HTML、CSS 和影像。 這些範本 tooreference 您自己的 Azure Blob 儲存體帳戶，您將需要 tooedit hello HTML 檔案。 開啟`unified.html`和`selfasserted.html`和取代的任何執行個體`https://localhost`hello hello 前述步驟中記下您的容器 url。 您必須使用 hello 絕對路徑的 HTML 檔案，因為 hello HTML 在此情況下，會由 Azure AD，hello 網域下 hello `https://login.microsoftonline.com`。

### <a name="upload-hello-sample-files"></a>上傳檔案的 hello 範例
在 [hello 相同的儲存機制中解壓縮`B2CAzureStorageClient.zip`和執行的 hello`B2CAzureStorageClient.exe`中的檔案。 這個程式只需將上傳您指定 tooyour 儲存體帳戶，並啟用 CORS 存取這些檔案的 hello 目錄中的所有 hello 檔案。 如果您遵循上述步驟 hello，hello HTML 和 CSS 檔案將會指向 tooyour 儲存體帳戶。 請注意該 hello 儲存體帳戶名稱屬於 hello 前面`blob.core.windows.net`; 例如， `contoso`。 您可以確認 hello 內容具有已上傳正確嘗試 tooaccess`https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html`瀏覽器上。 也使用[http://test-cors.org/](http://test-cors.org/) toomake 確定 hello 內容現在是啟用 CORS。 (尋找"XHR 狀態： 200"hello 結果中。)

### <a name="customize-your-policy-again"></a>再次自訂您的原則
既然您已上傳 hello 範例內容 tooyour 自己的儲存體帳戶，您必須編輯註冊原則 tooreference 它。 重複步驟 hello hello [」 自訂原則 」](#customize-your-policy)節，這次使用您自己的儲存體帳戶 Url。 比方說，hello 位置您`unified.html`檔案將會`<url-of-your-container>/wingtip/unified.html`。

現在您可以使用 hello**立即執行**按鈕或您自己的應用程式 tooexecute 您的原則一次。 hello 應該查看幾乎完全 hello 相同-您使用 hello 相同的結果範例 HTML 和 CSS，這兩種情況。 不過，您的原則現在會參考 Azure Blob 儲存體，您的執行個體，也是可用 tooedit 和請上傳一次為您的 hello 檔案。 如需有關自訂 hello HTML 和 CSS，請參閱 toohello[主要 UI 自訂發行項](active-directory-b2c-reference-ui-customization.md)。

