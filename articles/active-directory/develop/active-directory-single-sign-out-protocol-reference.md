---
title: "aaaAzure 單一簽出 SAML 通訊協定 |Microsoft 文件"
description: "本文說明 hello Azure Active Directory 中的單一登出 SAML 通訊協定"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 單一登出 SAML 通訊協定
Azure Active Directory (Azure AD) 支援 hello SAML 2.0 web 瀏覽器單一登出設定檔。 單一登出 toowork 正確，hello **LogoutURL** hello 應用程式必須明確地註冊應用程式註冊期間使用 Azure AD。 在登出後，azure AD 使用 hello LogoutURL tooredirect 使用者。

這個圖表可顯示 hello hello Azure AD 單一登出程序工作流程。

![單一登出工作流程](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
雲端服務傳送的 hello`LogoutRequest`訊息 tooAzure AD tooindicate 工作階段已終止。 hello 下列摘錄顯示範例`LogoutRequest`項目。

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
hello`LogoutRequest`傳送的項目 tooAzure AD 需要 hello 下列屬性：

* `ID`： 這會識別 hello 登出要求。 hello 值`ID`不應以數字開頭。 hello 一般作法是 tooappend**識別碼**toohello GUID 字串表示法。
* `Version`: Hello 將值設定這個項目太**2.0**。 需要此值。
* `IssueInstant`：這是具有國際標準時間 (UTC) 值和[來回行程格式 ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx) 的 `DateTime` 字串。 Azure AD 會預期此類型的值，但不會強制。

### 簽發者
hello`Issuer`中的項目`LogoutRequest`必須完全符合其中一個 hello **ServicePrincipalNames** hello Azure AD 中的雲端服務中。 一般而言，這會設定 toohello**應用程式識別碼 URI**應用程式登錄期間指定。

### NameID
hello 值 hello`NameID`項目必須完全符合 hello`NameID`的 hello 正在登出的使用者。

## LogoutResponse
Azure AD 傳送`LogoutResponse`中回應 tooa`LogoutRequest`項目。 hello 下列摘錄顯示範例`LogoutResponse`。

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Azure AD 設定 hello `ID`，`Version`和`IssueInstant`中 hello 值`LogoutResponse`項目。 它也會設定 hello `InResponseTo` hello 項目 toohello 值`ID`屬性 hello`LogoutRequest`為引發回應 hello。

### 簽發者
Azure AD 會將此值太`https://login.microsoftonline.com/<TenantIdGUID>/`其中<TenantIdGUID>是 hello hello Azure AD 租用戶的租用戶識別碼。

hello tooevaluate hello 值`Issuer`項目，使用 hello 值 hello**應用程式識別碼 URI**在應用程式登錄期間提供。

### 狀態
Azure AD 使用 hello `StatusCode` hello 中的項目`Status`元素 tooindicate hello 成功或失敗的登出。當 hello 登出嘗試失敗時，hello`StatusCode`項目也可包含自訂錯誤訊息。
