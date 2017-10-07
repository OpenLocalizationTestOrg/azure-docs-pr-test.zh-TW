---
title: "aaaAdd 公司品牌 tooyour 登入和存取面板頁面"
description: "了解如何 tooadd 公司品牌 toohello Azure 登入頁面和 hello 存取面板頁面"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>新增公司品牌 tooyour 登入和存取面板頁面
tooavoid 混淆的可能性，許多公司都想 tooapply 一致的外觀及操作所有 hello 網站和他們管理的服務。 Azure Active Directory 可讓您遵循網頁與您的公司標誌自訂色彩配置的 hello toocustomize hello 外觀提供這項功能：

* **登入頁面**-這是出現在您登入 tooOffice 365 hello 頁面或其他 web 應用程式使用 Azure AD 作為身分識別提供者。 您與此頁面互動主領域探索或 tooenter 期間您的認證。 hello 主領域探索可讓 hello 系統 tooredirect 同盟使用者 tootheir 內部部署 STS （例如 AD FS)。
* **存取面板頁面**-hello 存取面板是網頁型入口網站，可讓您 tooview 及啟動 hello 雲端型應用程式您 Azure AD 管理員已授與您存取權。 tooaccess hello 存取面板中，使用下列 URL 的 hello: [https://myapps.microsoft.com](https://myapps.microsoft.com)。

本主題說明如何自訂登入頁面 hello 和 hello 存取面板頁面。

> [!NOTE]
> * 公司商標是只適用於您已升級 toohello Premium 或 Azure Active Directory Basic 版或 Office 365 使用者的功能。 如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。
> * Azure Active Directory Premium 和 Basic 版本可供位於中國的客戶使用 hello Azure Active Directory 的全球執行個體。 Azure Active Directory Premium 和 Basic 版是目前不支援在中國的 21Vianet 所操作的 hello Microsoft Azure 服務中。 如需詳細資訊，請連絡我們在 hello [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。
>
>

## <a name="customizing-hello-sign-in-page"></a>自訂 hello 登入頁面
一般而言，如果您需要瀏覽器為基礎的存取 tooyour 雲端應用程式和貴組織訂閱的服務，您可以使用 hello 登入頁面。

如果您已套用變更 tooyour 登入頁面上，就可以在 hello 變更 tooappear tooan 小時。

只有當您使用租用戶特定 URL (例如 https://outlook.com/**contoso**.com 或 https://mail.**contoso**.com) 來造訪服務時，才會顯示加上商標的登入頁面。

當您造訪具有非租用戶特定 URL (例如 https://mail.office365.com) 的服務，就會看到未加上商標的登入頁面。 在此情況下，只要您一輸入使用者識別碼或是選取使用者磚，就會顯示您的商標。

> [!NOTE]
> * 您的網域名稱必須為 使用出現在 hello **Active Directory** > **目錄** > **網域**區段 hello Azure 傳統入口網站在您已設定的商標。
> * 登入頁面品牌不會延續 toohello 消費者登入的 Microsoft 的頁面。 如果您使用個人 Microsoft 帳戶登入，您可能會看到加上品牌的 Azure AD 所呈現的使用者磚清單，但您組織的品牌 hello 不會套用 toohello Microsoft 帳戶登入頁面。
>
>

如果您的公司品牌、 色彩和其他可自訂的元素，此頁面上，您會想 tooshow，請參閱下列映像 toounderstand hello hello 兩種體驗差異 hello。

下列螢幕擷取畫面顯示和 hello Office 365 登入頁面在桌面的電腦上的範例 hello**之前**自訂：

![自訂前的 Office 365 登入頁面][1]

下列螢幕擷取畫面顯示和 hello Office 365 登入頁面在桌面的電腦上的範例 hello**之後**自訂：

![自訂後的 Office 365 登入頁面][2]

hello 下列螢幕擷取畫面顯示的範例登入頁面 hello Office 365 行動裝置上**之前**自訂：

![自訂前的 Office 365 登入頁面][3]

hello 下列螢幕擷取畫面顯示的範例登入頁面 hello Office 365 行動裝置上**之後**自訂：

![自訂後的 Office 365 登入頁面][4]

當您調整瀏覽器視窗時，hello 大型圖例，hello 像之前，顯示一個通常會裁剪 tooaccommodate 不同的螢幕外觀比例。 這一點，您應該嘗試 tookeep hello 主要視覺元素 hello 圖中的，使其永遠顯示 hello 左上角 （右上由右至左語言）。 這是很重要，因為 hello 右下角出現朝上 / 左邊 hello 或從向 hello 上層 hello 底部調整大小通常就會發生。

hello 下圖顯示剩餘的調整大小的 toohello hello 瀏覽器時，如何裁剪 hello 圖：

![][6]

以下是如何出現之後 hello 瀏覽器會調整大小接近 hello 上方：

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>可以自訂 hello 頁面上的哪些元素？
您可以自訂下列項目 hello 登入頁面上的 hello:

![][5]

| 頁面元素 | 在 [hello] 頁面上的位置 |
|:--- | --- |
| 橫幅標誌 |顯示 hello 的右上方 hello 頁面。 取代 hello 標誌 hello 目的地站台 （例如登入 toodisplays。 Office 365 或 Azure)。 |
| 大型圖例/背景色彩 |顯示 hello hello 頁面左邊。 會取代您要登入 toodisplays hello 映像 hello 目的地網站。 取代 hello 大型圖例在低頻寬連線或窄的畫面上，可能會顯示 hello 背景色彩。 |
| 讓我保持登入 |顯示在 hello 密碼文字方塊下方。 |
| 登入頁面文字 |當您需要 tooconvey 很有幫助的資訊，再使用登入工作或學校帳戶時，上述 hello 頁尾。 例如，您可能想 tooinclude hello 電話號碼 tooyour 服務台或法律聲明。 |

> [!NOTE]
> 所有元素都是選用的。 比方說，如果您指定橫幅標誌 但沒有大型圖例，hello 登入頁面會顯示您的標誌和 hello 圖例中 hello 目的地站台 （也就是 hello Office 365 加州高速公路影像）。
>
>

在您登入頁面上，hello**讓我保持登**核取方塊可讓使用者 tooremain 時關閉並重新開啟瀏覽器登入。 它不會影響工作階段存留期。 您可以隱藏 hello hello Azure Active Directory 登入頁面上的核取方塊。

Hello 核取方塊會顯示是否取決 hello 設定**隱藏 KMSI**。

![][9]

toohide hello 核取方塊，設定此設定太**隱藏**。

> [!NOTE]
> SharePoint Online 和 Office 2010 的某些功能而定的使用者可以 toocheck 此方塊。 如果您設定此設定 toohidden，您的使用者可能會看到 toosign 中其他和非預期的提示。
>
>

您也可以將此頁面上的所有元素都翻成當地使用語。 設定一組「預設」自訂元素之後，就可以設定不同地區設定的其他版本。 您也可以混合使用並符合各種元素。 例如，您可以：

* 建立適用於所有文化的「預設」大型圖例，然後建立英文和法文的特定版本。 當您設定您的瀏覽器 tooone 的這兩種語言時，會出現 hello 特定映像，而 hello 預設圖例出現的所有其他語言。
* 為您的組織設定不同的標誌 (例如日文或希伯來文版本)。

## <a name="access-panel-page-customization"></a>存取面板頁面自訂
hello 存取面板 頁面是您已授與的快速存取 toohello 雲端應用程式存取 tooby 您的系統管理員基本上入口網站頁面。 在此頁面上，您的應用程式會顯示為可點選的應用程式圖格。

下列螢幕擷取畫面的 hello 自訂後，顯示存取面板頁面的範例。

![][8]

## <a name="configure-your-directory-with-company-branding"></a>使用公司商標來設定目錄
您可以在 hello Azure 傳統入口網站中設定一個預設集的每個目錄的自訂項目。 已儲存 hello 預設值之後，系統管理員可以新增每個項目，針對不同語言的當地語系化的版本 / 地區設定。 所有可自訂元素都是選用的。

例如，如果您設定預設 橫幅標誌，但沒有大型圖例，hello 登入頁面會顯示您的標誌 hello 右上角。 不過，系統會顯示 hello hello 站台的預設圖例。

假設有下列組態的 hello:

* 預設的橫幅標誌和英文登入頁面文字
* 語言特定的德文登入頁面文字

如果您的語言喜好設定為德文，您會取得 hello 預設橫幅標誌 但 hello 德文的文字。

雖然技術上來說，您可以設定一組不同的 Azure AD 支援每種語言，我們建議您保留 hello 多變化低、 維護和效能考量。

> [!IMPORTANT]
> Yammer 並不會顯示 hello 使用者登入之後，Azure AD 品牌登入頁面之前的 hello。 hello 使用者會看到第一次，hello 泛用 Office 365 登入頁面和 hello 然後品牌頁面之後。   
 
 
**tooadd 公司商標 tooyour 目錄中，執行下列步驟的 hello:**

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)想 toocustomize hello 目錄的系統管理員身分。
2. 選取您想要 toocustomize hello 目錄。
3. 在 hello hello 上方的工具列中按一下**設定**。
4. 按一下 [自訂商標] 。
5. 修改您想 toocustomize 的 hello 項目。 所有欄位都是選用的。
6. 按一下 [儲存] 。

它最多可能需要新的變更 tooan 小時您製作 toohello 登入頁面，商標 tooappear。

**tooadd 特定語言的公司品牌，執行下列步驟的 hello:**

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)想 toocustomize hello 目錄的系統管理員身分。
2. 選取您想要 toocustomize hello 目錄。
fs3。 在 hello hello 上方的工具列中按一下**設定**。
4. 按一下 [自訂商標] 。
5. 按一下 [新增特定語言的商標] 。
6. 選取您想 toocustomize hello 標誌，然後再按一下 hello 語言**下一步**。
7. 編輯您要為其 tooconfigure 特定語言覆寫只 hello 元素。 所有欄位都是選用的。 如果欄位保留空白，然後 hello 自訂的預設值改為顯示 （或 hello Microsoft 預設值，如果未設定自訂的預設值）。
8. 按一下 [儲存] 。

**tooremove 公司品牌從您的目錄中，執行下列步驟的 hello:**

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)想 toocustomize hello 目錄的系統管理員身分。
2. 選取您想要 toocustomize hello 目錄。
3. 在 hello hello 上方的工具列中按一下**設定**。
4. 按一下 [自訂商標] 。
5. 在 hello 自訂品牌 頁面上，選取 **編輯現有品牌設定**並前往 toohello 下一個頁面。
6. 根據哪一個項目要 tooremove，執行下列一或多個 hello 下列：

    a. 在 [橫幅標誌] 之下，選取 [移除上傳的標誌]。

    b.這是另一個 C# 主控台應用程式。 在 [圖格標誌] 之下，選取 [移除上傳的標誌]。

    c. 移除所有的文字方塊中的 hello 文字。

    d. 按 [下一步] 。

    e. 移除所有的文字方塊中的 hello 文字。
