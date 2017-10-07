---
title: "aaaAzure Active Directory 識別身分保護腳本 |Microsoft 文件"
description: "了解如何 Azure AD Identity Protection 可讓您 toolimit hello 能力，攻擊者 tooexploit 遭盜用身分識別的裝置或 toosecure 盜用身分識別或先前已 toobe 可疑或已知的裝置。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Azure Active Directory Identity Protection 腳本
這個腳本可協助您︰

* Hello 識別身分保護環境中的資料填入模擬的風險事件和弱點
* 設定 風險為基礎的條件式存取原則和測試 hello 這些原則的影響

## <a name="simulating-risk-events"></a>模擬風險事件
此章節提供您的步驟來模擬 hello 下列風險事件類型：

* 從匿名 IP 位址登入 (容易)
* 從不熟悉的位置登入 (適中)
* 不可能的旅遊 tooatypical 位置 （困難）

無法以安全的方式模擬其他風險事件。

### <a name="sign-ins-from-anonymous-ip-addresses"></a>從匿名 IP 位址登入
此風險事件類型會識別從被視為匿名 Proxy IP 位址的 IP 位址成功登入的使用者。 這些 proxy 是 toohide 的人使用其裝置的 IP 位址，並可用於被用於惡意用途。

**登入的 toosimulate 從匿名 IP，執行下列步驟的 hello**:

