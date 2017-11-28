---
title: "單一登入 SAML 通訊協定 aaaAzure |Microsoft 文件"
description: "本文章說明 Azure Active Directory 中的 hello 單一登入 SAML 通訊協定"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 單一登入 SAML 通訊協定
本文涵蓋 hello SAML 2.0 驗證要求和回應，Azure Active Directory (Azure AD) 支援的單一登入。

圖的 hello 通訊協定描述 hello 單一登入順序。 hello 雲端服務 （hello 服務提供者） 會使用 HTTP 重新導向繫結 toopass `AuthnRequest` （驗證要求） 元素 tooAzure AD （hello 身分識別提供者）。 然後 azure AD 會使用 HTTP post 繫結 toopost`Response`元素 toohello 雲端服務。

![單一登入工作流程](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
toorequest 使用者驗證，雲端服務傳送`AuthnRequest`元素 tooAzure AD。 範例 SAML 2.0 `AuthnRequest` 看起來可能像這樣︰

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| 參數 |  | 說明 |
| --- | --- | --- |
| ID |必要 |Azure AD 會使用這個屬性 toopopulate hello `InResponseTo` hello 傳回回應的屬性。 識別碼開頭不可以是數字，因此常用的策略是 tooprepend 類似 「 識別碼 」 toohello GUID 字串表示法的字串。 例如， `id6c1c178c166d486687be4aaf5e482730` 便是有效的識別碼。 |
| 版本 |必要 |這應該是 **2.0**。 |
| IssueInstant |必要 |這是具有 UTC 值和 [來回行程格式 ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx)的日期時間字串。 Azure AD 必須要有這種日期時間值，但不會評估或使用 hello 值。 |
| AssertionConsumerServiceUrl |選用 |如果提供，這必須符合 hello `RedirectUri` hello Azure AD 中的雲端服務。 |
| ForceAuthn |選用 | 這是布林值。 如果為 true，這表示該 hello 使用者將會強制的 toore-驗證，即使它們與 Azure AD 的有效工作階段。 |
| IsPassive |選用 |這是布林值，指定是否 Azure AD 會驗證 hello 使用者以無訊息模式，而不需使用者互動，使用 hello 工作階段 cookie，如果有的話。 如果為 true，Azure AD 會嘗試使用 hello 工作階段 cookie tooauthenticate hello 使用者。 |

其他所有 `AuthnRequest` 屬性 (例如 Consent、Destination、AssertionConsumerServiceIndex、AttributeConsumerServiceIndex 和 ProviderName) 會 **遭到忽略**。

Azure AD 也會忽略 hello`Conditions`中的項目`AuthnRequest`。

### 簽發者
hello`Issuer`中的項目`AuthnRequest`必須完全符合其中一個 hello **ServicePrincipalNames** hello Azure AD 中的雲端服務中。 一般而言，這會設定 toohello**應用程式識別碼 URI**應用程式登錄期間指定。

包含 hello 範例 SAML 摘錄`Issuer`項目看起來像這樣：

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
這個項目要求特定名稱 ID 格式 hello 回應，並選擇性在`AuthnRequest`傳送元素 tooAzure AD。

範例 `NameIdPolicy` 元素看起來像這樣︰

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

如果提供 `NameIDPolicy`，您可以包含其選擇性的 `Format` 屬性。 hello`Format`屬性可以有只有其中一個值的 hello; 任何其他值會導致錯誤。

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory 發出 hello NameID 宣告做為成對識別碼。
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory 發出的電子郵件地址格式中的 hello NameID 宣告。
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`： 這個值允許 Azure Active Directory tooselect hello 宣告格式。 Azure Active Directory 發出 hello NameID 做為成對識別碼。
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory 會發出 hello NameID 宣告做為唯一 toohello 目前的 SSO 作業的隨機產生的值。 這表示 hello 值是暫時性的便無法使用的 tooidentify hello 驗證使用者。

Azure AD 會忽略 hello`AllowCreate`屬性。

### RequestAuthnContext
hello`RequestedAuthnContext`項目會指定所需的 hello 驗證方法。 它是選擇性的`AuthnRequest`傳送元素 tooAzure AD。 Azure AD 只支援一個 `AuthnContextClassRef` 值︰`urn:oasis:names:tc:SAML:2.0:ac:classes:Password`。

### 範圍
hello`Scoping`項目，其中包含身分識別提供者的清單，是選擇性的`AuthnRequest`傳送元素 tooAzure AD。

如果提供，不會包含 hello`ProxyCount`屬性`IDPListOption`或`RequesterID`項目，因為它們不支援。

### 簽章
請勿在 `AuthnRequest` 元素中包含 `Signature` 元素，因為 Azure AD 不支援簽署的驗證要求。

### 主旨
Azure AD 會忽略 hello`Subject`元素`AuthnRequest`項目。

## Response
要求的登入成功完成時，Azure AD 會回傳回應 toohello 雲端服務。 範例回應 tooa 成功登入嘗試看起來像這樣：

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Response
hello`Response`元素包含 hello hello 授權要求結果。 Azure AD 設定 hello `ID`，`Version`和`IssueInstant`中 hello 值`Response`項目。 它也會設定下列屬性的 hello:

* `Destination`： 登入成功完成時，這設定 toohello `RedirectUri` hello 服務提供者 （雲端服務）。
* `InResponseTo`： 這個設定 toohello`ID`屬性 hello`AuthnRequest`起始 hello 回應的項目。

### 簽發者
Azure AD 設定 hello`Issuer`項目太`https://login.microsoftonline.com/<TenantIDGUID>/`其中<TenantIDGUID>是 hello hello Azure AD 租用戶的租用戶識別碼。

例如，具有 Issuer 元素的範例回應看起來可能像這樣︰

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### 狀態
hello`Status`元素傳達 hello 成功或失敗的登入。 它包含 hello`StatusCode`元素，其中包含程式碼或一組巢狀的程式碼代表 hello 要求的 hello 狀態。 它也包含 hello`StatusMessage`元素，其中包含 hello 登入程序期間所產生的自訂錯誤訊息。

<!-- TODO: Add a authentication protocol error reference -->

hello 以下是 SAML 回應 tooan 登入嘗試失敗。

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Assertion
在加法 toohello `ID`，`IssueInstant`和`Version`，Azure AD 設定下列項目在 hello hello `Assertion` hello 回應的項目。

#### 簽發者
這設定得`https://sts.windows.net/<TenantIDGUID>/`其中<TenantIDGUID>為 hello hello Azure AD 租用戶的租用戶識別碼。

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### 簽章
Azure AD 簽署 hello 回應 tooa 成功登入中的判斷提示。 hello`Signature`元素包含數位簽章 hello 雲端服務可以使用 tooauthenticate hello 來源 tooverify hello 完整性 hello 判斷提示。

此數位簽章，Azure AD 使用的 toogenerate hello hello 的簽署金鑰`IDPSSODescriptor`及其中繼資料文件項目。

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### 主旨
這會指定 hello hello hello 判斷提示中的 hello 陳述式主體的主體。 它包含`NameID`元素，其代表 hello 已驗證的使用者。 hello`NameID`值是目標的識別碼，是為 hello hello 語彙基元的對象的導向的唯一 toohello 服務提供者。 它是持續性的 - 可撤銷，但絕對不會重新指派。 它也是不透明的也就是說，它才不會顯示 hello 使用者相關的任何項目，並且不能做為識別項為屬性查詢。

hello`Method`屬性 hello`SubjectConfirmation`項目一定會設定太`urn:oasis:names:tc:SAML:2.0:cm:bearer`。

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### 條件
這個項目會指定定義 hello 可接受的條件使用的 SAML 判斷提示。

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

hello`NotBefore`和`NotOnOrAfter`屬性指定 hello 間隔期間的 hello 判斷提示是否正確。

* hello 值 hello`NotBefore`屬性些許是等於 tooor （少於一秒） 晚於 hello 值`IssueInstant`hello 屬性`Assertion`項目。 Azure AD 並不考慮任何本身與時差 hello 雲端服務 （服務提供者），而且不加入任何緩衝 toothis 時間。
* hello 值 hello`NotOnOrAfter`屬性是 hello hello 值晚 70 分鐘`NotBefore`屬性。

#### 對象
這包含可識別適用對象的 URI。 Azure AD 設定此項目 toohello 值 hello 值`Issuer`hello 的項目`AuthnRequest`起始 hello 登入。 tooevaluate hello`Audience`值，請使用 hello hello 值`App ID URI`應用程式登錄期間指定。

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

像 hello`Issuer`值 hello`Audience`值必須完全符合其中一個 hello 服務主體名稱，代表在 Azure AD 中的 hello 雲端服務。 不過，如果 hello 值的 hello`Issuer`項目不是 URI 值，hello `Audience` hello 回應中的值為 hello`Issuer`值前面加上`spn:`。

#### AttributeStatement
這包含 hello 主體或使用者相關宣告。 hello 下列摘錄中包含的範例`AttributeStatement`項目。 hello 省略符號表示該 hello 元素可以包含多個屬性和屬性值。

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **名稱宣告**: hello 的 hello 值`Name`屬性 (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) 是 hello hello 驗證使用者的使用者主體名稱，例如`testuser@managedtenant.com`。
* **ObjectIdentifier 宣告**: hello 的 hello 值`ObjectIdentifier`屬性 (`http://schemas.microsoft.com/identity/claims/objectidentifier`) 為 hello `ObjectId` hello 目錄物件，代表 hello 的 Azure AD 中驗證的使用者。 `ObjectId`是的不可變、 全域唯一的並重複使用的 hello 的安全識別項驗證的使用者。

#### AuthnStatement
這個項目會判斷提示該 hello 判斷提示主體在特定時間以特定方式通過驗證。

* hello`AuthnInstant`屬性會指定 hello hello 使用者使用 Azure AD 驗證的時間。
* hello`AuthnContext`項目會指定使用 tooauthenticate hello 使用者的 hello 驗證內容。

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```