---
title: "aaaSplit 合併安全性設定 |Microsoft 文件"
description: "設定加密的 x409 憑證"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>分割合併安全性設定
toouse hello 分割/合併服務，您必須正確設定安全性。 hello 服務是 Microsoft Azure SQL Database 的 hello 彈性延展功能的一部分。 如需詳細資訊，請參閱 [Elastic Scale 分割及合併服務教學課程](sql-database-elastic-scale-configure-deploy-split-and-merge.md)

## <a name="configuring-certificates"></a>設定憑證
憑證有兩種設定方式。 

1. [tooConfigure hello SSL 憑證](#to-configure-the-ssl-certificate)
2. [tooConfigure 用戶端憑證](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>tooobtain 憑證
可以取得憑證，從公用憑證授權單位 (Ca) 或 hello [Windows 憑證服務](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx)。 這些是慣用的 hello 方法 tooobtain 憑證。

如果這些選項都無法使用，您可以產生 **自我簽署憑證**。

## <a name="tools-toogenerate-certificates"></a>工具 toogenerate 憑證
* [makecert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>toorun hello 工具
* 從 Visual Studio 的開發人員命令提示字元，請參閱 [Visual Studio 命令提示字元](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    如果已安裝，請移至：
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* 取得 hello 從 WDK [Windows 8.1： 下載的套件與工具](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>tooconfigure hello SSL 憑證
SSL 憑證是必要的 tooencrypt hello 通訊，並驗證 hello 伺服器。 選擇 hello 最適用的 hello 三種案例，並執行所有步驟：

### <a name="create-a-new-self-signed-certificate"></a>建立新的自我簽署憑證
1. [建立自我簽署憑證](#create-a-self-signed-certificate)
2. [建立自我簽署 SSL 憑證的 PFX 檔案](#create-pfx-file-for-self-signed-ssl-certificate)
3. [上傳 SSL 憑證 tooCloud 服務](#upload-ssl-certificate-to-cloud-service)
4. [在服務組態檔中更新 SSL 憑證](#update-ssl-certificate-in-service-configuration-file)
5. [匯入 SSL 憑證授權單位](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>toouse hello 憑證從現有的憑證存放區
1. [從憑證存放區匯出 SSL 憑證](#export-ssl-certificate-from-certificate-store)
2. [上傳 SSL 憑證 tooCloud 服務](#upload-ssl-certificate-to-cloud-service)
3. [在服務組態檔中更新 SSL 憑證](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse PFX 檔案中現有的憑證
1. [上傳 SSL 憑證 tooCloud 服務](#upload-ssl-certificate-to-cloud-service)
2. [在服務組態檔中更新 SSL 憑證](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>tooconfigure 用戶端憑證
在訂單 tooauthenticate 要求 toohello 服務會需要用戶端憑證。 選擇 hello 最適用的 hello 三種案例，並執行所有步驟：

### <a name="turn-off-client-certificates"></a>關閉用戶端憑證
1. [關閉用戶端憑證式驗證](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>發行新的自我簽署用戶端憑證
1. [建立自我簽署憑證授權單位](#create-a-self-signed-certification-authority)
2. [上傳的 CA 憑證 tooCloud 服務](#upload-ca-certificate-to-cloud-service)
3. [在服務組態檔中更新 CA 憑證](#update-ca-certificate-in-service-configuration-file)
4. [發行用戶端憑證](#issue-client-certificates)
5. [建立用戶端憑證的 PFX 檔案](#create-pfx-files-for-client-certificates)
6. [匯入用戶端憑證](#Import-Client-Certificate)
7. [複製用戶端憑證指紋](#copy-client-certificate-thumbprints)
8. [在 hello 服務組態檔中設定允許用戶端](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>使用現有的用戶端憑證
1. [Find CA Public Key](#find-ca-public-key)
2. [上傳的 CA 憑證 tooCloud 服務](#Upload-CA-certificate-to-cloud-service)
3. [在服務組態檔中更新 CA 憑證](#Update-CA-Certificate-in-Service-Configuration-File)
4. [複製用戶端憑證指紋](#Copy-Client-Certificate-Thumbprints)
5. [在 hello 服務組態檔中設定允許用戶端](#configure-allowed-clients-in-the-service-configuration-file)
6. [設定用戶端憑證撤銷檢查](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>允許的 IP 位址
存取 toohello 服務端點可以是受限制的 toospecific 的 IP 位址範圍。

## <a name="tooconfigure-encryption-for-hello-store"></a>tooconfigure 加密 hello 存放區
憑證是儲存在 hello 中繼資料存放區的必要的 tooencrypt hello 認證。 選擇 hello 最適用的 hello 三種案例，並執行所有步驟：

### <a name="use-a-new-self-signed-certificate"></a>使用新的自我簽署憑證
1. [建立自我簽署憑證](#create-a-self-signed-certificate)
2. [建立自我簽署加密憑證的 PFX 檔案](#create-pfx-file-for-self-signed-ssl-certificate)
3. [上傳加密憑證 tooCloud 服務](#upload-encryption-certificate-to-cloud-service)
4. [在服務組態檔中更新加密憑證](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>使用現有的憑證從 hello 憑證存放區
1. [從憑證存放區匯出加密憑證](#export-encryption-certificate-from-certificate-store)
2. [上傳加密憑證 tooCloud 服務](#upload-encryption-certificate-to-cloud-service)
3. [在服務組態檔中更新加密憑證](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>使用 PFX 檔案中現有的憑證
1. [上傳加密憑證 tooCloud 服務](#upload-encryption-certificate-to-cloud-service)
2. [在服務組態檔中更新加密憑證](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>hello 預設組態
hello 預設組態會拒絕所有存取 toohello HTTP 端點。 這是建議的設定，因為 hello 要求 toothese 端點可能會夾帶資料庫認證等機密資訊的 hello。
hello 預設組態可讓所有存取 toohello HTTPS 端點。 這項設定可能會進一步限制。

### <a name="changing-hello-configuration"></a>變更 hello 組態
hello 套用 tooand 端點的存取控制規則的群組中設定 hello  **<EndpointAcls>**  > 一節中 hello**服務組態檔**。

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

中所設定的存取控制項群組中的 hello 規則<AccessControl name="">hello 服務組態檔區段。 

網路存取控制清單的文件說明 hello 格式。
例如，tooallow hello 範圍 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS 端點中的唯一 Ip，hello 規則看起來會像這樣：

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>阻絕服務預防
有兩個不同的機制支援 toodetect 並防止阻絕服務攻擊：

* 限制每個遠端主機的並行要求數目 (預設為關閉)
* 限制每個遠端主機的存取速率 (預設為開關)

這些根據 hello 進一步記載於 IIS 中的動態 IP 安全性的功能。 當變更此設定要小心的 hello 下列因素：

* hello 行為的 proxy 和網路位址轉譯裝置對 hello 遠端主機資訊
* Hello web 角色中的每個要求 tooany 資源會被視為 （例如載入指令碼、 影像和其他內容）

## <a name="restricting-number-of-concurrent-accesses"></a>限制並行存取的數量
設定此行為的 hello 設定如下：

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

變更 DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable 這項保護。

## <a name="restricting-rate-of-access"></a>限制存取的速率
設定此行為的 hello 設定如下：

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>設定 hello 回應 tooa 拒絕要求
hello 下列設定會設定 hello 回應 tooa 已拒絕要求：

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
如需其他支援的值，請參閱在 IIS 中的動態 IP 安全性 toohello 文件。

## <a name="operations-for-configuring-service-certificates"></a>設定服務憑證的作業
本主題僅供參考。 請遵循 hello 組態步驟中所述：

* 設定 hello SSL 憑證
* 設定用戶端憑證

## <a name="create-a-self-signed-certificate"></a>建立自我簽署憑證
執行：

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* -n hello 與服務 URL。 支援萬用字元 ("CN=*.cloudapp.net") 和替代名稱 ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net")。
* -e hello 憑證到期日與建立強式密碼，並指定它出現提示時。

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>建立自我簽署 SSL 憑證的 PFX 檔案
執行：

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

輸入密碼，然後使用這些選項來匯出憑證：

* 是，匯出 hello 私密金鑰
* 匯出所有延伸內容

## <a name="export-ssl-certificate-from-certificate-store"></a>從憑證存放區匯出 SSL 憑證
* 尋找憑證
* 按一下 [動作] -> [所有工作] -> [匯出...]
* 使用這些選項將憑證匯出至 .PFX 檔案：
  * 是，匯出 hello 私密金鑰
  * 如果可能包含 hello 憑證路徑中的所有憑證 * 匯出所有擴充的屬性

## <a name="upload-ssl-certificate-toocloud-service"></a>上傳 SSL 憑證 toocloud 服務
上傳以 hello 現有或產生的憑證。以 hello SSL 金鑰組的 PFX 檔案：

* 輸入 hello 密碼保護 hello 私密金鑰資訊

## <a name="update-ssl-certificate-in-service-configuration-file"></a>在服務組態檔中更新 SSL 憑證
更新下列 hello 指紋 hello 上傳憑證 toohello 雲端服務的 hello 服務組態檔中設定的 hello hello 憑證指紋值：

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>匯入 SSL 憑證授權單位
遵循下列步驟，在所有帳戶/機器將與 hello 服務進行通訊：

* 按兩下 hello。在 Windows 檔案總管的 CER 檔案
* 在 hello 憑證對話方塊中，按一下 安裝憑證...
* 憑證匯入到信任的根憑證授權單位存放區的 hello

## <a name="turn-off-client-certificate-based-authentication"></a>關閉用戶端憑證式驗證
只有用戶端憑證式驗證支援，並停用允許公用存取 toohello 服務端點，除非其他機制中的位置 （例如 Microsoft Azure 虛擬網路）。

變更 hello 服務組態檔 tooturn hello 功能中的這些設定 toofalse：

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

接著，將相同的憑證指紋與 hello SSL 憑證的 hello 複製在 hello CA 憑證設定：

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>建立自我簽署憑證授權單位
執行下列步驟 toocreate 為憑證授權單位的自我簽署的憑證 tooact hello:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize 它

* -e 與 hello 憑證到期日

## <a name="find-ca-public-key"></a>尋找 CA 公開金鑰
所有用戶端憑證必須發出 hello 服務所信任的憑證授權單位。 找到 hello 公用金鑰 toohello 發出 hello 將要 toobe 的用戶端憑證的憑證授權單位使用的驗證順序 tooupload 它 toohello 雲端服務。

如果找不到 hello hello 公開金鑰檔案，請將它匯出從 hello 憑證存放區：

* 尋找憑證
  * 用戶端憑證所發出的搜尋 hello 相同的憑證授權單位
* 按兩下 hello 憑證。
* 選取在 hello 憑證 對話方塊中的 hello 憑證路徑索引標籤。
* 按兩下 hello 路徑中的 hello CA 項目。
* 記下 hello 憑證內容。
* 關閉 hello**憑證**對話方塊。
* 尋找憑證
  * 搜尋 hello 先前所述的 CA。
* 按一下 [動作] -> [所有工作] -> [匯出...]
* 使用這些選項將憑證匯出至 .CER：
  * **否，不要匯出 hello 私密金鑰**
  * 如果可能的話 hello 憑證路徑中包含的所有憑證。
  * 匯出所有延伸內容。

## <a name="upload-ca-certificate-toocloud-service"></a>上傳 CA 憑證 toocloud 服務
上傳以 hello 現有或產生的憑證。Hello CA 公開金鑰的 CER 檔案。

## <a name="update-ca-certificate-in-service-configuration-file"></a>在服務組態檔中更新 CA 憑證
更新下列 hello 指紋 hello 上傳憑證 toohello 雲端服務的 hello 服務組態檔中設定的 hello hello 憑證指紋值：

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

更新下列設定以 hello 相同的 hello hello 值指紋：

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>發行用戶端憑證
每個個別的授權的 tooaccess hello 服務應該具有用戶端憑證發出 his/hers 獨佔使用，而且應該選擇強式密碼 tooprotect his/hers 擁有其私密金鑰。 

必須的 hello hello 自我簽署 CA 憑證的同一部電腦所產生及儲存中執行下列步驟的 hello:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

自訂：

* -n toohello 將與此憑證驗證的用戶端識別碼
* -e 與 hello 憑證到期日
* MyID.pvk 和 MyID.cer，使用這個用戶端憑證的唯一檔名

此命令會提示輸入密碼 toobe 建立，然後用一次。 請使用強式密碼。

## <a name="create-pfx-files-for-client-certificates"></a>建立用戶端憑證的 PFX 檔案
對於每個產生的用戶端憑證，請執行：

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

自訂：

    MyID.pvk and MyID.cer with hello filename for hello client certificate

輸入密碼，然後使用這些選項來匯出憑證：

* 是，匯出 hello 私密金鑰
* 匯出所有延伸內容
* 此憑證發給 hello 個別 toowhom 應該選擇 hello 匯出的密碼

## <a name="import-client-certificate"></a>匯入用戶端憑證
用戶端憑證已發出的每個個別應該匯入 hello 金鑰組在 hello 機器最初將使用 toocommunicate 與 hello 服務：

* 按兩下 hello。在 Windows 檔案總管的 PFX 檔案
* 憑證匯入到個人存放區至少這個選項的 hello:
  * 核取 [包含所有延伸內容]

## <a name="copy-client-certificate-thumbprints"></a>複製用戶端憑證指紋
用戶端憑證已發出的每個個別必須遵循下列步驟中的 his/hers 順序 tooobtain hello 指紋憑證將會加入 toohello 服務組態檔：

* 執行 certmgr.exe
* 選取 hello 個人 索引標籤
* 按兩下 hello toobe 用於驗證的用戶端憑證
* 在開啟的 hello 憑證對話方塊，選取 [hello 詳細資料] 索引標籤
* 請確定 [顯示] 是顯示 [全部]
* 選取 hello 欄位名為 hello 清單中的憑證指紋
* 複製 hello hello 指紋值 * * 刪除不可見的 Unicode 字元前面 hello 第一個數字 * * 刪除全部為空格

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Hello 服務組態檔中設定允許用戶端
更新下列 hello hello 允許存取 toohello 服務的用戶端憑證指紋的逗號分隔清單的 hello 服務組態檔中設定的 hello hello 值：

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>設定用戶端憑證撤銷檢查
hello 預設設定不會檢查以 hello 憑證授權單位用戶端憑證的撤銷狀態。 在 hello tooturn 檢查，如果 hello 發行 hello 用戶端憑證的憑證授權單位支援這類檢查，請變更 hello hello 值 hello X509RevocationMode 列舉型別中定義的其中一個具備下列設定：

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>建立自我簽署加密憑證的 PFX 檔案
如需加密憑證，請執行：

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

自訂：

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

輸入密碼，然後使用這些選項來匯出憑證：

* 是，匯出 hello 私密金鑰
* 匯出所有延伸內容
* 上傳 hello 憑證 toohello 雲端服務時，您將需要 hello 密碼。

## <a name="export-encryption-certificate-from-certificate-store"></a>從憑證存放區匯出加密憑證
* 尋找憑證
* 按一下 [動作] -> [所有工作] -> [匯出...]
* 使用這些選項將憑證匯出至 .PFX 檔案： 
  * 是，匯出 hello 私密金鑰
  * 如果可能包含 hello 憑證路徑中的所有憑證 
* 匯出所有延伸內容

## <a name="upload-encryption-certificate-toocloud-service"></a>上傳加密憑證 toocloud 服務
上傳以 hello 現有或產生的憑證。Hello 加密金鑰組的 PFX 檔案：

* 輸入 hello 密碼保護 hello 私密金鑰資訊

## <a name="update-encryption-certificate-in-service-configuration-file"></a>在服務組態檔中更新加密憑證
更新下列 hello 指紋 hello 上傳憑證 toohello 雲端服務的 hello 服務組態檔中設定的 hello hello 憑證指紋值：

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>常見的憑證作業
* 設定 hello SSL 憑證
* 設定用戶端憑證

## <a name="find-certificate"></a>尋找憑證
請遵循下列步驟：

1. 執行 mmc.exe。
2. [檔案] -> [新增/移除嵌入式管理單元]
3. 選取 [ **憑證**]。
4. 按一下 [新增] 。
5. 選擇 hello 憑證存放區位置。
6. 按一下 [完成] 。
7. 按一下 [確定] 。
8. 展開 [ **憑證**]。
9. 展開 hello 憑證存放區節點。
10. 展開 hello 憑證子節點。
11. 在 [hello] 清單中選取的憑證。

## <a name="export-certificate"></a>匯出憑證
在 hello**憑證匯出精靈**:

1. 按一下 [下一步] 。
2. 選取**是**，然後**匯出 hello 私密金鑰**。
3. 按一下 [下一步] 。
4. 選取 hello 想要的輸出檔案格式。
5. 核取 hello 所需的選項。
6. 核取 [ **密碼**]。
7. 輸入強式密碼並加以確認。
8. 按一下 [下一步] 。
9. 輸入或瀏覽 toostore hello 憑證的其中一個檔案名稱 (使用。PFX 副檔名）。
10. 按一下 [下一步] 。
11. 按一下 [完成] 。
12. 按一下 [確定] 。

## <a name="import-certificate"></a>匯入憑證
在 hello 憑證匯入精靈：

1. 選取 hello 存放區位置。
   
   * 選取**目前使用者**如果只在目前使用者 下執行的處理序將存取 hello 服務
   * 選取**本機**如果其他處理程序，請在此電腦將存取 hello 服務
2. 按一下 [下一步] 。
3. 如果從檔案匯入，確認 hello 檔案路徑。
4. 如果匯入 .PFX 檔案：
   1. 輸入 hello 保護 hello 私密金鑰的密碼
   2. 選取匯入選項
5. 選取 hello 下列存放區中的 「 位置 」 的憑證
6. 按一下 [瀏覽] 。
7. 選取 hello 所需的存放區。
8. 按一下 [完成] 。
   
   * 如果選擇 hello 受信任的根憑證授權單位存放區，按一下**是**。
9. 在所有對話方塊視窗上，按一下 [ **確定** ]。

## <a name="upload-certificate"></a>Upload certificate
在 hello [Azure 入口網站](https://portal.azure.com/)

1. 選取 [雲端服務] 。
2. 選取 hello 雲端服務。
3. 在 hello 上方功能表中，按一下 **憑證**。
4. Hello 下方列上，按一下**上傳**。
5. 選取 hello 憑證檔案。
6. 如果它是。PFX 檔案中，輸入 hello 私用金鑰 hello 密碼。
7. 完成後，複製 hello hello 清單中的新項目中的 hello 憑證指紋。

## <a name="other-security-considerations"></a>其他安全性考量
使用 hello HTTPS 端點時，這份文件中所述的 hello SSL 設定加密 hello 服務及其用戶端之間的通訊。 這是因為資料庫存取權的認證重要，而且 hello 通訊中所包含的其他可能的敏感資訊。 不過請注意，hello 服務持續發生內部狀態，包括認證，其內部的資料表中已經提供給中繼資料儲存在 Microsoft Azure 訂用帳戶中的 hello Microsoft Azure SQL 資料庫中。 該資料庫已定義為 hello 下列服務組態檔中的設定的一部分 (。CSCFG 檔案）： 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

這個資料庫中儲存的認證會被加密。 不過，最佳做法，請向上 toodate 保留 web 和背景工作角色的服務部署中，而且兩者都有存取 toohello 中繼資料資料庫與 hello 憑證用於加密和解密預存認證的安全，您會看到。 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

