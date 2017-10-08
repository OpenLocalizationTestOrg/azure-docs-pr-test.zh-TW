---
title: "aaaVerify Azure Traffic Manager 設定 |Microsoft 文件"
description: "此文章將協助您驗證流量管理員設定"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>驗證流量管理員設定

tootest Traffic Manager 設定，您需要 toohave 多個用戶端，在不同的位置，您可以從中執行測試。 然後，將下一次在 Traffic Manager 設定檔中的 hello 端點。

* 設定 DNS TTL 值 hello 低，使變更傳播快速 （例如，30 秒為單位）。
* 知道 hello Azure 雲端服務和網站中您所測試的 hello 設定檔的 IP 位址。
* 使用工具，可讓您解析 DNS 名稱 tooan IP 位址，並顯示該位址。

您檢查 toosee hello DNS 名稱解析 tooIP hello 設定檔中的端點位址。 解析 hello 名稱應該與 hello Traffic Manager 設定檔中定義的 hello 流量路由方式一致的方式。 您可以使用類似的 hello 工具**nslookup**或**繼續深入了解**tooresolve DNS 名稱。

hello 以下範例將協助您測試 Traffic Manager 設定檔。

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>使用 Windows 中的 nslookup 和 ipconfig 檢查流量管理員設定檔

1. 以系統管理員的身分開啟命令或 Windows PowerShell 命令提示字元。
2. 型別`ipconfig /flushdns`tooflush hello DNS 解析程式快取。
3. 輸入 `nslookup <your Traffic Manager domain name>`。 例如，下列命令檢查 hello hello 前置詞的網域名稱來 hello *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    典型的結果會顯示下列資訊的 hello:

    + hello DNS 名稱和 IP 位址的 hello DNS 伺服器正在存取 tooresolve 此 Traffic Manager 網域名稱。
    + hello Traffic Manager 網域名稱輸入 hello 命令列上之後"nslookup"後面，而且 hello IP 位址 toowhich hello Traffic Manager 網域解析。 hello 第二個 IP 位址是 hello 重要的一個 toocheck。 其值必須符合其中一個 hello 雲端服務或網站 hello 所測試的 Traffic Manager 設定檔中的公用虛擬 IP (VIP) 位址。

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>Tootest hello 容錯移轉如何流量路由方法

1. 保持所有端點運作。
2. 在單一用戶端，使用 nslookup 或類似的公用程式要求公司網域名稱的 DNS 解析。
3. 請確定該 hello 解析 IP 位址符合 hello 主要端點。
4. 將您的主要端點關機，或移除監視檔案，以便 Traffic Manager 認為服務的 hello 應用程式已關閉的 hello。
5. 等候 hello Traffic Manager 設定檔的 hello DNS--存留時間 (TTL) 再加上兩分鐘。 例如，若您的 DNS TTL 為 300 秒 (5 分鐘)，則您必須等待 7 分鐘。
6. 排清您的 DNS 用戶端快取，使用 nslookup 要求 DNS 解析。 在 Windows 中，您可以清除 DNS 快取與 hello ipconfig /flushdns 命令。
7. 請確定該 hello 解析 IP 位址是否符合您的次要端點。
8. 重複 hello 程序，接著垮每個端點。 請確認該 hello DNS 傳回 hello 清單中的 hello 的 hello 下一個端點的 IP 位址。 當所有端點都皆停止後時，您應該再次取得 hello hello 主要端點 IP 位址。

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>如何 tootest hello 加權流量路由方法

1. 保持所有端點運作。
2. 在單一用戶端，使用 nslookup 或類似的公用程式要求公司網域名稱的 DNS 解析。
3. 請確定該 hello 解析 IP 位址是否符合其中一個端點。
4. 排清 DNS 用戶端快取，然後對每個端點重複步驟 2 和 3。 您應該可看到為每個端點傳回不同的 IP 位址。

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>如何 tootest hello 效能流量路由方法

tooeffectively 測試效能流量路由方式中，您必須有遍佈各地的 hello world 的用戶端。 您可以建立用戶端可以使用的 tootest 不同 Azure 區域中您的服務。 如果您有全球網路，您可以從遠端登入 tooclients 中其他部分的 hello world 方法，並可以從該處執行測試。

或者，您可以找到免費的 Web 型 DNS 查閱和挖掘服務。 這些工具提供 hello 能力 toocheck DNS 名稱解析從 hello 世界各地的不同位置。 例如，搜尋 "DNS lookup" 相關資料。 如 Gomez 或 Keynote 協力廠商服務可以使用的 tooconfirm 您的設定檔會依預期分配流量。

## <a name="next-steps"></a>後續步驟

* [關於流量管理員流量路由方法](traffic-manager-routing-methods.md)
* [流量管理員的效能考量](traffic-manager-performance-considerations.md)
* [疑難排解流量管理員的已降級狀態](traffic-manager-troubleshooting-degraded.md)
