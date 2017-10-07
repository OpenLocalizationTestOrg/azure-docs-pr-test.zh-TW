---
title: "Azure AD Connect：設計概念 |Microsoft Docs"
description: "本主題詳細說明特定的實作設計領域"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect：設計概念
hello 本主題的目的是必須在 Azure AD connect 的 hello 實作設計期間思考 toodescribe 區域。 這個主題是特定領域的深入探討，而在其他主題中也會簡短描述這些概念。

## <a name="sourceanchor"></a>sourceAnchor
hello sourceAnchor 屬性定義為*hello 物件存留期間不可變屬性*。 它會唯一識別物件視為 hello 相同的物件在內部部署和 Azure AD 中。 也稱為 hello 屬性**immutableId**並用 hello 兩個名稱是可互換。

hello word 不可變的是 「 不變更 」，是重要的 toothis 主題。 因為已設定之後，就無法變更這個屬性的值，所以重要 toopick 支援您的案例的設計。

hello 屬性可用於下列案例的 hello:

* 在建置新的同步處理引擎伺服器，或在災害復原案例後進行重建時，這個屬性會連結 Azure AD 中的現有物件與內部部署的物件。
* 如果您移動從僅限雲端的身分識別 tooa 已同步處理身分識別模型，則這個屬性允許的物件太"硬碟的相符項目 」 中的現有物件 Azure AD 與內部部署物件。
* 如果您使用同盟，則此屬性，以及 hello **userPrincipalName**用於 hello toouniquely 識別使用者的宣告。

本主題只討論有關 sourceAnchor 與 toousers。 hello 適用相同的規則 tooall 物件類型，但它只適用於使用者是此問題通常是一項考量。

### <a name="selecting-a-good-sourceanchor-attribute"></a>選取良好的 sourceAnchor 屬性
hello 屬性值必須遵守下列規則的 hello:

* 長度小於 60 個字元
  * 系統會將 a-z、A-Z 或 0-9 以外的字元編碼並計為 3 個字元
* 不包含特殊字元︰&#92; ! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* 必須是全域唯一的
* 必須是字串、整數或二進位
* 不應以使用者的名稱、這些變更為基礎
* 不應區分大小寫，並避免可能會因大小寫而改變的值
* 應該在 hello 物件建立時指派

如果 hello 選取 sourceAnchor 不是字串型別，則會不顯示 Azure AD 連接 Base64Encode hello 屬性值 tooensure 任何特殊字元。 如果您使用比 ADFS 的另一部同盟伺服器，請確定您也可以 Base64Encode hello 屬性的伺服器。

hello sourceAnchor 屬性會區分大小寫。 值為"JohnDoe"不是 hello 與 「 johndoe 」 相同。 但是您不應該擁有兩個只有大小寫有差異的不同物件。

如果您有單一樹系內部部署，您應該使用然後 hello 屬性是**objectGUID**。 這也是您在 Azure AD Connect 中使用快速設定，並也 hello DirSync 使用的屬性時所使用的 hello 屬性。

如果您有多個樹系並不會移動使用者之間樹系和網域，然後**objectGUID**是不錯的屬性 toouse 即使在此情況下。

如果樹系和網域之間移動使用者，然後您必須尋找的屬性，不會變更，或可以移動與 hello 使用者在 hello 移動。 建議的方法是 toointroduce 綜合的屬性。 可保存 GUID 之類項目的屬性也可能適用。 在物件建立時，新的 GUID，建立並上 hello 使用者加上戳記。 自訂同步處理規則中可建立 hello 同步作業引擎伺服器 toocreate 根據 hello 這個值**objectGUID**和 ADDS 中的更新 hello 選取的屬性。 當您移動 hello 物件時，請確定 tooalso 複製 hello 內容，這個值。

另一個解決方案是 toopick 您知道不會變更現有屬性。 常用的屬性包括 **employeeID**。 如果您將包含字母的屬性，請確定沒有任何機率 hello 大小寫 （大寫與小寫） 可以變更 hello 屬性的值。 不正確的屬性，不應包含 hello hello 使用者名稱與這些屬性。 在婚姻或離婚，hello 名稱會是預期的 toochange，這不允許這個屬性。 這是另一個原因為何等屬性**userPrincipalName**，**郵件**，和**targetAddress**不 hello Azure AD Connect 的安裝中甚至可能 tooselect精靈。 這些屬性也包含 hello"@"字元，這不允許在 hello sourceAnchor。

### <a name="changing-hello-sourceanchor-attribute"></a>Hello sourceAnchor 屬性變更
在 Azure AD 中已建立 hello 物件並 hello 身分識別同步處理之後，就無法變更 hello sourceAnchor 屬性值。

