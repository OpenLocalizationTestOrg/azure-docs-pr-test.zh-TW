---
title: "aaaRDG 和使用 RADIUS 的 Azure MFA Server |Microsoft 文件"
description: "這是可協助您部署遠端桌面閘道與 Azure Multi-factor Authentication Server 驗證使用 RADIUS 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server
通常，遠端桌面閘道會使用本機網路原則的服務 」 (NPS) tooauthenticate 使用者 hello。 本文說明如何 tooroute RADIUS 要求出從 hello 遠端桌面閘道 (透過 hello 本機 NPS) toohello Multi-factor Authentication Server。 hello Azure MFA 和 RD 閘道的組合表示您的使用者可以從任何地方存取其工作環境執行強式驗證時。 

由於終端機服務的 Windows 驗證不支援 Server 2012 r2 中，使用 MFA Server RD 閘道和 RADIUS toointegrate。 

Hello Azure Multi-factor Authentication Server 伺服器上安裝不同，hello RADIUS 要求哪些 proxy hello 遠端桌面閘道伺服器上備份 toohello NPS。 NPS 驗證 hello 使用者名稱和密碼之後，它會傳回回應 toohello Multi-factor Authentication Server。 然後，MFA Server hello 執行 hello 第二個驗證因素，並傳回結果 toohello 閘道。

## <a name="prerequisites"></a>必要條件

- 已加入網域的 Azure MFA Server。 如果沒有任何已安裝，請依照下列中的 hello 步驟[hello Azure Multi-factor Authentication Server 使用者入門](multi-factor-authentication-get-started-server.md)。
- 使用網路原則服務進行驗證的遠端桌面閘道。

## <a name="configure-hello-remote-desktop-gateway"></a>設定遠端桌面閘道 hello
設定 hello RD 閘道 toosend RADIUS 驗證 tooan Azure Multi-factor Authentication Server。 

1. 在 RD 閘道管理員中，以滑鼠右鍵按一下 hello 伺服器名稱，然後選取**屬性**。
2. 移 toohello **RD CAP 存放區**索引標籤並選取**執行 NPS 的中央伺服器**。 
3. 輸入 hello 名稱或 IP 位址的每一部伺服器，一或多個 Azure Multi-factor Authentication Server 新增為 RADIUS 伺服器。 
4. 為每一部伺服器建立共用密碼。

## <a name="configure-nps"></a>設定 NPS
hello RD 閘道使用 NPS toosend hello RADIUS 要求 tooAzure Multi-factor Authentication。 tooconfigure NPS，首先您變更 hello hello 雙步驟驗證完成之前，tooprevent hello RD 閘道在逾時的逾時設定。 接著，您會從您的 MFA 伺服器更新 NPS tooreceive RADIUS 驗證。 使用下列程序 tooconfigure NPS hello:

### <a name="modify-hello-timeout-policy"></a>修改 hello 逾時原則

1. 在 NPS 中，開啟 hello **RADIUS 用戶端和伺服器**hello 剩餘資料行，然後選取功能表**遠端 RADIUS 伺服器群組**。 
2. 選取 hello **TS GATEWAY SERVER GROUP**。 
3. 移 toohello**負載平衡** 索引標籤。 
4. 變更這兩個 hello**卸除的要求都視為前，無回應的秒數**和 hello**伺服器被識別為無法使用時，在要求之間的秒數**toobetween 30 到 60秒數。 （如果您發現該 hello 伺服器仍然會逾時在驗證期間，您可以再回到這裡並增加 hello 秒數。）
5. 移 toohello**驗證/帳戶**索引標籤上，檢查指定相符項目 hello 連接埠接聽 Multi-factor Authentication Server 的 hello hello RADIUS 連接埠。

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>準備從 hello MFA Server NPS tooreceive 驗證

1. 以滑鼠右鍵按一下**RADIUS 用戶端**RADIUS 用戶端和伺服器 hello 剩餘資料行，然後選取底下**新增**。
2. 新增 hello Azure Multi-factor Authentication Server 的 RADIUS 用戶端。 選擇 [好記的名稱] 並指定共用密碼。
3. 開啟 hello**原則**hello 剩餘資料行，然後選取功能表**連線要求原則**。 您應會看見在設定 RD 閘道時所建立的原則，其名稱為 [TS 閘道授權原則]。 此原則轉送 RADIUS 要求 toohello Multi-factor Authentication Server。
4. 以滑鼠右鍵按一下 [TS 閘道授權原則]，然後選取 [重複原則]。 
5. 開啟 hello 新原則，然後移至 toohello**條件** 索引標籤。
6. 加入條件符合 hello hello hello Azure Multi-factor Authentication Server RADIUS 用戶端的步驟 2 中設定的易記名稱的用戶端易記名稱。 
7. 移 toohello**設定**索引標籤並選取**驗證**。
8. 變更 hello 驗證提供者太**驗證此伺服器上的要求**。 此原則可確保當 NPS 收到 RADIUS 要求從 hello Azure MFA Server 時，在本機而不是傳送 RADIUS 要求後 toohello Azure Multi-factor Authentication Server，可能會導致迴圈狀況發生 hello 驗證。 
9. tooprevent 迴圈條件，請確定 hello 新原則會排序在 hello hello 原始原則之上**連線要求原則**窗格。

## <a name="configure-azure-multi-factor-authentication"></a>設定 Azure Multi-Factor Authentication

hello Azure Multi-factor Authentication Server 會設定為 RD 閘道和 NPS 之間的 RADIUS proxy。  它應該與 hello RD 閘道伺服器位於不同網域的伺服器上安裝。 使用下列程序 tooconfigure hello Azure Multi-factor Authentication Server 的 hello。

1. 開啟 hello Azure Multi-factor Authentication Server，然後選取 hello RADIUS 驗證 圖示。 
2. 檢查 hello**啟用 RADIUS 驗證**核取方塊。
3. Hello 用戶端] 索引標籤，確定 hello 連接埠符合 NPS 中的設定，然後選取 [**新增**。
4. 加入 hello RD 閘道伺服器 IP 位址、 應用程式名稱 （選用） 和共用的密碼。 hello 共用密碼需要 toobe hello 相同 hello Azure Multi-factor Authentication Server 和 RD 閘道上。
3. 移 toohello**目標** 索引標籤並選取 hello **RADIUS 伺服器**選項按鈕。
4. 選取**新增**，然後輸入 hello IP 位址、 共用的密碼和 hello NPS 伺服器的連接埠。 除非使用中央 NPS，否則 hello RADIUS 用戶端和 RADIUS 目標是 hello 相同。 hello 共用的密碼必須符合 hello hello hello NPS 伺服器的 RADIUS 用戶端區段中的一個安裝程式。

![Radius 驗證](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>後續步驟

- 整合 Azure MFA 與 [IIS Web Apps](multi-factor-authentication-get-started-server-iis.md)

- 在 hello 解答[Azure Multi-factor Authentication 常見問題集](multi-factor-authentication-faq.md)
