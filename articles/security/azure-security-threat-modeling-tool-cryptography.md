---
title: "aaaCryptography-Microsoft 威脅模型化工具-Azure |Microsoft 文件"
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
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>安全性架構︰密碼編譯 | 風險降低 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **Web 應用程式** | <ul><li>[只使用核准的對稱區塊編碼器和金鑰長度](#cipher-length)</li><li>[針對對稱編碼器使用核准的區塊編碼器模式和初始化向量](#vector-ciphers)</li><li>[使用核准的非對稱演算法、金鑰長度和填補](#padding)</li><li>[使用核准的亂數產生器](#numgen)</li><li>[請勿使用對稱串流編碼器](#stream-ciphers)</li><li>[使用核准的 MAC/HMAC/索引雜湊演算法](#mac-hash)</li><li>[只使用核准的密碼編譯雜湊函式](#hash-functions)</li></ul> |
| **資料庫** | <ul><li>[在 hello 資料庫中使用強式加密演算法 tooencrypt 資料](#strong-db)</li><li>[SSIS 套件應予以加密和數位簽章](#ssis-signed)</li><li>[新增數位簽章 toocritical 資料庫安全性實體](#securables-db)</li><li>[使用 SQL server EKM tooprotect 加密金鑰](#ekm-keys)</li><li>[如果加密金鑰不能展現的 tooDatabase 引擎，使用永遠加密功能](#keys-engine)</li></ul> |
| **IoT 裝置** | <ul><li>[在 IoT 裝置上安全地儲存密碼編譯金鑰](#keys-iot)</li></ul> | 
| **IoT 雲端閘道** | <ul><li>[產生的隨機對稱金鑰的長度足夠驗證 tooIoT 中樞](#random-hub)</li></ul> | 
| **Dynamics CRM 行動用戶端** | <ul><li>[確定已備妥需要使用 PIN 並允許遠端抹除的裝置管理原則](#pin-remote)</li></ul> | 
| **Dynamics CRM Outlook 用戶端** | <ul><li>[確定已備妥需要 PIN/密碼/自動鎖定並會加密所有資料的裝置管理原則 (例如 Bitlocker)](#bitlocker)</li></ul> | 
| **Identity Server** | <ul><li>[確定在使用 Identity Server 時會變換簽署金鑰](#rolled-server)</li><li>[確定 Identity Server 會使用密碼編譯增強式用戶端識別碼和用戶端祕密](#client-server)</li></ul> | 

## <a id="cipher-length"></a>只使用核准的對稱區塊編碼器和金鑰長度

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>對稱的區塊密碼和相關聯的金鑰長度的已明確地核准您的組織中的 hello 密碼編譯警告器，必須使用產品。 在 Microsoft 核准對稱演算法包括 hello 遵循區塊密碼：</p><ul><li>對於新的程式碼，可接受 AES-128、AES-192 和 AES-256</li><li>對於現有程式碼的回溯相容性，可接受三金鑰 3DES</li><li>對於使用對稱區塊編碼器的產品︰<ul><li>新的程式碼需要進階加密標準 (AES)</li><li>為了回溯相容性，現有程式碼允許三金鑰三重資料加密標準 (3DES)</li><li>其他所有區塊編碼器 (包括 RC2、DES、兩金鑰 3DES、DESX 和 Skipjack) 只能用於解密舊資料，若用於加密，則必須加以取代</li></ul></li><li>對稱區塊加密演算法需要至少 128 位元的金鑰長度。 hello 僅建議用於新的程式碼的區塊加密演算法是 AES （AES 128、 AES 192 和 AES 256 均可接受）</li><li>三個索引鍵 3DES 是目前可接受，如果已在使用中現有的程式碼。建議您轉換 tooAES。 DES、DESX、RC2 和 Skipjack 不再被視為是安全的。 這些演算法可能只用於解密 hello 起見，回溯相容性的現有資料，應該重新加密資料使用建議的區塊編碼器</li></ul><p>請注意，所有的對稱區塊編碼器都必須搭配核准的編碼器模式使用，此模式需要使用適當的初始化向量 (IV)。 適當的 IV 通常是亂數，而絕不會是常數值</p><p>貴組織的密碼編譯面板檢閱之後，可能會允許將使用舊版或其他未核准的密碼編譯演算法和較小的金鑰長度 hello 讀取現有資料 （相對於的 toowriting 新資料）。 不過，您必須針對這項需求申請例外狀況。 此外，在企業部署中的產品時應該考慮警告系統管理員不安全加密編譯是使用的 tooread 資料。 此類警告應清楚說明原因並提供可採取的動作。 在某些情況下，可能是適當 toohave 群組原則控制 hello 使用弱式密碼編譯</p><p>為了實現受管理的密碼編譯靈活性所允許的 .NET 演算法 (依偏好順序)</p><ul><li>AesCng (符合 FIPS 規範)</li><li>AuthenticatedAesCng (符合 FIPS 規範)</li><li>AESCryptoServiceProvider (符合 FIPS 規範)</li><li>AESManaged (不符合 FIPS 規範)</li></ul><p>請注意 無這些演算法可以指定透過 hello`SymmetricAlgorithm.Create`或`CryptoConfig.CreateFromName`而不進行變更 toohello machine.config 檔案的方法。 此外，請注意 AES.NET 先前 too.NET 3.5 版本中的名為`RijndaelManaged`，和`AesCng`和`AuthenticatedAesCng`是 > 可透過 CodePlex 和 hello 基礎作業系統所需 CNG</p>

## <a id="vector-ciphers"></a>針對對稱編碼器使用核准的區塊編碼器模式和初始化向量

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 所有的對稱區塊編碼器都必須搭配核准的對稱編碼器模式使用。 僅將核准的 hello 模式是 CBC 及 CTS。 特別是，您應該避免 hello 電子代碼活頁簿 (ECB) 模式的作業;使用 ECB 需要您的組織 Crypto 面板檢閱。 OFB、CFB、CTR、CCM 和 GCM 或其他任何加密模式的使用，全都必須通過組織的密碼編譯委員會審核。 重複使用相同 hello 與在 「 資料流這類編碼器模式中，「 CTR，例如區塊加密的初始化向量 (IV) 可能會導致加密的資料 toobe 揭露。 所有的對稱區塊編碼器也必須搭配適當的初始化向量 (IV) 使用。 適當的 IV 是指密碼編譯增強式亂數，而絕不會是常數值。 |

## <a id="padding"></a>使用核准的非對稱演算法、金鑰長度和填補

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>禁止的密碼編譯演算法的 hello 使用引進了極大的風險 tooproduct 安全性，且必須予以避免。 產品只能使用組織的密碼編譯委員會已明確核准的密碼編譯演算法及相關聯的金鑰長度和填補。</p><ul><li>**RSA-** 可用於加密、金鑰交換和簽章。 RSA 加密，必須使用只進行 hello OAEP 或 RSA KEM 填補模式。 現有程式碼只能在為了相容性因素時使用 PKCS #1 v1.5 填補模式。 明確禁止使用 null 填補。 新的程式碼需要 > = 2048 位元的金鑰。 在經過貴組織的密碼編譯委員會審核之後，現有程式碼也可支援 < 2048 位元的金鑰，但只能用於實現回溯相容性。 < 1024 位元的金鑰只能用於解密/驗證舊資料，若用於加密或簽署作業，則必須加以取代</li><li>**ECDSA-** 只能用於簽章。 新的程式碼需要金鑰位元數 > = 256 的 ECDSA。 ECDSA 為基礎的簽章必須使用其中一個 hello 三個核准 NIST 曲線 (P-256、 P-384 或 P521)。 在經過貴組織的密碼編譯委員會審核之後，才能使用已經過徹底分析的曲線。</li><li>**ECDH-** 只能用於金鑰交換。 新的程式碼需要金鑰位元數 > = 256 的 ECDH。 ECDH 為基礎的金鑰交換必須使用其中一個 hello 三個核准 NIST 曲線 (P-256、 P-384 或 P521)。 在經過貴組織的密碼編譯委員會審核之後，才能使用已經過徹底分析的曲線。</li><li>**DSA-** 在經過貴組織的密碼編譯委員會審核並核准之後即可接受。 請連絡您的安全性 advisor tooschedule 貴組織的密碼編譯面板檢閱。 如果貴用戶使用 DSA 核准之後，請注意，您將需要 tooprohibit 使用金鑰的長度小於 2048 位元。 自 Windows 8 開始，CNG 支援長度為 2048 位元 (含) 以上的金鑰。</li><li>**Diffie-Hellman-** 只能用於工作階段金鑰管理。 新的程式碼需要長度 > = 2048 位元的金鑰。 在經過貴組織的密碼編譯委員會審核之後，現有程式碼也可支援長度 < 2048 位元的金鑰，但只能用於實現回溯相容性。 不得使用 < 1024 位元的金鑰。</li><ul>

## <a id="numgen"></a>使用核准的亂數產生器

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>產品必須使用核准的亂數產生器。 虛擬亂數的函式，例如 hello C 執行階段函式 rand、 hello.NET Framework 類別 System.Random 或系統函數，例如 GetTickCount 必須，因此，永遠不會使用這類程式碼中。 禁止使用 hello 雙重橢圓曲線亂數產生器 (DUAL_EC_DRBG) 演算法</p><ul><li>**CNG-** BCryptGenRandom （hello BCRYPT_USE_SYSTEM_PREFERRED_RNG 旗標，除非 hello 呼叫端執行的任何 IRQL 大於 0 [也就是 PASSIVE_LEVEL] 建議使用）</li><li>**CAPI-** cryptGenRandom</li><li>**Win32/64-** RtlGenRandom (新的實作應該使用 BCryptGenRandom 或 CryptGenRandom) * rand_s * SystemPrng (適用於核心模式)</li><li>**.NET-** RNGCryptoServiceProvider 或 RNGCng</li><li>**Windows 市集應用程式-** Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom 或 .GenerateRandomNumber</li><li>**Apple OS X (10.7+)/iOS(2.0+)-** int SecRandomCopyBytes (SecRandomRef 隨機 size_t 計數、 uint8_t*位元組)</li><li>**Apple OS X (< 10.7)-** 使用 /開發人員/隨機 tooretrieve 隨機數字</li><li>**Java (包括 Google Android Java 程式碼)-** java.security.SecureRandom 類別。 請注意，針對 Android 4.3 (軟糖 Bean)，開發人員必須遵循的 hello，Android 建議的因應措施更新他們的應用程式 tooexplicitly 初始化 hello PRNG 與從 /dev/urandom 或 /dev/random entropy</li></ul>|

## <a id="stream-ciphers"></a>請勿使用對稱串流編碼器

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 不得使用對稱串流編碼器，例如 RC4。 產品不該使用對稱串流編碼器，而該使用區塊編碼器，特別是金鑰長度至少 128 位元的 AES。 |

## <a id="mac-hash"></a>使用核准的 MAC/HMAC/索引雜湊演算法

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>產品只能使用核准的訊息驗證碼 (MAC) 或雜湊式訊息驗證碼 (HMAC) 演算法。</p><p>訊息驗證碼 (MAC) 是一段資訊附加的 tooa 訊息，可讓其收件者 tooverify 兩者 hello hello 寄件者及其 hello 完整性的 hello 訊息使用祕密金鑰。 hello 使用任一雜湊 MAC ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) 或[區塊編碼器型 MAC](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf)是允許的只要所有基礎的雜湊或對稱式加密演算法也使用; 核准目前這包含 hello HMAC SHA2 函式 （hmac-sha256、 HMAC SHA384 及 hmac-sha512） 和 hello CMAC/OMAC1 和 OMAC2 區塊編碼器為基礎的 Mac （這些 AES 為基礎）。</p><p>使用的 HMAC SHA1 可能會允許平台相容性，但您將會是必要的 toofile 例外狀況 toothis 程序，並接受貴組織的密碼編譯的檢閱。 不允許的小於 128 位元 Hmac tooless 截斷。 使用客戶方法 toohash 索引鍵和資料未獲得核准，並必須經過組織的密碼編譯面板檢閱先前 toouse。</p>|

## <a id="hash-functions"></a>只使用核准的密碼編譯雜湊函式

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>產品必須使用 hello sha-2 系列雜湊演算法 （SHA256、 SHA384 及 SHA512）。 如果需要較短的雜湊，例如順序 toofit hello 短 MD5 雜湊納入考量，使用這項設計的資料結構中的 128 位元輸出長度產品團隊可能會截斷 hello SHA2 雜湊 (通常為 SHA256) 的其中一個。 請注意，SHA384 是 SHA512 的截斷版本。 不允許針對安全性目的 tooless 小於 128 位元的加密編譯雜湊截斷。 新的程式碼不能使用 hello MD2、 MD4、 MD5、 SHA 0、 sha-1 或 RIPEMD 雜湊演算法。 這些演算法在計算時可能會發生雜湊衝突，而結果便是打斷演算法。</p><p>為了實現受管理的密碼編譯靈活性所允許的 .NET 雜湊演算法 (依偏好順序)：</p><ul><li>SHA512Cng (符合 FIPS 規範)</li><li>SHA384Cng (符合 FIPS 規範)</li><li>SHA256Cng (符合 FIPS 規範)</li><li>SHA512Managed （非 FIPS 相容） （使用 SHA512 做為演算法名稱呼叫 tooHashAlgorithm.Create 或 CryptoConfig.CreateFromName 中）</li><li>SHA384Managed （非 FIPS 相容） （使用 SHA384 演算法名稱呼叫 tooHashAlgorithm.Create 或 CryptoConfig.CreateFromName）</li><li>SHA256Managed （非 FIPS 相容） （使用 SHA256 演算法名稱呼叫 tooHashAlgorithm.Create 或 CryptoConfig.CreateFromName）</li><li>SHA512CryptoServiceProvider (符合 FIPS 規範)</li><li>SHA256CryptoServiceProvider (符合 FIPS 規範)</li><li>SHA384CryptoServiceProvider (符合 FIPS 規範)</li></ul>| 

## <a id="strong-db"></a>在 hello 資料庫中使用強式加密演算法 tooencrypt 資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [選擇加密演算法](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **步驟** | 加密演算法會定義未經授權的使用者無法輕鬆反轉的資料轉換。 SQL Server 可讓系統管理員和開發人員 toochoose 數種演算法，包括 DES、 Triple DES、 TRIPLE_DES_3KEY、 RC2、 RC4、 128 位元 RC4、 DESX、 128 位元 AES、 192 位元 AES 和 256 位元 AES 中 |

## <a id="ssis-signed"></a>SSIS 套件應予以加密和數位簽章

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [識別來源的封裝使用數位簽章 hello](https://msdn.microsoft.com/library/ms141174.aspx)，[威脅和弱點安全防護 (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **步驟** | hello 的來源封裝為個別的 hello 或建立 hello 封裝的組織。 執行來自未知或未受信任來源的套件可能有風險。 未經授權 tooprevent 的竄改的 SSIS 封裝，應使用數位簽章。 此外，在儲存體/傳輸期間的 hello 封裝 tooensure hello 機密性，SSIS 封裝有 toobe 加密 |

## <a id="securables-db"></a>新增數位簽章 toocritical 資料庫安全性實體

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [新增簽章 (Transact-SQL)](https://msdn.microsoft.com/library/ms181700) |
| **步驟** | 在 hello 資料庫完整性的重大安全性實體之 toobe 驗證的情況下，應使用數位簽章。 資料庫安全性實體 (例如預存程序、函式、組件或觸發程序) 可以加上數位簽章。 以下是時這非常有用的範例： 讓我們說出 ISV （獨立軟體廠商） 提供支援 tooa 軟體傳遞 tooone 客戶的營業。 之後，才提供支援，hello ISV 會想 tooensure hello 軟體中安全性實體的資料庫已不會遭不小心或惡意的嘗試。 如果安全性實體的 hello 經過數位簽署，hello ISV 可以驗證其數位簽章，並驗證其完整性。| 

## <a id="ekm-keys"></a>使用 SQL server EKM tooprotect 加密金鑰

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [SQL Server 可延伸金鑰管理 (EKM)](https://msdn.microsoft.com/library/bb895340)、[使用 Azure Key Vault 的可延伸金鑰管理 (SQL Server)](https://msdn.microsoft.com/library/dn198405) |
| **步驟** | SQL Server 可延伸金鑰管理可讓您保護儲存在外部裝置中，例如智慧卡、 USB 裝置或 EKM/HSM 模組 hello 資料庫檔案 toobe hello 加密金鑰。 這也會讓資料庫管理員 （除了 hello sysadmin 群組的成員） 的資料保護。 資料可以加密所使用的加密金鑰只 hello 資料庫使用者存取 tooon hello 外部 EKM/HSM 模組。 |

## <a id="keys-engine"></a>如果加密金鑰不能展現的 tooDatabase 引擎，使用永遠加密功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | SQL Azure、OnPrem |
| **屬性**              | SQL 版本 - V12、MsSQL2016 |
| **參考**              | [永遠加密 (資料庫引擎)](https://msdn.microsoft.com/library/mt163865) |
| **步驟** | 永遠加密已設計功能 tooprotect 敏感性資料，像是信用卡號碼或國家身分證字號 （例如美國社會安全號碼），儲存在 Azure SQL Database 或 SQL Server 資料庫中。 一律加密可讓用戶端 tooencrypt 用戶端應用程式內的機密資料，並永遠不會顯示 hello 加密金鑰 toohello Database Engine （SQL Database 或 SQL Server）。 如此一來，「 永遠加密 」 的區隔擁有者 hello 資料 （且可以檢視） 和管理者 hello 資料 （但應該不具備存取權） |

## <a id="keys-iot"></a>在 IoT 裝置上安全地儲存密碼編譯金鑰

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 裝置 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | 裝置作業系統 - Windows IoT 核心版、裝置連線能力 - Azure IoT 裝置 SDK |
| **參考**              | [Windows IoT 核心版上的 TPM](https://developer.microsoft.com/windows/iot/docs/tpm)、[設定 Windows IoT 核心版上的 TPM](https://developer.microsoft.com/windows/iot/win10/setuptpm)、[Azure IoT 裝置 SDK TPM](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM) |
| **步驟** | 在硬體保護的儲存體 (如 TPM 或智慧卡晶片) 中安全地對稱或憑證私密金鑰。 Windows 10 IoT 核心版支援 hello 使用者的 TPM，而且有數個可用的相容 Tpm: https://developer.microsoft.com/windows/iot/win10/tpm。 它會建議 toouse 韌體或離散的 TPM。 軟體 TPM 只應用於開發和測試用途。 一旦 TPM 而且 hello 金鑰佈建中，產生 hello 語彙基元的 hello 程式碼應該寫入不含硬式編碼的任何敏感資訊。 | 

### <a name="example"></a>範例
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
可以看出 hello 裝置主索引鍵不存在 hello 程式碼中。 相反地，它會儲存在 hello TPM 在插槽 0。 TPM 的裝置會產生短期 SAS 權杖，然後使用 tooconnect toohello IoT 中樞。 

## <a id="random-hub"></a>產生的隨機對稱金鑰的長度足夠驗證 tooIoT 中樞

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 雲端閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | 閘道選擇 - Azure IoT 中樞 |
| **參考**              | N/A  |
| **步驟** | IoT 中樞包含裝置身分識別登錄，在佈建裝置時，會自動產生隨機的對稱金鑰。 建議的 toouse hello Azure IoT 中樞身分識別登錄 toogenerate hello 索引鍵的這項功能用於驗證。 也可以建立 hello 裝置時，指定索引鍵 toobe IoT 中樞。 如果裝置佈建期間 IoT 中樞外部產生金鑰，則建議 toocreate 的隨機對稱金鑰或至少 256 位元。 |

## <a id="pin-remote"></a>確定已備妥需要使用 PIN 並允許遠端抹除的裝置管理原則

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM 行動用戶端 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 確定已備妥需要使用 PIN 並允許遠端抹除的裝置管理原則 |

## <a id="bitlocker"></a>確定已備妥需要 PIN/密碼/自動鎖定並會加密所有資料的裝置管理原則 (例如 Bitlocker)

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM Outlook 用戶端 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 確定已備妥需要 PIN/密碼/自動鎖定並會加密所有資料的裝置管理原則 (例如 Bitlocker) |

## <a id="rolled-server"></a>確定在使用 Identity Server 時會變換簽署金鑰

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Identity Server | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Identity Server - 金鑰、簽章和密碼編譯](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) |
| **步驟** | 確定在使用 Identity Server 時會變換簽署金鑰。 hello 參考一節中的 hello 連結說明如何這應該計劃而不會造成中斷 tooapplications 信賴憑證者身分識別的伺服器上。 |

## <a id="client-server"></a>確定 Identity Server 會使用密碼編譯增強式用戶端識別碼和用戶端祕密

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Identity Server | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>確定 Identity Server 會使用密碼編譯增強式用戶端識別碼和用戶端祕密。 產生用戶端識別碼和密碼時，應使用下列指導方針的 hello:</p><ul><li>產生隨機 GUID 為 hello 用戶端識別碼</li><li>產生密碼編譯隨機的 256 位元金鑰做為 hello 密碼</li></ul>|
