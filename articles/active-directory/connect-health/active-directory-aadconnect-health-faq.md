---
title: "aaaAzure Active Directory 連線健全狀況常見問題集-Azure |Microsoft 文件"
description: "此常見問題集會回答 Azure AD Connect Health 的相關問題。 此常見問題集涵蓋使用 hello 服務，包括 hello 計費模型、 功能、 限制，以及支援的相關問題。"
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Azure AD Connect Health 常見問題集
這篇文章包含有關 Azure Active Directory (Azure AD) 連線的健康情況集 (faq) 解答 toofrequently。 這些常見問題集涵蓋疑問 toouse hello 服務，其中包括 hello 計費模型、 功能、 限制，以及支援的方式。

## <a name="general-questions"></a>一般問題
**問：我管理多個 Azure AD 目錄。我要如何切換 toohello 具有 Azure Active Directory Premium？**

tooswitch 不同 Azure AD 租用戶，選取 hello 目前登入的**使用者名**在 hello 右上角，然後選擇 hello 適當的帳戶。 如果此處未列出 hello 帳戶，請選取**登出**，然後再使用 hello 全域系統管理員認證具有 Azure Active Directory Premium 的 hello 目錄啟用 toosign 中的。

**問︰Azure AD Connect Health 支援哪個版本的身分識別角色？**

hello 下表列出 hello 角色，並支援的作業系統版本。

