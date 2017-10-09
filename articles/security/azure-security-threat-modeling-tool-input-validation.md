---
title: "驗證-Microsoft 威脅模型化工具-Azure aaaInput |Microsoft 文件"
description: "hello 威脅模型化工具中公開的威脅防護功能"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>安全性架構︰輸入驗證 | 風險降低 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **Web 應用程式** | <ul><li>[停用所有使用未受信任樣式表之轉換的 XSLT 指令碼](#disable-xslt)</li><li>[確定可能包含使用者可控制內容的每個頁面都選擇不要自動探查 MIME](#out-sniffing)</li><li>[強化或停用 XML 實體解析](#xml-resolution)</li><li>[利用 http.sys 的應用程式會執行 URL 標準化驗證](#app-verification)</li><li>[確定在接受使用者的檔案時已備妥適當的控制](#controls-users)</li><li>[確定 Web 應用程式有使用 type-safe 參數來存取資料](#typesafe)</li><li>[使用個別的模型繫結類別，或繫結的篩選器清單 tooprevent MVC 大量指派弱點](#binding-mvc)</li><li>[編碼不受信任的 web 輸出先前 toorendering](#rendering)</li><li>[對所有字串類型的模型屬性執行輸入驗證和篩選](#typemodel)</li><li>[應該對接受所有字元的表單欄位 (例如 RTF 編輯器) 套用清理](#richtext)</li><li>[未指派並沒有內建的編碼方式的 DOM 項目 toosinks](#inbuilt-encode)</li><li>[驗證所有重新導向 hello 應用程式中的都已關閉或安全地完成](#redirect-safe)</li><li>[對控制器方法所接受的所有字串類型參數實作輸入驗證](#string-method)</li><li>[設定處理 tooprevent DoS 到期 toobad 規則運算式的規則運算式的上限逾時](#dos-expression)</li><li>[避免在 Razor 檢視中使用 Html.Raw](#html-razor)</li></ul> | 
| **資料庫** | <ul><li>[請勿在預存程序中使用動態查詢](#stored-proc)</li></ul> |
| **Web API** | <ul><li>[確定 Web API 方法已完成模型驗證](#validation-api)</li><li>[對 Web API 方法所接受的所有字串類型參數實作輸入驗證](#string-api)</li><li>[確定 Web API 有使用 type-safe 參數來存取資料](#typesafe-api)</li></ul> | 
| **Azure Document DB** | <ul><li>[針對 DocumentDB 使用參數化 SQL 查詢](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[透過結構描述繫結驗證 WCF 輸入](#schema-binding)</li><li>[透過參數偵測器驗證 WCF 輸入](#parameters)</li></ul> |

## <a id="disable-xslt"></a>停用所有使用未受信任樣式表之轉換的 XSLT 指令碼

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [XSLT 安全性](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx)、[XsltSettings.EnableScript 屬性](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **步驟** | XSLT 支援指令碼內使用 hello 的樣式表`<msxml:script>`項目。 這可讓自訂函式 toobe 用於 XSLT 轉換。 hello hello hello 轉換的程序的內容下執行 hello 指令碼。 受信任的環境 tooprevent 執行不受信任的程式碼中，必須停用 XSLT 指令碼。 *如果使用.NET:*預設停用 XSLT 指令碼; 不過，您必須確認，它尚未明確啟用透過 hello`XsltSettings.EnableScript`屬性。|

### <a name="example"></a>範例 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>範例
如果您將使用 MSXML 6.0，XSLT 指令碼預設會停用;不過，您必須確定，它尚未明確啟用透過 AllowXsltScript hello XML DOM 物件屬性。 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>範例
如果您使用 MSXML 5 或較低版本，預設會啟用 XSLT 指令碼，因此您必須明確地加以停用。 設定 hello XML DOM 物件屬性 AllowXsltScript toofalse。 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>確定可能包含使用者可控制內容的每個頁面都選擇不要自動探查 MIME

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [IE8 安全性單元五 - 完善的保護](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)  |
| **步驟** | <p>針對可包含使用者可控制內容的每個頁面上，您必須使用 hello HTTP 標頭`X-Content-Type-Options:nosniff`。 toocomply 此項需求，您可以任一組 hello 必要的標頭可能包含可控制使用者的內容，那些頁面的頁面，或您可以將它設定全域 hello 應用程式中的所有頁面。</p><p>每一種會從 web 伺服器傳送的檔案都具有相關聯[MIME 類型](http://en.wikipedia.org/wiki/Mime_type)(也稱為*內容類型*)，以描述 hello 性質 hello 內容 （也就是影像、 文字、 應用程式等）</p><p>hello X 內容-類型選項標頭是可讓開發人員的 HTTP 標頭，其內容不應為 MIME 探查 toospecify。 此標頭是設計的 toomitigate MIME 探查攻擊。 Internet Explorer 8 (IE8) 已新增對此標頭的支援</p><p>只有 Internet Explorer 8 (IE8) 的使用者能夠受益於 X-Content-Type-Options。 舊版 Internet Explorer 不目前尊重 hello X 內容-類型選項標頭</p><p>Internet Explorer 8 （和更新版本） 是 hello 只有主要瀏覽器 tooimplement MIME 探查退出功能。 這項建議是否以及何時其他主要瀏覽器 (Safari、 Firefox Chrome) 實作類似的功能，將會更新的 tooinclude 語法這些瀏覽器</p>|

### <a name="example"></a>範例
tooenable hello 必要的標頭全域的 hello 應用程式中的所有頁面，您可以執行 hello 下列其中一種： 

* 新增 hello web.config 檔案中的 hello 標頭，如果 hello 應用程式裝載在由網際網路資訊服務 (IIS) 7 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* 加入透過 hello hello 標頭全域應用程式\_BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* 實作自訂 HTTP 模組 

``` 
public class XContentTypeOptionsModule : IHttpModule 
  {
    #region IHttpModule Members 
    public void Dispose() 
    { 

    } 
    public void Init(HttpApplication context)
    { 
      context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders); 
    } 
    #endregion 
    void context_PreSendRequestHeaders(object sender, EventArgs e) 
      { 
        HttpApplication application = sender as HttpApplication; 
        if (application == null) 
          return; 
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* 您可以將它加入 tooindividual 回應啟用 hello 必要的標頭標記僅適用於特定頁面： 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>強化或停用 XML 實體解析

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [XML 實體擴充](http://capec.mitre.org/data/definitions/197.html)、[XML 阻斷服務攻擊與防禦](http://msdn.microsoft.com/magazine/ee335713.aspx)、[MSXML 安全性概觀](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx)、[保護 MSXML 程式碼的最佳作法](http://msdn.microsoft.com/library/ms759188(VS.85).aspx)、[NSXMLParserDelegate 通訊協定參考](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html)、[解析外部參考](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **步驟**| <p>雖然它尚未廣泛使用，但沒有允許 hello XML 剖析器 tooexpand 巨集實體與 hello 文件本身內或從外部來源所定義值的 XML 功能。 例如，hello 文件可能會定義實體"companyname"hello 值 「 Microsoft 」，以便每次 hello 文字"&companyname;"會出現在 hello 文件，它會自動取代 Microsoft 的 hello 文字。 或者，hello 文件可能會定義實體所參考的外部 web 服務 toofetch hello 目前值的 Microsoft 存貨的 「 MSFTStock"。</p><p>然後隨時"&MSFTStock;"會出現在 hello 文件，它會自動取代 hello 目前股票價格。 不過，這項功能可能會濫用 toocreate 拒絕服務 (DoS) 的情況。 攻擊者可以巢狀多個實體 toocreate 指數擴充 XML 定取用 hello 系統上所有可用的記憶體。 </p><p>或者，他可以建立資料流處理後的外部參考無限量的資料，或只是停止回應的 hello 執行緒。 如此一來，所有的小組必須內部及/或外部 XML 實體解析如果完全停用其應用程式不會使用它，或以手動方式限制 hello 記憶體數量以及 hello 應用程式可以使用的實體解析，如果此功能的時間絕對必要。 如果應用程式不需要解析實體，則請停用。 </p>|

### <a name="example"></a>範例
針對.NET Framework 程式碼，您可以使用下列方法的 hello:

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
請注意該 hello 預設值是`ProhibitDtd`中`XmlReaderSettings`為 true，但在`XmlTextReader`為 false。 如果您使用 XmlReaderSettings，您不需要 tooset ProhibitDtd tootrue 明確，但建議為了安全起見，您執行。 也請注意 hello XmlDocument 類別可讓實體解析，根據預設值。 

### <a name="example"></a>範例
XmlDocuments，使用 hello 的 toodisable 實體解析`XmlDocument.Load(XmlReader)`hello 的多載載入方法和設定 hello 適當屬性中的 hello XmlReader 引數 toodisable 解析 hello 下列程式碼所示： 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>範例
如果您的應用程式可能不是停用實體解析，設定 hello XmlReaderSettings.MaxCharactersFromEntities 屬性 tooa 合理的值，根據 tooyour 應用程式的需求。 這會限制 hello 潛在的指數擴充 DoS 攻擊的影響。 下列程式碼的 hello 提供這個方法的範例： 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>範例
如果您需要 tooresolve 內嵌實體，但不是需要 tooresolve 外部實體，設定 hello XmlReaderSettings.XmlResolver 屬性 toonull。 例如： 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
請注意，在 MSXML6，ProhibitDTD 設定 tootrue （停用 DTD 處理） 預設值。 針對 Apple OSX/iOS 程式碼，您可以使用的 XML 剖析器有兩個︰NSXMLParser 和 libXML2。 

## <a id="app-verification"></a>利用 http.sys 的應用程式會執行 URL 標準化驗證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>任何使用 http.sys 的應用程式皆應遵循下列指導方針︰</p><ul><li>限制 hello URL 長度 toono 16,384 以上字元 （ASCII 或 Unicode）。 這是 hello 絕對最大 URL 長度 hello 預設網際網路資訊服務 (IIS) 6 設定為基礎。 網站長度應盡可能不超過此上限</li><li>這些會利用 hello 標準化規則中的 hello.NET FX 作為 hello 標準.NET Framework 檔案 I/O 類別 （例如 FileStream)</li><li>明確建置已知檔案名稱的允許清單</li><li>明確拒絕不會提供 UrlScan 拒絕的已知檔案類型︰exe、bat、cmd、com、htw、ida、idq、htr、idc、shtm[l]、stm、printer、ini、pol、dat 檔案</li><li>攔截 hello 下列例外狀況：<ul><li>System.ArgumentException (針對裝置名稱)</li><li>System.NotSupportedException (針對資料串流)</li><li>System.IO.FileNotFoundException (針對無效的逸出檔名)</li><li>System.IO.DirectoryNotFoundException (針對無效的逸出目錄)</li></ul></li><li>*不這麼做*tooWin32 檔案 I/O Api 呼叫。 無效的 URL 依正常程序會傳回 400 錯誤 toohello 使用者，並記錄 hello 真的錯誤。</li></ul>|

## <a id="controls-users"></a>確定在接受使用者的檔案時已備妥適當的控制

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [不受限制的檔案上傳](https://www.owasp.org/index.php/Unrestricted_File_Upload)、[檔案簽章資料表](http://www.garykessler.net/library/file_sigs.html) |
| **步驟** | <p>上傳的檔案代表極大的風險 tooapplications。</p><p>許多攻擊 hello 第一個步驟是的 tooget 某些程式碼 toohello 系統 toobe 遭受攻擊。 然後 hello 攻擊只需要的 toofind 方式 tooget hello 程式碼執行。 使用檔案上傳有助於 hello 攻擊者達成 hello 第一個步驟。 不受限制的檔案上傳 hello 結果可能會不同，包括完整的系統接管，多載的檔案系統或資料庫中，轉送攻擊 tooback 後端系統，以及簡單的損毀。</p><p>它相依於哪些 hello 應用程式不與 hello 上傳檔案，特別是儲存在何處。 伺服器端缺少驗證上傳檔案的動作。 請針對檔案上傳功能實作下列安全性控制︰</p><ul><li>副檔名檢查 (只應接受一組有效的允許檔案類型)</li><li>檔案大小上限</li><li>您必須上傳的 toowebroot;hello 位置應該在非系統磁碟機上的目錄</li><li>命名慣例應該遵守，使得 hello 上傳的檔案名稱有一些隨機性，因此為 tooprevent 檔案會覆寫</li><li>應該寫入 toohello 磁碟之前的防毒掃描檔案</li><li>確認驗證 hello 檔案名稱和任何中繼資料 （例如檔案路徑），惡意的字元</li><li>應該檢查檔案格式的簽章，tooprevent masqueraded 的檔案上傳的使用者 （例如，藉由變更副檔名 tootxt 上載的 exe 檔案）</li></ul>| 

### <a name="example"></a>範例
Hello 關於檔案格式的簽章驗證的最後一個點，請參閱下方的 toohello 類別，如需詳細資訊： 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>確定 Web 應用程式有使用 type-safe 參數來存取資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>如果您使用 hello 參數集合，SQL 會視為 hello 輸入是做為常值，而不是可執行程式碼。 hello 參數集合可以是輸入資料上的使用的 tooenforce 類型和長度條件約束。 Hello 範圍以外的值會觸發例外狀況。 如果不使用類型安全的 SQL 參數，攻擊者可能會內嵌在 hello 進行篩選輸入可以 tooexecute 資料隱碼攻擊。</p><p>當建構 SQL 查詢中發生的未篩選的輸入的 tooavoid 可能 SQL 資料隱碼攻擊時，請使用類型安全的參數。 type-safe 參數可與預存程序和動態 SQL 陳述式搭配使用。 參數都會視做為常值 hello 資料庫，而不是可執行程式碼。 參數的類型和長度也會受到檢查。</p>|

### <a name="example"></a>範例 
hello 下列程式碼顯示如何 toouse 型別以 hello SqlParameterCollection 安全參數呼叫預存程序時。 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
在上述程式碼範例的 hello，hello 輸入的值不能超過 11 個字元。 如果 hello 資料不符合 toohello 型別或 hello 參數所定義的長度，hello SqlParameter 類別擲回例外狀況。 

## <a id="binding-mvc"></a>使用個別的模型繫結類別，或繫結的篩選器清單 tooprevent MVC 大量指派弱點

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | [中繼資料屬性](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute)，[公用金鑰安全性的弱點可能會和緩和措施](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation)，[完整指南 tooMass ASP.NET MVC 中的指派](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx)， [EF 使用 MVC 使用者入門](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **步驟** | <ul><li>**我應該在何時尋找 over-posting 弱點？-** over-posting 弱點可能發生在您從使用者輸入繫結模型類別的任何位置。 MVC 等架構可在自訂 .NET 類別中代表使用者資料，包括純舊 CLR 物件 (POCO)。 MVC 會自動填入這些 hello 要求資料的模型類別提供方便的表示法，來處理使用者輸入。 這些類別包括不應該由 hello 使用者設定的屬性，hello 應用程式可以很容易遭受 tooover 張貼攻擊，允許使用者控制的 hello 應用程式不會預期的資料。 MVC 模型繫結，例如資料庫存取技術，例如像 Entity Framework 的物件/relational mapper 通常也支援使用 POCO 物件 toorepresent 資料庫資料。 這些資料模型類別提供 hello 相同方便處理資料庫資料與 MVC 處理使用者輸入。 因為 MVC 和 hello 資料庫支援類似的模型，例如 POCO 物件似乎相同類別的這兩種用途的簡單 tooreuse hello。 考量，以及它的 toopreserve 分隔是其中一個常見區域，其中非預期的屬性是此作法失敗公開 toomodel 繫結，啟用過度張貼攻擊。</li><li>**為什麼不應該使用我的未篩選的資料庫模型類別當做參數 toomy MVC 動作？-**因為 MVC 模型繫結會將繫結的任何項目在該類別。 即使 hello 的資料不會出現在檢視中，惡意使用者可以使用此資料包含，傳送 HTTP 要求和 MVC 會很樂意將它繫結動作指出資料庫類別 hello 圖形的資料，因為它應該接受使用者輸入。</li><li>**為何應該重視 hello 圖形使用模型繫結？-**與過度廣泛的模型使用 ASP.NET MVC 模型繫結公開應用程式 tooover 張貼攻擊。 過度張貼可能會讓攻擊者 toochange 應用程式資料超過預期，例如覆寫項目或 hello 安全性帳戶的權限的 hello 價格哪些 hello 開發人員。 應用程式應該使用何種不受信任的輸入 tooallow 透過模型繫結的特定動作繫結模型 （或特定允許的內容篩選器清單） tooprovide 明確的合約。</li><li>**要擁有個別的繫結模型是否只要複製程式碼即可？-** 否，此作業和關注點分離有關。 如果您重複使用動作方法中的資料庫模型，您對任何屬性 （或子屬性），類別可以設定的 HTTP 要求中的 hello 使用者。 如果這不是您想要的 MVC toodo，您需要的篩選器清單或個別的類別圖形 tooshow MVC 哪些資料可以來自使用者改為輸入。</li><li>**如果有使用者輸入的個別繫結模型，有 tooduplicate 我資料附註屬性？-**不一定。 您可以使用 MetadataTypeAttribute hello 資料庫模型類別 toolink toohello 上的中繼資料的模型繫結類別上。 只 hello hello MetadataTypeAttribute 所參考類型的附註必須是參考的類型 （可能有較少的屬性，但不得超過） hello 的子集。</li><li>**在使用者輸入模型和資料庫模型之間來回移動資料很麻煩。是否可以使用反映功能直接複製所有屬性？-** 是。 hello 會出現在 hello 繫結模型的屬性會判斷使用者輸入安全 toobe hello 的。 沒有安全性理由而無法使用反映 toocopy 透過共同存在這兩個模型之間的所有屬性。</li><li>**您認為 [Bind(Exclude ="â€¦")] 如何。我能否使用此方法而不使用個別的繫結模型？-** 不建議使用這個方法。 使用 [Bind(Exclude ="â€¦")] 表示任何新的屬性預設都是可繫結的。 加入新的屬性之後，額外的步驟 tooremember tookeep 項目是安全的而非具有 hello 設計是安全的預設值。 Hello 開發人員檢查這份清單，每次會新增的屬性是根據風險。</li><li>**[Bind(Include ="â€¦")] 適用於編輯作業嗎？-** 否。 [Bind(Include ="â€¦")] 僅適用於插入樣式的作業 (新增資料)。 更新樣式作業 （修改現有的資料），會使用另一個方法，例如擁有個別的繫結模型，或傳遞明確允許的屬性 tooUpdateModel 或 TryUpdateModel 的清單。 加入 [繫結 (Include ="「 正確 」。 「)] 上的編輯作業的屬性表示 MVC 將會建立物件執行個體，並設定只 hello 列出屬性，讓其他所有在其預設值。 Hello 資料保存時，它會完全取代 hello 現有實體，重設任何省略的屬性 tootheir 預設值為 hello 值。 例如，如果省略 IsAdmin [繫結 (Include ="「 正確 」。 「)] 屬性上的編輯作業，任何使用者名稱已在編輯過透過這個動作會重設 tooIsAdmin = false （已編輯的任何使用者會失去管理員狀態）。 如果您想 tooprevent 更新 toocertain 屬性，請使用其中一個 hello 上方的其他方法。 請注意，某些版本的 MVC 工具會對編輯作業上的 [Bind(Include ="â€¦")] 產生控制器類別，並表示從該清單中移除屬性會防止 over-posting 攻擊。 不過，如上面所述，該方法無法如預期運作，而改為將會重設中省略的 hello 屬性 tootheir 預設值的任何資料。</li><li>**針對建立作業使用 [Bind(Include ="â€¦")] 而非使用個別繫結模型，是否有需要注意的事項？-** 是。 首先，這個方法不適用於編輯案例，需要維護兩種不同方法來降低所有 over-posting 弱點。 第二個、 個別的繫結模型，強制執行 「 重要性分離用於用於持續性，使用者輸入和 hello 圖形的 hello 圖形之間的項目 [繫結 (Include ="â € 正確 」。 「)] 不會執行。 第三，請注意，[繫結 (Include ="â € 正確 」。 「)] 只能處理最上層屬性。您無法允許 hello 屬性中的部分 （例如"Details.Name") 的子屬性。 最後，也可能是最重要的，使用 [繫結 (Include ="â € 正確 」。 「)] 新增額外的步驟，必須記住任何階段 hello 類別用於模型繫結。 如果新的動作方法會直接繫結 toohello 資料類別，且忘記 tooinclude [繫結 (Include ="「 正確 」。 「)] 屬性，它可以很容易遭受 tooover 張貼攻擊，因此 hello [繫結 (Include ="「 正確 」。 「)] 的方法是比較安全的預設值。 如果您使用 [繫結 (Include ="â € 正確 」。 「)]，小心一律 tooremember toospecify 它每次您的資料類別會顯示為動作方法參數。</li><li>**建立作業的情況為何放 hello [繫結 (Include ="â € 正確 」。 「)] 上 hello 模型類別本身的屬性？不是這種方法是否避免 hello 需要 tooremember 放 hello 屬性上每個動作方法？-**這個方法在某些情況下的效果。 使用 [繫結 (Include ="â € 正確 」。 「)] hello 模型型別本身 （而不是在使用這個類別的動作參數），並避免 hello 需要 tooremember tooinclude hello [繫結 (Include ="â € 正確 」。 「)] 上每個動作方法的屬性。 直接在 hello 類別上有效地使用 hello 屬性建立個別的介面區，此類別的模型繫結用途。 不過，此方法只允許在每個模型類別上使用一個模型繫結外觀。 如果其中一個動作方法需要 tooallow 模型繫結的欄位 （例如，僅限系統管理員動作，以更新使用者角色），而不需要其他動作 tooprevent 模型繫結，此欄位，這種方法將無法運作。 每一個類別只能有一個模型繫結] 圖形。如果不同的動作需要不同的模型繫結圖形，他們需要的 toorepresent 這些分隔圖形使用其中一個個別的模型繫結類別，或是不同的 [繫結 (Include ="â € 正確 」。 「)] 上 hello 動作方法的屬性。</li><li>**何謂繫結模型？會在 hello 檢視模型相同的動作嗎？-**這些是兩個相關的概念。 模型繫結是指在動作中使用 tooa 模型類別 hello 詞彙是參數清單 （hello 圖形從 MVC 模型繫結 toohello 動作方法傳遞）。 hello 詞彙檢視模式是指從動作方法 tooa 檢視傳遞 tooa 模型類別。 使用特定檢視的模型是常見的方法，將資料傳遞從動作方法 tooa 檢視。 通常，此圖形也適用於模型繫結，而且 hello 詞彙檢視模型可以是相同的模型使用兩個地方使用的 toorefer hello。 toobe 精確，特別是有關繫結模型，將焦點放在 hello 圖形傳遞 toohello 動作，就是進行大量指派關切的事項討論此程序。</li></ul>| 

## <a id="rendering"></a>編碼不受信任的 web 輸出先前 toorendering

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、Web Form、MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | [如何在 ASP.NET 中的 tooprevent 跨網站指令碼](http://msdn.microsoft.com/library/ms998274.aspx)，[跨網站指令碼處理](http://cwe.mitre.org/data/definitions/79.html)， [XSS （跨網站指令碼） 預防小工作表](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **步驟** | 跨網站指令碼 （通常縮寫為 XSS） 是線上服務或取用輸入 hello web 從任何應用程式/元件的攻擊媒介。 XSS 弱點可能會允許攻擊者 tooexecute 指令碼透過易受攻擊的 web 應用程式的其他使用者的電腦上。 惡意的指令碼可以使用的 toosteal cookie 和否則竄改透過 JavaScript 犧牲者的電腦。 若要預防 XSS，您可以驗證使用者輸入、確保其格式正確無誤並先加以編碼，再轉譯於網頁中。 使用 Web Protection Library 即可進行輸入驗證和輸出編碼。 用於 Managed 程式碼 (C\#，VB.net 等)，請使用其中一個或多個適當的編碼方式，從 hello Web 保護 (反 XSS) 程式庫，視 hello 取得在： 認定 hello 使用者輸入的內容而定：| 

### <a name="example"></a>範例

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>對所有字串類型的模型屬性執行輸入驗證和篩選

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | [新增驗證](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation)、[驗證 MVC 應用程式中的模型資料](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)、[ASP.NET MVC 應用程式的指導原則](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **步驟** | <p>必須先驗證所有 hello 輸入的參數，它們會以 hello 應用程式 tooensure 安全防護 hello 應用程式時，會針對惡意的使用者輸入。 驗證 hello 與白名單驗證策略的伺服器端上，使用規則運算式驗證輸入的值。 Unsanitized 使用者輸入傳遞 toohello 方法的參數會使程式碼資料隱碼弱點 /。</p><p>對於 Web 應用程式，進入點還可能包括表單欄位、QueryStrings、Cookie、HTTP 標頭和 Web 服務參數。</p><p>hello 下列輸入的驗證檢查必須執行根據模型繫結：</p><ul><li>hello 模型屬性加以註解與 RegularExpression 註釋，以接受允許的字元和最大允許長度</li><li>hello 控制器方法應該執行 ModelState 有效性</li></ul>|

## <a id="richtext"></a>應該對接受所有字元的表單欄位 (例如 RTF 編輯器) 套用清理

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [將不安全的輸入編碼](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3)， [HTML 清理程式](https://github.com/mganss/HtmlSanitizer) |
| **步驟** | <p>找出所有您想 toouse 的 static 標記標籤。 常見的作法是 toorestrict 格式化 toosafe HTML 項目，例如`<b>`（粗體） 和`<i>`（斜體）。</p><p>寫入 HTML 編碼的 hello 資料之前它。 這可將安全方法是讓它 toobe 任何惡意指令碼當做文字處理，不是可執行程式碼。</p><ol><li>停用 ASP.NET 要求驗證加 hello hello ValidateRequest ="false"屬性 toohello @ Page 指示詞</li><li>編碼 hello 字串輸入 hello HtmlEncode 方法</li><li>使用 StringBuilder 和其取代方法 tooselectively 移除 hello 想 toopermit 編碼 hello HTML 項目上呼叫</li></ol><p>hello 頁面中的 hello 參考會停用 ASP.NET 要求的驗證設定`ValidateRequest="false"`。 它將 HTML 編碼的 hello 輸入，並選擇性地允許 hello`<b>`和`<i>`或者，也可以使用 HTML 處理.NET 程式庫。</p><p>HtmlSanitizer 是清除的 HTML 片段與文件的建構，可能會導致 tooXSS 攻擊的.NET 程式庫。 它會使用 AngleSharp tooparse、 操作及呈現 HTML 和 CSS。 HtmlSanitizer 可以安裝以 NuGet 套件，並 hello 使用者輸入可傳遞相關 HTML 或 CSS 處理方法，視需要在 hello 伺服器端上。 請注意，只有在迫不得已時才可考慮使用清理做為安全性控制方法。</p><p>輸入驗證和輸出編碼會是較佳的安全性控制方法。</p> |

## <a id="inbuilt-encode"></a>未指派並沒有內建的編碼方式的 DOM 項目 toosinks

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 許多 javascript 函式預設不會進行編碼。 指派不受信任的輸入的 tooDOM 項目，透過這類函式時，可能會導致跨網站指令碼 (XSS) 執行。| 

### <a name="example"></a>範例
以下是不安全的範例︰ 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
請勿使用 `innerHtml`；而應使用 `innerText`。 同樣地，不要使用 `$("#elm").html()`，而應使用 `$("#elm").text()` 

## <a id="redirect-safe"></a>驗證所有重新導向 hello 應用程式中的都已關閉或安全地完成

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [hello OAuth 2.0 授權架構-開啟重新導向程式](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **步驟** | <p>設計應用程式要求重新導向 tooa 使用者提供的位置必須限制 hello 可能重新導向目標 tooa 預先定義 「 安全 」 清單的站台或網域。 Hello 應用程式中的所有重新導向必須關閉/安全。</p><p>toodo 這樣：</p><ul><li>找出所有重新導向</li><li>為每個重新導向實作適當的風險降低措施。 適當的風險降低措施包括重新導向允許清單或使用者確認。 如果具有開啟重新導向弱點的網站或服務使用 Facebook/OAuth/OpenID 身分識別提供者，攻擊者便可竊取使用者的登入權杖，然後假扮該使用者。 這是固有的風險時使用 OAuth，而其記錄在 RFC 6749"hello OAuth 2.0 授權架構"，區段 10.15"開啟重新導向 」 同樣地，使用者的認證可以受到使用開啟的重新導向矛網路釣魚攻擊</li></ul>|

## <a id="string-method"></a>對控制器方法所接受的所有字串類型參數實作輸入驗證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | [驗證 MVC 應用程式中的模型資料](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)、[ASP.NET MVC 應用程式的指導原則](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **步驟** | 對於只接受基本資料類型而不接受模型來做為引數的方法，應該使用規則運算式進行輸入驗證。 在此，Regex.IsMatch 應搭配使用有效的 regex 模式。 如果不符合 hello 輸入 hello 指定的規則運算式，控制項應該不會繼續，而且提供適當的警告，關於驗證失敗應該會顯示。| 

## <a id="dos-expression"></a>設定處理 tooprevent DoS 到期 toobad 規則運算式的規則運算式的上限逾時

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、Web Form、MVC5、MVC6  |
| **屬性**              | N/A  |
| **參考**              | [DefaultRegexMatchTimeout 屬性](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **步驟** | tooensure 阻斷服務攻擊格式不建立規則運算式，會造成大量回溯，設定 hello 全域預設逾時。 如果花費的時間超出 hello 定義上限 hello 處理時間，則會擲回逾時例外狀況。 如果進行任何設定，則會是無限 hello 逾時。| 

### <a name="example"></a>範例
例如，hello 下列組態將會擲回 RegexMatchTimeoutException，如果 hello 處理時間超過 5 秒： 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>避免在 Razor 檢視中使用 Html.Raw

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| 步驟 | ASP.Net 網頁 (Razor) 會執行自動 HTML 編碼。 內嵌程式碼區塊 (@ blocks) 所列印的所有字串會自動進行 HTML 編碼。 不過，在叫用 `HtmlHelper.Raw` 方法時，它會傳回非 HTML 編碼的標記。 如果`Html.Raw()`helper 方法，則它會略過 hello 自動編碼 Razor 提供保護。|

### <a name="example"></a>範例
以下是不安全的範例︰ 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
請勿使用`Html.Raw()`除非需要 toodisplay 標記。 這個方法不會隱含執行輸出編碼。 請使用其他 ASP.NET 協助程式，例如 `@Html.DisplayFor()` 

## <a id="stored-proc"></a>請勿在預存程序中使用動態查詢

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>SQL 資料隱碼攻擊利用輸入的驗證 toorun 任意命令 hello 資料庫中的弱點。 它可能發生在您的應用程式會使用輸入的 tooconstruct 動態 SQL 陳述式 tooaccess hello 資料庫。 如果您的程式碼使用預存程序來傳遞包含原始使用者輸入的字串，也可能發生此弱點。 使用 hello SQL 插入式攻擊，hello 攻擊者可以在 hello 資料庫中執行任意命令。 （包括 hello SQL 陳述式中的預存程序） 的所有 SQL 陳述式必須是參數都化。 參數化的 SQL 陳述式會接受字元而不會有問題 （例如，單引號） 的特殊意義 tooSQL 具有強型別。 |

### <a name="example"></a>範例
以下是不安全的動態預存程序範例︰ 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>範例
以下是安全地實作相同的預存程序的 hello: 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>確定 Web API 方法已完成模型驗證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | [ASP.NET Web API 中的模型驗證](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **步驟** | 用戶端傳送資料 tooa web API，時，強制 toovalidate hello 資料之前進行任何處理。 接受的 ASP.NET Web Api 的模型做為輸入，會使用資料註解 hello 屬性 hello 模型的模型 tooset 驗證規則。|

### <a name="example"></a>範例
下列程式碼的 hello 示範 hello 相同： 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>範例
Hello 的 hello API 控制器動作方法，在 hello 模型的有效性會具有 toobe 明確檢查過如下所示： 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>對 Web API 方法所接受的所有字串類型參數實作輸入驗證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、MVC 5、MVC 6 |
| **屬性**              | N/A  |
| **參考**              | [驗證 MVC 應用程式中的模型資料](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)、[ASP.NET MVC 應用程式的指導原則](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **步驟** | 對於只接受基本資料類型而不接受模型來做為引數的方法，應該使用規則運算式進行輸入驗證。 在此，Regex.IsMatch 應搭配使用有效的 regex 模式。 如果不符合 hello 輸入 hello 指定的規則運算式，控制項應該不會繼續，而且提供適當的警告，關於驗證失敗應該會顯示。|

## <a id="typesafe-api"></a>確定 Web API 有使用 type-safe 參數來存取資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>如果您使用 hello 參數集合，SQL 會視為 hello 輸入是做為常值，而不是可執行程式碼。 hello 參數集合可以是輸入資料上的使用的 tooenforce 類型和長度條件約束。 Hello 範圍以外的值會觸發例外狀況。 如果不使用類型安全的 SQL 參數，攻擊者可能會內嵌在 hello 進行篩選輸入可以 tooexecute 資料隱碼攻擊。</p><p>當建構 SQL 查詢中發生的未篩選的輸入的 tooavoid 可能 SQL 資料隱碼攻擊時，請使用類型安全的參數。 type-safe 參數可與預存程序和動態 SQL 陳述式搭配使用。 參數都會視做為常值 hello 資料庫，而不是可執行程式碼。 參數的類型和長度也會受到檢查。</p>|

### <a name="example"></a>範例
hello 下列程式碼顯示如何 toouse 型別以 hello SqlParameterCollection 安全參數呼叫預存程序時。 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
在上述程式碼範例的 hello，hello 輸入的值不能超過 11 個字元。 如果 hello 資料不符合 toohello 型別或 hello 參數所定義的長度，hello SqlParameter 類別擲回例外狀況。 

## <a id="sql-docdb"></a>針對 Cosmos DB 使用參數化 SQL 查詢

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure Document DB | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [在 DocumentDB 中宣佈 SQL 參數化](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) |
| **步驟** | 雖然 DocumentDB 只支援唯讀查詢，但如果查詢是藉由串連使用者輸入來建構，仍可以發動 SQL 插入式攻擊。 可能會讓它們不應該存取 hello 內使用者 toogain 存取 toodata 相同集合中依製作惡意的 SQL 查詢。 如果查詢是根據使用者輸入所建構而成，請使用參數化的 SQL 查詢。 |

## <a id="schema-binding"></a>透過結構描述繫結驗證 WCF 輸入

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **步驟** | <p>缺乏驗證會導致 toodifferent 型別資料隱碼攻擊。</p><p>訊息驗證代表一個防線 hello 保護您的 WCF 應用程式中。 使用此方法時，您可以驗證使用結構描述 tooprotect WCF 免於遭受惡意用戶端的服務作業的訊息。 驗證由 hello 用戶端 tooprotect hello 用戶端免受攻擊接收惡意服務的所有訊息。 訊息驗證可讓可能 toovalidate 訊息作業取用訊息合約或資料合約，無法完成時，使用參數驗證。 訊息驗證可讓您在結構描述，藉以提供更大的彈性，並減少開發時間內 toocreate 驗證邏輯。 建立標準資料表示法的 hello 組織內部的不同應用程式可以重複使用結構描述。 此外，訊息驗證可讓您 tooprotect 作業時，它們會消耗涉及合約表示商務邏輯的複雜資料型別。</p><p>tooperform 訊息驗證，您先建立的結構描述，表示您的服務和 hello 資料型別這些作業所耗用的 hello 作業。 然後，您會建立會實作自訂用戶端訊息偵測器和自訂發送器訊息偵測器 toovalidate hello 訊息從 hello 服務傳送/接收.NET 類別。 接下來，您可以實作自訂端點行為 tooenable 訊息驗證用戶端 hello 和 hello 服務上。 最後，您會在 hello 類別，可讓您 tooexpose hello 擴充 hello 服務或 hello 用戶端 hello 組態檔中的自訂端點行為上實作的自訂組態項目 」</p>|

## <a id="parameters"></a>透過參數偵測器驗證 WCF 輸入

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **步驟** | <p>輸入和資料驗證代表一個重要防線 hello 保護您的 WCF 應用程式中。 您應該驗證服務中公開 WCF 服務作業 tooprotect hello 免於遭受惡意用戶端的所有參數。 相反地，您也應該驗證所有惡意服務所收到 hello 用戶端 tooprotect hello 用戶端不受攻擊的傳回值</p><p>WCF 會提供不同的擴充性點，讓您 toocustomize hello WCF 執行階段行為藉由建立自訂延伸模組。 訊息偵測器 」 和 「 參數偵測器時可以使用兩個擴充性機制使用 toogain 進一步控制用戶端和服務之間傳遞的 hello 資料。 您應該使用參數偵測器的輸入驗證，並需要服務上進出 tooinspect hello 整個訊息時才使用訊息偵測器。</p><p>tooperform 輸入驗證，您會建置.NET 類別，實作自訂參數偵測器作業順序 toovalidate 參數中，在您的服務。 您接著將 hello 用戶端和 hello 服務上實作自訂端點行為 tooenable 驗證。 最後，您將可讓您 tooexpose hello 擴充 hello 服務或 hello 用戶端 hello 組態檔中的自訂端點行為的 hello 類別上實作自訂組態項目</p>|