基於這個理由，hello 下列限制適用於 tooAzure AD 連線：

* hello sourceAnchor 屬性只能在初始安裝期間設定。 如果您重新執行 hello 安裝精靈，此選項會處於唯讀狀態。 如果您需要 toochange 這項設定，則您必須解除安裝並重新安裝。
* 如果您安裝其他 Azure AD Connect 的伺服器，則選取必須 hello 如先前使用相同的 sourceAnchor 屬性。 如果您先前已在使用 DirSync，移動 tooAzure AD 連線，則您必須使用**objectGUID**因為這是使用 DirSync hello 屬性。
* 如果 hello sourceAnchor 值變更之後已匯出的 tooAzure AD，然後 Azure AD Connect 同步處理擲回錯誤，且不允許任何其他變更該物件之前 hello 問題已修正並 hello sourceAnchor 回變更 hello hello 物件。來源目錄。

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>使用 msDS-ConsistencyGuid 來作為 sourceAnchor
根據預設，Azure AD Connect (版本 1.1.486.0 和較舊) 使用 objectGUID 做 hello sourceAnchor 屬性。 ObjectGUID 是由系統所產生。 您並無法在建立內部部署 AD 物件時指定它的值。 一節中所述[sourceAnchor](#sourceanchor)，情況下，您需要 toospecify hello sourceAnchor 值。 適用於 tooyou hello 案例時，您必須使用可設定的 AD 屬性 (例如，ConsistencyGuid msDS) 為 hello sourceAnchor 屬性。

Azure AD Connect (1.1.524.0 版本和之後) 現在可協助 hello 使用 Msds-primary-computer ConsistencyGuid 做為 sourceAnchor 屬性。 使用此功能時，Azure AD Connect 會自動設定 hello 同步處理規則：

1. 作為 Msds-primary-computer ConsistencyGuid hello sourceAnchor 屬性使用者物件。 若為其他物件類型，則要使用 ObjectGUID。

2. 任何給定的內部部署 AD 使用者並不填入其 Msds-primary-computer ConsistencyGuid 屬性，Azure AD Connect 寫入其 objectGUID 值後 toohello Msds-primary-computer ConsistencyGuid 屬性在內部部署 Active Directory 中的物件。 填入 hello Msds-primary-computer ConsistencyGuid 屬性之後，Azure AD Connect 然後匯出 hello 物件 tooAzure AD。

>[!NOTE]
> 一次內部部署 AD 物件會匯入至 Azure AD Connect （，，匯入 hello AD 連接器空間投射至 hello Metaverse），您無法再變更 sourceAnchor 值。 toospecify hello sourceAnchor 值的指定內部部署 AD 物件、 設定其 Msds-primary-computer ConsistencyGuid 屬性，才能匯入 Azure AD Connect。

### <a name="permission-required"></a>所需權限
針對這個功能 toowork，與在內部部署 Active Directory 的 hello AD DS 帳戶使用 toosynchronize 必須授與寫入權限 toohello Msds-primary-computer ConsistencyGuid 屬性在內部部署 Active Directory 中。

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>如何 tooenable hello ConsistencyGuid 功能-新的安裝
您可以在全新安裝期間啟用 hello 使用 ConsistencyGuid 做為 sourceAnchor。 本節詳述快速和自訂安裝。

  >[!NOTE]
  > 僅有較新版本的 Azure AD Connect (1.1.524.0 及之後) 支援 hello 全新安裝期間使用 ConsistencyGuid 做 sourceAnchor。

### <a name="how-tooenable-hello-consistencyguid-feature"></a>如何 tooenable hello ConsistencyGuid 功能
目前，可以只啟用 hello 功能，在安裝新的 Azure AD Connect，僅期間。

#### <a name="express-installation"></a>快速安裝
使用快速模式中安裝 Azure AD Connect 時, hello Azure AD Connect 精靈會自動決定 hello 最適當的 AD 屬性 toouse 做 hello sourceAnchor 屬性使用下列邏輯 hello:

* 首先，做為您的 Azure AD 租用戶 tooretrieve hello AD 屬性 hello Azure AD Connect 精靈查詢 hello sourceAnchor 屬性 hello 先前的 Azure AD Connect 的安裝中，（如果有的話）。 這項資訊是否可用，Azure AD Connect 會使用 hello 相同 AD 屬性。

  >[!NOTE]
  > 僅有較新版本的 Azure AD Connect (1.1.524.0 及之後) 安裝期間使用 Azure AD 租用戶中的儲存資訊，關於 hello sourceAnchor 屬性。 較舊版本的 Azure AD Connect 則不會這麼做。

* 如果使用 hello sourceAnchor 屬性的相關資訊無法使用，hello 精靈會檢查 hello Msds-primary-computer ConsistencyGuid 屬性在內部部署 Active Directory 中的 hello 狀態。 Hello 屬性未設定 hello 目錄中的任何物件上，如果 hello 精靈會使用 hello Msds-primary-computer ConsistencyGuid 作為 hello sourceAnchor 屬性。 如果在 hello 目錄的一或多個物件上設定 hello 屬性，hello 精靈結束時 hello 屬性正由其他應用程式，因此不適合做為 sourceAnchor 屬性...

* 在此情況下，hello 精靈就會回到 toousing objectGUID 做 hello sourceAnchor 屬性。

* 一旦決定 hello sourceAnchor 屬性是，hello 精靈 hello 將資訊儲存在 Azure AD 租用戶。 hello 資訊供未來的 Azure AD Connect 的安裝。

快速安裝完成之後，「 hello 精靈 」 會通知您哪一個屬性具有已挑選為 hello 來源錨點屬性。

![精靈的通知指出它已挑選 AD 屬性來作為 sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>自訂安裝
使用自訂 模式中安裝 Azure AD Connect 時, hello Azure AD Connect 精靈設定 sourceAnchor 屬性時，就會提供兩個選項：

![自訂安裝 - sourceAnchor 設定](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| 設定 | 說明 |
| --- | --- |
| 可讓 Azure 能管理我的 hello 來源錨點 | 如果您要為您的 Azure AD toopick hello 屬性，請選取此選項。 如果您選取此選項時，Azure AD Connect 精靈會套用 hello 相同[sourceAnchor 屬性選取邏輯 Express 安裝期間使用](#express-installation)。 類似的 tooExpress 安裝 hello 精靈會通知您哪一個屬性具有已挑選為 hello 來源錨點屬性自訂安裝完成之後。 |
| 特定的屬性 | 如果您想 toospecify hello sourceAnchor 屬性的現有 AD 屬性，請選取此選項。 |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>如何 tooenable hello ConsistencyGuid 功能-現有的部署
如果您有現有的 Azure AD Connect 部署使用 objectGUID 做 hello 來源錨點屬性，您可以切換它 toousing ConsistencyGuid 改為。

>[!NOTE]
> 僅有較新版本的 Azure AD Connect (1.1.552.0 及之後) 支援從 ObjectGuid tooConsistencyGuid 做 hello 來源錨點屬性切換。

tooswitch 從 objectGUID tooConsistencyGuid 做 hello 來源錨點屬性：

1. 啟動 hello Azure AD Connect 精靈，然後按一下**設定**toogo toohello 工作 畫面。

2. 選取 hello**設定來源錨點**工作選項，並按一下**下一步**。

   ![啟用現有部署的 ConsistencyGuid - 步驟 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. 輸入 Azure AD 系統管理員認證，然後按一下 [下一步]。

4. Azure AD Connect 精靈會分析您在內部部署 Active Directory 中的 hello Msds-primary-computer ConsistencyGuid 屬性 hello 狀態。 如果 hello 屬性未設定任何物件在目錄中，Azure AD Connect 結束時，沒有其他應用程式目前正在使用 hello 屬性，並為安全 toouse hello 它為 hello 來源錨點屬性。 按一下**下一步**toocontinue。

   ![啟用現有部署的 ConsistencyGuid - 步驟 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. 在 hello**準備 tooConfigure**畫面上，按一下**設定**toomake hello 組態變更。

   ![啟用現有部署的 ConsistencyGuid - 步驟 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Hello 組態完成之後，hello 精靈會指示該 Msds-primary-computer ConsistencyGuid 現在當作 hello 來源錨點屬性。

   ![啟用現有部署的 ConsistencyGuid - 步驟 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Hello 在分析期間 （步驟 4），如果 hello 目錄中的一個或多個物件上設定 hello 屬性 hello 精靈結束時，hello 屬性已由另一個應用程式，並傳回錯誤 hello 如下圖所示。 如果您確定該 hello 屬性不會使用現有的應用程式，您需要 toocontact 支援 toosuppress 如何 hello 錯誤的詳細資訊。

![啟用現有部署的 ConsistencyGuid - 錯誤](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>對 AD FS 或第三方同盟設定的影響
如果您使用 Azure AD Connect toomanage 內部部署 AD FS 部署、 hello Azure AD Connect 會自動更新 hello 宣告規則 toouse hello 相同 AD 屬性做為 sourceAnchor。 這可確保產生的 ADFS 該 hello ImmutableID 宣告與 hello sourceAnchor 值匯出 tooAzure AD 一致。

如果您要管理 Azure AD Connect 之外的 AD FS，或使用協力廠商同盟伺服器進行驗證，您必須手動更新 hello 宣告規則 ImmutableID 宣告 toobe 一致 hello sourceAnchor 值匯出為 tooAzure AD發行項 > 一節中所述[修改 AD FS 宣告規則](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims)。 hello 精靈就會返回 hello 安裝完成之後，下列警告：

![第三方同盟設定](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>加入新的目錄 tooexisting 部署
假設您已部署 Azure AD Connect 與 hello ConsistencyGuid 功能啟用，而且現在您想要 tooadd 另一個目錄 toohello 部署。 當您嘗試 tooadd hello 目錄時，Azure AD Connect 精靈會檢查 hello hello 目錄中的 hello Msds-primary-computer ConsistencyGuid 屬性狀態。 如果在 hello 目錄的一或多個物件上設定 hello 屬性，hello 精靈結束時 hello 屬性已由其他應用程式，並傳回錯誤 hello 如下圖所示。 如果您確定該 hello 屬性不會使用現有的應用程式，您需要 toocontact 支援 toosuppress 如何 hello 錯誤的詳細資訊。

![加入新的目錄 tooexisting 部署](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Azure AD 登入
同時使用 Azure AD 整合您的內部部署目錄，它是重要的 toounderstand hello 同步處理設定如何影響 hello 方式使用者驗證。 Azure AD 使用 userPrincipalName (UPN) tooauthenticate hello 使用者。 不過，當您同步處理您的使用者，您必須選擇 hello 屬性 toobe 謹慎使用的 userPrincipalName 值。

### <a name="choosing-hello-attribute-for-userprincipalname"></a>選擇 hello userPrincipalName 屬性
當您選取 hello 屬性提供用於 Azure 的一個 UPN toobe hello 值應該確定

* hello 屬性值符合 toohello UPN 的語法 (RFC 822)，它應該是 hello 格式username@domain
* 中的 hello hello 值符合 tooone hello 後置字元在 Azure AD 中驗證自訂網域

快速設定，在 hello 會假設是 userPrincipalName hello 屬性的選擇。 Hello userPrincipalName 屬性未包含 hello 值，如果您想 tooAzure，在您的使用者 toosign，則您必須選擇**自訂安裝**。

### <a name="custom-domain-state-and-upn"></a>自訂網域狀態和 UPN
它是重要 tooensure 是 hello UPN 尾碼的已驗證的網域。

John 是 contoso.com 中的使用者。您想要 John toouse hello 內部部署 UPN john@contoso.com toosign tooAzure 之後在已同步處理使用者 tooyour Azure AD 目錄 contoso.onmicrosoft.com。 toodo 因此，您需要 tooadd，並確認 contoso.com 做為自訂網域，在 Azure AD，您可以在開始之前同步處理 hello 使用者。 如果 John，例如 contoso.com hello UPN 尾碼不符合在 Azure AD 中的已驗證的網域，然後 Azure AD 來取代 hello UPN 尾碼 contoso.onmicrosoft.com。

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>無法路由傳送的內部部署網域與 Azure AD 的 UPN
有些組織有無法路由傳送的網域，例如 contoso.local 或簡單單一標籤網域，例如 contoso。 您不能 tooverify 路由的內部網域在 Azure AD 中。 Azure AD Connect 可以在 Azure AD 同步 tooonly 已驗證的網域。 當您建立 Azure AD 目錄時，它會建立可路由傳送的網域，而該網域會成為 Azure AD 的預設網域，例如 contoso.onmicrosoft.com。因此，它會變成必要 tooverify 其他任何可路由網域，在此案例中如果您不想 toosync toohello 預設 onmicrosoft.com 網域。

讀取[加入您的自訂網域名稱 tooAzure Active Directory](../active-directory-add-domain.md)如需加入及驗證網域的詳細資訊。

Azure AD Connect 會偵測您是否在無法路由傳送的網域環境中執行，並且會適當地警告您不要繼續進行快速設定。 如果您要在路由的內部網域中，操作可能是該 hello hello 使用者 UPN，然後也有非路由傳送的尾碼。 例如，如果您正在執行 contoso.local，Azure AD Connect 會建議您 toouse 自訂設定，而不是使用 express 設定。 使用自訂設定，就應該做為 UPN toosign tooAzure 中同步處理的 tooAzure AD hello 使用者之後可以 toospecify hello 屬性。

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