|角色| 作業系統/版本|
|--|--|
|Active Directory Federation Services (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | 版本 1.0.9125 或更高版本|
|Active Directory Domain Services (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

請注意 hello hello 服務所提供的功能可能不同，根據 hello 角色和 hello 作業系統而不同。 換句話說，所有 hello 功能可能無法供所有作業系統版本。 請參閱 hello 功能描述，如需詳細資訊。

**問： 如何授權執行我的基礎結構需要 toomonitor？**

* hello 第一個 Connect Health 代理程式需要至少一個 Azure AD Premium 授權。
* 每多一個註冊代理程式，就需要再 25 個 Azure AD Premium 授權。
* 代理程式計數是跨越所有受監視的角色 （AD FS、 Azure AD Connect，及/或 AD DS） 中註冊的代理程式的對等 toohello 總數。

授權資訊也可以找到上 hello [Azure AD 定價頁面](https://aka.ms/aadpricing)。

範例：

| 已註冊的代理程式 | 需要的授權 | 監視組態範例 |
| ------ | --------------- | --- |
| 1 | 1 | 1 個 Azure AD Connect 伺服器 |
| 2 | 26| 1 個 Azure AD Connect 伺服器、1 個網域控制站 |
| 3 | 51 | 1 個 Active Directory Federation Services (AD FS) 伺服器、1 個 AD FS Proxy、1 個網域控制站 |
| 4 | 76 | 1 個 AD FS 伺服器、1 個 AD FS Proxy、2 個網域控制站 |
| 5 | 101 | 1 個 Azure AD Connect 伺服器、1 個 AD FS 伺服器、1 個 AD FS Proxy、2 個網域控制站 |


## <a name="installation-questions"></a>安裝問題

**問： hello 的 hello Azure AD Connect Health 代理程式安裝在個別伺服器上的影響為何？**

與尊重 toohello CPU、 記憶體耗用量、 網路頻寬和儲存體最小的 hello 影響安裝 hello Microsoft Azure AD Connect Health 代理程式，AD FS web 應用程式 proxy 伺服器，Azure AD Connect （同步） 伺服器、 網域控制站。

下列數字的 hello 是近似值：

* CPU 耗用量：增加約 1-5%。
* 記憶體耗用量： too10%的 hello 系統總記憶體。

> [!NOTE]
> 如果 hello 代理程式無法與 Azure 通訊，hello 代理程式會儲存 hello 資料在本機定義的最大限制。 hello 代理程式會覆寫 hello 「 快取 」 的資料，「 最近最少服務 」 為基礎。
>
>

* Azure AD Connect Health 代理程式的本機緩衝區儲存體：約 20 MB。
* AD FS 伺服器，我們建議，您佈建 Azure AD Connect Health 代理程式 tooprocess 的 hello AD FS 稽核通道 1024 MB (1 GB) 的磁碟空間 hello 的所有稽核資料之前會覆寫。

**問： 我可以 tooreboot 我的伺服器 hello hello Azure AD Connect Health 代理程式安裝期間嗎？**

否。 hello 安裝 hello 代理程式不會要求您 tooreboot hello 伺服器。 不過，某些先決條件步驟的安裝可能需要 hello 伺服器重新的開機。

例如，在 Windows Server 2008 R2 上安裝 .NET 4.5 Framework 需要重新啟動伺服器。

**問：Azure AD Connect Health 是否透過傳遞 Http Proxy 運作？**

是。 針對進行中操作，您可以設定 hello 健康情況代理程式 toouse HTTP proxy tooforward 傳出 HTTP 要求。
深入了解[設定 Health 代理程式的 HTTP Proxy](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy)。

如果您需要 tooconfigure proxy 代理程式註冊期間，您可能需要 toomodify Internet Explorer Proxy 設定事先。

1. 開啟 Internet Explorer > [設定]  >  [網際網路選項]  >  [連線]  >  [LAN 設定]。
2. 選取 [在您的區域網路使用 Proxy 伺服器]。
3. 如果您有不同的 Proxy 連接埠供 HTTP 和 HTTPS/安全使用，請選取 [進階]。

**問： 沒有 Azure AD Connect Health 支援基本驗證連接 tooHTTP proxy 時？**

否。 機制 toospecify 任意使用者名稱和密碼進行基本驗證目前不支援。

**問： 哪些防火牆連接埠是否需要 hello Azure AD Connect Health 代理程式 toowork tooopen 嗎？**

請參閱 hello[需求 > 一節](active-directory-aadconnect-health-agent-install.md#requirements)hello 清單的防火牆連接埠與其他連線的需求。

**問： 為什麼看兩部伺服器以相同的名稱，在 hello Azure AD Connect Health 入口網站中的 hello？**

當您從伺服器移除代理程式時，hello 伺服器是不會自動移除 hello Azure AD Connect Health 入口網站。 如果您以手動方式從伺服器移除代理程式，或移除 hello 伺服器本身，您會需要 toomanually 刪除 hello 伺服器項目從 hello Azure AD Connect Health 入口網站。

您可能會在伺服器重新製作映像，或建立新的伺服器 hello 與相同的詳細資訊 （例如電腦名稱）。 如果您並未從 hello Azure AD Connect Health 入口網站中，移除 hello 已註冊的伺服器，而且您 hello 新的伺服器上安裝 hello 代理程式，您可能會看到兩個項目以 hello 相同的名稱。

在此情況下，手動刪除屬於 toohello 舊伺服器 hello 項目。 此伺服器 hello 資料應過期。

## <a name="health-agent-registration-and-data-freshness"></a>Health 代理程式註冊和資料有效性

**問： 什麼是 hello 健全狀況代理程式註冊失敗的常見原因，以及如何疑難排解問題？**

hello 健康情況代理程式可能會失敗 tooregister 到期 toohello 下列可能的原因：

* hello 代理程式無法與所需的 hello 端點通訊，因為防火牆封鎖流量。 在 Web 應用程式 Proxy 伺服器上尤其常見。 請確定您已允許連出通訊所需的 toohello 端點及連接埠。 請參閱 hello[需求 > 一節](active-directory-aadconnect-health-agent-install.md#requirements)如需詳細資訊。
* 連出通訊是由 hello 網路層膨脹 tooan SSL 檢查。 這會導致 hello 憑證 hello 代理程式會使用 toobe 取代 hello 檢查伺服器/實體，然後 hello 步驟 toocomplete hello 代理程式註冊失敗。
* hello 使用者沒有存取 tooperform hello 登錄 hello 代理程式。 根據預設，全域系統管理員具有存取權。 您可以使用[Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate 存取 tooother 使用者。

**問： 我已開始收到警示，「 健全狀況服務的資料不是向上 toodate。 」如何疑難排解 hello 問題？**

它不會收到 hello 的所有資料點 hello 伺服器 hello 中最後兩小時時，azure AD Connect Health 便會產生 hello 警示。 有很多原因都可能導致引發此警示。

* hello 代理程式無法與所需的 hello 端點通訊，因為防火牆封鎖流量。 在 Web 應用程式 Proxy 伺服器上尤其常見。 請確定您已允許連出通訊所需的 toohello 結束點及連接埠。 請參閱 hello[需求 > 一節](active-directory-aadconnect-health-agent-install.md#requirements)如需詳細資訊。
* 連出通訊是由 hello 網路層膨脹 tooan SSL 檢查。 這會導致 hello 憑證 hello 代理程式會使用 toobe 取代 hello 檢查伺服器/實體，然後 hello 程序失敗 tooupload 資料 toohello Azure AD Connect Health 服務。
* 您可以使用內建 hello 代理程式的 hello 連線命令。 [閱讀更多資訊](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)。
* hello 代理程式也支援透過未經驗證的 HTTP Proxy 的傳出連線。 [閱讀更多資訊](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy)。

## <a name="operations-questions"></a>操作問題
**問： 我需要 tooenable hello web 應用程式 proxy 伺服器上的稽核嗎？**

否，稽核不需要 toobe hello web 應用程式 proxy 伺服器上啟用。

**問：Azure AD Connect Health 警示如何獲得解決？**

Azure AD Connect Health 警示會在成功情況下獲得解決。 Azure AD Connect Health 代理程式偵測，並定期報告 hello 成功條件 toohello 服務。 有幾項警示的 hello 隱藏項目是以時間為基礎。 換句話說，如果 hello 相同錯誤狀況未觀察到的警示產生 72 個小時內，會自動解決 hello 警示。

**問： 我已開始收到警示，「 測試驗證要求 （綜合交易） 無法 tooobtain 語彙基元。 」如何疑難排解 hello 問題？**

Hello 安裝 AD FS 伺服器上的健全狀況代理程式失敗 tooobtain 權杖做為起始的 hello 健康情況代理程式的綜合交易的一部分時，azure AD Connect Health 的 AD FS 會產生此警示。 hello 健康情況代理程式會使用 hello 本機系統內容，並嘗試本身的信賴憑證者合作對象 tooget 語彙基元。 這是所有測試 tooensure AD FS 已發行權杖的狀態。

通常這項測試失敗，因為 hello 健康情況代理程式是無法 tooresolve hello AD FS 伺服器陣列名稱。 這種情況 hello AD FS 伺服器是網路負載平衡器後方，而且 hello 要求取得初始化的節點為 hello 負載平衡器後方 （相對於的 tooa 一般用戶端 hello 負載平衡器前面）。 這可以藉由修復更新 hello"hosts"檔案位於"C:\Windows\System32\drivers\etc"tooinclude hello 的 hello AD FS 伺服器的 IP 位址或回送 IP 位址 (127.0.0.1) hello AD FS 伺服器陣列名稱 （例如，sts.contoso.com)。 加入 hello 主機檔案，將會最少運算 hello 的網路呼叫，進而 hello 健康情況代理程式 tooget hello 語彙基元。

**問： 我收到一封電子郵件，指出 我的電腦不修補 hello 最近 ransomeware 攻擊。我為什麼收到這封電子郵件？**

Azure AD Connect Health 服務掃描它會監視 tooensure hello 所需的修補程式的電腦已安裝的所有 hello。 hello 電子郵件已傳送 toohello 租用戶系統管理員，如果至少一部電腦沒有 hello 的重大修補程式。 下列邏輯 hello 已使用的 toomake 這項判斷。
1. 尋找所有 hello hotfix 安裝在 hello 電腦上。
2. 檢查是否至少一個從 hello hello Hotfix 定義清單會出現。
3. 如果是，hello 機器已受保護。 如果沒有，hello 機器位於 hello 攻擊的風險。

您可以使用下列 PowerShell 指令碼 tooperform hello 這個核取以手動方式。 它會實作 hello 上方邏輯。

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>相關連結
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 代理程式安裝](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 操作](active-directory-aadconnect-health-operations.md)
* [在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)
* [使用 Azure AD Connect Health 進行同步處理](active-directory-aadconnect-health-sync.md)
* [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health 版本歷程記錄](active-directory-aadconnect-health-version-history.md)
