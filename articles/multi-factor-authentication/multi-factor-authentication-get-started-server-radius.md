---
title: "驗證和 Azure MFA Server aaaRADIUS |Microsoft 文件"
description: "這是可協助您部署 RADIUS 驗證與 Azure Multi-factor Authentication Server 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>將 RADIUS 驗證與 Azure Multi-Factor Authentication Server 整合
使用 Azure MFA Server tooenable hello RADIUS 驗證 區段並設定 RADIUS 驗證。 RADIUS 是標準通訊協定 tooaccept 驗證要求和 tooprocess 這些要求。 hello Azure Multi-factor Authentication Server 做為 RADIUS 伺服器。 請將它插入您的 RADIUS 用戶端 （VPN 應用裝置） 和您可能是 Active Directory (AD)、 LDAP 目錄或其他 RADIUS 伺服器 tooadd Azure Multi-factor Authentication 的驗證目標之間。 針對 Azure Multi-factor Authentication (MFA) toofunction 中，您必須設定 Azure MFA Server hello，讓它可以與 hello 用戶端伺服器和 hello 驗證目標通訊。 hello Azure MFA Server 會接受來自 RADIUS 用戶端要求、 針對 hello 驗證目標驗證認證、 加入 Azure Multi-factor Authentication，和傳送回應後 toohello RADIUS 用戶端。 只有 hello 主要驗證和 hello Azure 多重要素驗證成功，才會成功 hello 驗證要求。

> [!NOTE]
> hello MFA Server 只支援 PAP （密碼驗證通訊協定） 和 MSCHAPv2 （Microsoft Challenge Handshake 驗證通訊協定） 做為 RADIUS 伺服器時，RADIUS 通訊協定。  時 hello MFA server 做為支援該通訊協定的 RADIUS proxy tooanother RADIUS 伺服器，可以使用其他通訊協定，例如 EAP （可延伸驗證通訊協定）。
>
> 在此組態中，單向傳送 SMS 和 OATH 權杖不運作，因為 hello MFA Server 無法起始成功的 RADIUS 挑戰回應，使用替代的通訊協定。

![Radius 驗證](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>新增 RADIUS 用戶端
Windows server 上安裝 hello Azure Multi-factor Authentication Server tooconfigure RADIUS 驗證。 如果您有 Active Directory 環境，hello 伺服器應該加入的 toohello hello 網路內的網域。 使用下列程序 tooconfigure hello Azure Multi-factor Authentication Server 的 hello:

1. 在 hello Azure Multi-factor Authentication Server，按一下左窗格中 hello hello [RADIUS 驗證] 圖示。
2. 檢查 hello**啟用 RADIUS 驗證**核取方塊。
3. Hello 用戶端 索引標籤上變更 hello 驗證和帳戶處理連接埠如果 hello Azure MFA RADIUS 服務需要 toolisten 的非標準連接埠上的 RADIUS 要求。
4. 按一下 [新增] 。
5. 輸入 hello hello 應用裝置/伺服器將向 Azure Multi-factor Authentication Server toohello、 應用程式名稱 （選擇性） 和共用的密碼的 IP 位址。

  hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。

  hello 的共用密碼需要 toobe hello 相同的兩個 hello Azure Multi-factor Authentication Server 和應用裝置/伺服器。

6. 檢查 hello**需要進行 Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入 hello 伺服器與主體 toomulti 雙因素驗證。 如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於兩步驟驗證，請不要 hello 方塊中選取。
7. 檢查 hello**啟用後援 OATH 權杖**方塊，如果您要從行動裝置驗證應用程式的 toouse OATH 密碼做為後援 toohello 的頻外通話、 簡訊，或推播通知。
8. 按一下 [確定] 。

許多其他 RADIUS 用戶端視需要重複步驟 4 到 8 tooadd。

## <a name="configure-your-radius-client"></a>設定 RADIUS 用戶端

1. 按一下 hello**目標** 索引標籤。
2. 如果 hello Azure MFA Server 安裝在 Active Directory 環境中已加入網域的伺服器上，選取 Windows 網域。
3. 如果應該向 LDAP 目錄驗證使用者，請選取 [LDAP 繫結]。

  toouse LDAP 繫結，按一下 hello 目錄整合 圖示，然後編輯 hello hello 設定 索引標籤上的 LDAP 組態，使 hello 伺服器可以將繫結 tooyour 目錄。 可以找到設定 LDAP 的指示，在 hello [LDAP Proxy 組態指南](multi-factor-authentication-get-started-server-ldap.md)。

4. 如果應該向另一部 RADIUS 伺服器驗證使用者，選取 [RADIUS 伺服器]。
5. 按一下**新增**tooconfigure hello 伺服器 toowhich hello Azure MFA Server 將 proxy hello RADIUS 要求。
6. 在 hello [新增 RADIUS 伺服器] 對話方塊中，輸入 hello IP 位址的 hello RADIUS 伺服器和共用的密碼。

  hello 的共用密碼需要 toobe hello 相同的兩個 hello Azure Multi-factor Authentication Server 和 RADIUS 伺服器。 如果 hello RADIUS 伺服器會使用不同的通訊埠，請變更 hello 驗證連接埠和帳戶處理連接埠。

7. 按一下 [確定] 。
8. 新增 Azure MFA Server 的 RADIUS 用戶端中 hello hello 其他 RADIUS 伺服器，使它可以處理 tooit 寄 hello Azure MFA Server 的存取要求。 使用共用 hello Azure Multi-factor Authentication Server 中設定密碼相同的 hello。

重複這些步驟 tooadd 更多的 RADIUS 伺服器，並設定 hello 順序中的 hello Azure MFA Server 呼叫它們以 hello**移**和**下移**按鈕。

如此即完成 hello Azure Multi-factor Authentication Server 設定。 hello 伺服器的 RADIUS 存取要求來自 hello 設定用戶端正在 hello 設定連接埠上接聽。   

## <a name="radius-client-configuration"></a>RADIUS 用戶端組態
tooconfigure hello RADIUS 用戶端，使用 hello 指導方針：

* 設定您的應用裝置/伺服器 tooauthenticate 透過 RADIUS toohello Azure Multi-factor Authentication Server 的 IP 位址，就會成為 hello RADIUS 伺服器。
* 使用先前設定的密碼共用相同的 hello。
* 設定 hello RADIUS 逾時 too30 60 秒，以便有時間 toovalidate hello 使用者的認證、 執行雙步驟驗證、 接收其回應，以及然後回應 toohello RADIUS 存取要求。