7. 按一下**儲存**tooremove hello 項目。
8. 如果有必要，請按一下**自訂品牌**再次並移除所有特定語言品牌需要 toobe 重複這些步驟。
    當您按一下 已移除所有的品牌設定**自訂品牌**並查看 hello**自訂預設品牌**表單沒有現有的設定。

## <a name="testing-and-examples"></a>測試和範例
建議您先使用測試租用戶進行試驗，再於生產環境中進行變更。

**tooverify 是否您的品牌已套用：**

1. 開啟 InPrivate 或 Incognito 瀏覽器工作階段。
2. 請瀏覽 https://outlook.com/contoso.com，以您自訂的 hello 網域取代 contoso.com。

這也適用於類似 contoso.onmicrosoft.com 的網域。

toohelp 建立有效的自訂集，我們已自訂下列兩個虛構登入頁面的 hello:

* [http://aka.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://aka.ms/aaddemo002](http://aka.ms/aaddemo002)

tootest hello 語言專屬的設定，您會需要 toomodify hello 預設語言喜好設定設定您的自訂您的 web 瀏覽器 tooa 語言。 在 Internet Explorer 中，您會設定這在 hello**網際網路選項**功能表。

## <a name="customizable-elements"></a>可自訂元素
Azure AD 中的部分可自訂元素有多個使用案例。 您可以設定目錄每一次公司標誌，並且適用於兩者，hello 登入和存取面板 頁面。 有些可自訂的元素是特定唯一 toohello 登入頁面。 hello 下表提供詳細資料 hello 可自訂的不同元素。

| 名稱 | 說明 | 條件約束 | 建議 |
| --- | --- | --- | --- |
| 橫幅標誌 |hello 橫幅標誌會顯示 hello 登入頁面和 hello 存取面板上。 |<p>JPG 或 PNG</p><p>60x280 像素</p><p>10 KB</p> |<p>使用您組織的完整標誌 (包含形符和商標)</p><p>將它保留在 30 像素高 tooavoid 引入行動裝置上的捲軸</p><p>保持低於 4 KB</p><p>使用透明 PNG （不要認為該 hello 登入頁面一律擁有白色背景）</p> |
| 磚標誌 |（目前未用於 hello 登入頁面）在未來的 hello，此文字可能會使用的 tooreplace hello 泛用 「 公司或學校帳戶 」 形符 hello 體驗的不同位置中。 |<p>JPG 或 PNG</p><p>120x120 像素</p><p>10 KB</p> |<p>使其保持簡單 （沒有小型文字），因為此映像可能會調整大小的 too50% |
| </p> | | | |
| 登入頁面使用者名稱標籤 |（目前未用於 hello 登入頁面）在未來的 hello，此文字可能會使用的 tooreplace hello hello 體驗的不同位置中的泛用 「 公司或學校帳戶 」 字串。 您可以將它設定 toosomething，例如"Contoso account"或"Contoso id。 」 |<p>向上 too50 字元的 Unicode 文字</p><p>僅純文字 (沒有連結或 HTML 標記)</p> |<p>保持簡短和簡單</p><p>詢問使用者如何它們通常是指 toohello 工作或學校帳戶您提供的。</p> |
| 登入頁面文字 |此 「 重複使用 」 文字 hello 登入頁面表單下方會出現，並使用的 toocommunicate 其他指示，或可在 tooget 說明及支援。 |<p>向上 too256 字元的 Unicode 文字</p><p>僅純文字 (沒有連結或 HTML 標記)</p> |保持低於 250 個字元 (約 3 行文字) |
| 登入頁面圖例 |hello 圖是顯示在 hello 登入頁面 toohello hello 登入頁面表單左邊的大型映像。 |<p>JPG 或 PNG</p><p>1420x1200</p><p>500 KB</p> |<p>1420x1200 像素</p><p>重要事項：保持越小越好，最好低於 200 KB。 Hello 映像不快取時，如果此影像太大，會影響 hello 效能的 hello 登入頁面</p><p>這是通常裁剪影像，tooaccommodate 不同外觀比例。 Hello 主要視覺元素保持 hello 左上角 （右上方對 RTL 語言），因為從 hello 右下角，hello 瀏覽器視窗縮小至 hello 上 / 左邊，調整大小時發生。</p> |
| 登入頁面背景色彩 |在 hello 區域 toohello hello 登入頁面表單左邊用於 hello 登入頁面背景色彩。 |必須是十六進位格式的 RGB 色彩 (範例: #FFFFFF) |<p>hello 背景色彩可能會顯示以 hello 取代在低頻寬連接上的大型圖例</p><p>我們建議挑選橫幅標誌 hello hello 主要色彩</p> |

## <a name="next-steps"></a>後續步驟
* [開始使用 Azure Active Directory Premium](active-directory-get-started-premium.md)
* [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
