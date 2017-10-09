---
title: "aaaWindows 驗證和 Azure MFA Server |Microsoft 文件"
description: "這是可協助您部署的 Windows 驗證和 Azure Multi-factor Authentication Server 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Windows 驗證與 Azure Multi-Factor Authentication Server
使用 hello Azure Multi-factor Authentication Server tooenable hello Windows 驗證 區段並設定應用程式的 Windows 驗證。 設定 Windows 驗證之前，請記住清單後面的 hello:

* 在安裝之後，重新啟動終端機服務 tootake 效果 hello Azure 多重要素驗證。
* 如果已核取 [需要 Azure Multi-factor Authentication 使用者比對]，而您並不在 hello 使用者清單中，您之後將無法能 toolog hello 機器重新開機。
* 信任的 Ip 是取決於是否 hello 應用程式可以提供 hello 用戶端 IP 與 hello 驗證。 目前僅支援終端機服務。  

> [!NOTE]
> 這項功能不支援的 toosecure 終端機服務，Windows Server 2012 R2 上。

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure 應用程式使用 Windows 驗證時，使用下列程序的 hello。
1. 在 [hello Azure Multi-factor Authentication Server hello Windows 驗證] 圖示。
   ![Windows 驗證](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. 檢查 hello**啟用 Windows 驗證**核取方塊。 預設不核取此方塊。
3. hello 應用程式索引標籤可讓 hello 管理員 tooconfigure Windows 驗證的一或多個應用程式。
4. 選取伺服器或應用程式 – 指定是否啟用 hello 伺服器/應用程式。 按一下 [確定] 。
5. 按一下 [新增...]
6. hello 信任 Ip 索引標籤可讓您源自於特定 Ip 的 tooskip Azure 多重要素驗證的 Windows 工作階段。 例如，如果員工會從 hello 辦公室和家裡使用 hello 應用程式，您可能決定不想其電話響起進行 Azure Multi-factor Authentication 而 hello office。 因此，您可以指定 hello 辦公室子網路作為信任 Ip 項目。
7. 按一下 [新增...]
8. 選取**單一 IP**如果您想要 tooskip 單一 IP 位址。
9. 選取**IP 範圍**如果您想要 tooskip 整個 IP 範圍。 範例：10.63.193.1-10.63.193.100。
10. 選取**子網路**如果您想要 toospecify Ip 範圍使用子網路標記法。 輸入 hello 子網路的起始 IP 和挑選適當的網路遮罩 hello hello 下拉式清單中。
11. 按一下 [確定] 。

## <a name="next-steps"></a>後續步驟

- [設定 Azure MFA Server 的協力廠商 VPN 應用裝置](multi-factor-authentication-advanced-vpn-configurations.md)

- [Azure MFA 的強化現有的驗證基礎結構以 hello NPS 擴充功能](multi-factor-authentication-nps-extension.md)
