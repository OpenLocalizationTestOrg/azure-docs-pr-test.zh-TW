---
title: "aaaAdd 憑證 toohello Java CA 存放區 |Microsoft 文件"
description: "了解如何 tooadd 憑證授權單位 (CA) 憑證 toohello Java CA (cacerts) 之憑證存放區 Twilio 服務或 Azure 服務匯流排。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>新增憑證 toohello Java CA 的憑證存放區
hello 下列步驟顯示如何 tooadd 憑證授權單位 (CA) 憑證 toohello Java CA 憑證 (cacerts) 儲存。 使用 hello 範例 hello CA 憑證必須使用 hello Twilio 服務。 Hello 主題稍後提供的資訊說明 tooinstall hello CA hello Azure 服務匯流排的憑證。 

您可以使用 keytool tooadd hello CA 憑證先前 toozipping JDK，並將它加入 tooyour Azure 專案的**approot**資料夾，或者您可以執行使用 keytool tooadd hello 憑證 Azure 的啟動工作。 這個範例假設您將新增 CA 憑證先前 toohello 被壓縮的 JDK。 此外，特定的 CA 憑證將用於 hello 範例中，但取得不同的 CA 憑證的 hello 步驟中，並匯入至 hello cacerts 存放區會如下所示。

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>tooadd 憑證 toohello cacerts 儲存
1. 在命令提示字元設定 tooyour JDK **jdk\jre\lib\security**資料夾中，執行下列已安裝哪些憑證 toosee hello:
   
    `keytool -list -keystore cacerts`
   
    將會提示您輸入 hello 存放的密碼。 hello 預設密碼為**變更**。 (如果您想 toochange hello 密碼，請參閱 hello keytool 文件，網址<http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>。)這個範例假設 MD5 指紋 67:CB:9 D 與該 hello 憑證： C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 未列出，而且您想 tooimport it （此特定的憑證所 hello Twilio API 服務）。
2. 從憑證列在 hello 清單取得 hello 憑證[GeoTrust 根憑證](http://www.geotrust.com/resources/root-certificates/)。 Hello 憑證序號 35:DE:F4:CF hello 連結上按一下滑鼠右鍵，並將它儲存 toohello **jdk\jre\lib\security**資料夾。 基於此範例中，儲存名為 tooa 檔案**Equifax\_Secure\_憑證\_Authority.cer**。
3. 匯入 hello 憑證，透過 hello 下列命令：
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    當系統提示您 tootrust 此憑證，如果 hello 憑證 MD5 指紋 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4，回應輸入**y**。
4. 執行下列命令 tooensure hello CA 憑證的 hello 已成功匯入：
   
    `keytool -list -keystore cacerts`
5. 壓縮 hello JDK，並將它加入 tooyour Azure 專案的**approot**資料夾。

如需 keytool 的詳細資訊，請參閱 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>。

## <a name="azure-root-certificates"></a>Azure 根憑證
您使用 Azure 服務 （例如 Azure Service Bus) 的應用程式需要 tootrust hello Baltimore CyberTrust 根憑證。 （從 2013 年 4 月 15 日，Azure 已開始從 hello GTE CyberTrust 全域根 toohello Baltimore CyberTrust 根移轉。 這項移轉採取幾個月 toocomplete。）

hello Baltimore 憑證可能已經安裝在您 cacerts 存放區中，因此請記住 toorun hello **keytool-清單**命令 toosee 第一次，如果已經存在。

如果您需要 tooadd hello Baltimore CyberTrust 根，它有序號 02:00:00:b9 和 SHA1 指紋 d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c: 78:db:28:52:ca:e4:74。 您可以從下載<https://cacert.omniroot.com/bc2025.crt>，儲存 tooa 本機檔案具有副檔名**.cer**，然後再匯入使用**keytool**如上所示。

## <a name="next-steps"></a>後續步驟
如需使用 Azure 的 hello 的根憑證的詳細資訊，請參閱[Azure 根憑證移轉](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx)。

如需 Java 的詳細資訊，請參閱[適用於 Java 開發人員的 Azure](/java/azure)。