1. 下載 hello [Tor 瀏覽器](https://www.torproject.org/projects/torbrowser.html.en)。
2. 太使用 hello Tor 瀏覽器中，瀏覽[https://myapps.microsoft.com](https://myapps.microsoft.com)。   
3. 輸入您想要在 hello tooappear hello 帳戶 hello 認證**從匿名 IP 位址的登入**報表。

hello 登入將會出現在 hello Identity Protection 儀表板在 5 分鐘內。 

### <a name="sign-ins-from-unfamiliar-locations"></a>從不熟悉的位置登入
hello 不熟悉位置風險是即時的登入的評估機制，會考慮過去的登入位置 (IP、 緯度 / 經度和 ASN) toodetermine 新 / 不熟悉的位置。 hello 系統會將儲存先前 Ip 時，緯度 / 經度和使用者的 Asn 會視這些 toobe 熟悉的位置。 登入位置會被視為不熟悉，如果 hello 登入位置不符合任何 hello 現有熟悉的位置。

Azure Active Directory Identity Protection：  

* 有為期 14 天的初始學習期間，在這段期間內，它不會將任何新位置標示為不熟悉的位置。
* 會忽略從熟悉的裝置和位置的地理位置關閉 tooan 現有熟悉位置登入。

toosimulate 不熟悉位置，您有 toosign 從位置和 hello 帳戶沒有登入從之前的裝置。 

**toosimulate 登入，從不熟悉的位置，執行下列步驟的 hello**:

1. 選擇至少有 14 天登入歷程記錄的帳戶。 
2. 請執行下列其中一項：
   
   a. 在使用 VPN 時，瀏覽過[https://myapps.microsoft.com](https://myapps.microsoft.com)並輸入您想 toosimulate hello 風險事件的 hello 帳戶 hello 認證。
   
   b. 要求中使用 hello 帳戶的認證 （不建議使用） 中的不同位置 toosign 關聯。

hello 登入將會出現在 hello Identity Protection 儀表板在 5 分鐘內。

### <a name="impossible-travel-tooatypical-location"></a>不可能的旅遊 tooatypical 位置
模擬 hello 不可能的旅遊條件是很困難，因為 hello 演算法會使用機器學習 tooweed 出 false-誤判，例如不可能的旅遊從熟悉的裝置或從 Vpn 所使用的 hello 目錄中的其他使用者的登入。 此外，hello 演算法需要登入的歷程記錄 3 too14 天 hello 使用者後，才開始產生風險的事件。

**toosimulate 不可能的旅遊 tooatypical 位置中，執行下列步驟的 hello**:

1. 使用標準的瀏覽器，巡覽太[https://myapps.microsoft.com](https://myapps.microsoft.com)。  
2. 輸入您想 toogenerate 不可能的旅遊風險事件的 hello 帳戶 hello 認證。
3. 變更您的使用者代理程式。 您可以在 Internet Explorer 中從 [開發人員工具] 變更使用者代理程式，或在 Firefox 或 Chrome 中使用使用者代理程式切換器附加元件來變更您的使用者代理程式。
4. 變更您的 IP 位址。 使用 VPN、Tor 附加元件，或在不同資料中心於 Azure 中啟動新機器，即可變更您的 IP 位址。
5. 登入太[https://myapps.microsoft.com](https://myapps.microsoft.com)使用 hello 之前和之後 hello 先前登入在幾分鐘內相同的認證。

hello 登入將會顯示在 hello Identity Protection 儀表板 2-4 小時內。<br>
Hello 複雜機器學習所涉及的模型，因為沒有的機會，它將無法取得挑選。<br> 您可能希望 tooreplicate 步驟執行多個 Azure AD 帳戶。

## <a name="simulating-vulnerabilities"></a>模擬弱點
弱點是 Azure AD 環境中不良執行者可以利用的弱點。 Azure AD Identity Protection 中目前顯示 3 種會運用其他 Azure AD 功能的弱點。 這些弱點會自動顯示 hello Identity Protection 儀表板上設定這些功能之後。

* Azure AD [Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)
* Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)。
* Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md)。 

## <a name="user-compromise-risk"></a>使用者入侵風險
**tootest 使用者危害的風險，執行下列步驟的 hello**:

1. 登入太[https://portal.azure.com](https://portal.azure.com)與您的租用戶的全域管理員認證。
2. 瀏覽過**Identity Protection**。 
3. 在主要 hello **Azure AD Identity Protection**刀鋒視窗中，按一下 **設定**。 
4. 在 hello**入口網站設定**刀鋒視窗底下**安全性規則**，按一下**使用者危害的風險**。 
5. 在 hello**登入風險**刀鋒視窗中，開啟**啟用規則**登出，然後按一下**儲存**設定。
6. 對於指定的使用者帳戶，模擬不熟悉位置或匿名 IP 風險事件。 這會提升該使用者的 hello 使用者風險層級太**媒體**。
7. 等候幾分鐘，然後確認使用者的使用者層級為 [中] 。
8. 移 toohello**入口網站設定**刀鋒視窗。
9. 在 hello**使用者危害的風險**刀鋒視窗底下**規則啟用**，選取**上**。 
10. 選取其中一個 hello 下列選項：
    
    a. 選取 tooblock**媒體**下**區塊登入**。
    
    b. tooenforce 安全的密碼變更時，選取**媒體**下**需要多重要素驗證**。
11. 按一下 [儲存] 。
12. 您現在可以使用具有提高風險等級的使用者進行登入，以測試以風險為基礎的條件式存取。 如果 hello 使用者風險中，根據原則的 hello 組態，您是登入可能遭到封鎖，或被迫 toochange 您的密碼。 
    <br><br>
    ![腳本](./media/active-directory-identityprotection-playbook/201.png "腳本")
    <br>

## <a name="sign-in-risk"></a>登入風險
**tootest 登入的風險，執行下列步驟的 hello:**

1. 登入太[https://portal.azure.com](https://portal.azure.com)與您的租用戶的全域管理員認證。
2. 瀏覽過**Identity Protection**。
3. 在主要 hello **Azure AD Identity Protection**刀鋒視窗中，按一下 **設定**。 
4. 在 hello**入口網站設定**刀鋒視窗下**安全性規則**，按一下**登入風險**。
5. 在 hello * * 登入風險 * * 刀鋒視窗中，選取**上**下**規則啟用**。 
6. 選取其中一個 hello 下列選項：
   
   a. 選取 tooblock**媒體**下**區塊登入**
   
   b. tooenforce 安全的密碼變更時，選取**媒體**下**需要多重要素驗證**。
7. tooblock，選取媒體區塊下的登入。
8. tooenforce 多因素驗證，請選取**媒體**下**需要多重要素驗證**。
9. 按一下 [儲存] 。
10. 您現在可以藉由模擬 hello 不熟悉位置測試風險型條件式存取或匿名 IP 風險存在事件，因為兩者都**媒體**事件的風險。


![腳本](./media/active-directory-identityprotection-playbook/200.png "腳本")


## <a name="see-also"></a>另請參閱
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

