---
title: "aaaHow toogenerate 和傳輸受 HSM 保護金鑰的 Azure 金鑰保存庫 |Microsoft 文件"
description: "使用此發行項 toohelp 規劃、 產生，和然後再將您自己的 HSM 保護的金鑰 toouse 使用 Azure 金鑰保存庫。 也稱為 BYOK 或「攜帶您自己的金鑰」。"
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>如何為 Azure 金鑰保存庫的 toogenerate 並傳輸受 HSM 保護金鑰
## <a name="introduction"></a>簡介
為求保險，當您使用 Azure 金鑰保存庫，您可以匯入或硬體安全性模組 (Hsm)，絕不能離開 hello HSM 界限中產生的索引鍵。 此案例中通常是參照的 tooas*整合您自己金鑰*，或 BYOK。 hello Hsm 是的 FIPS 140-2 Level 2 驗證。 Azure 金鑰保存庫會使用 Thales nShield 系列 Hsm tooprotect 您的金鑰。

使用此主題 toohelp 規劃、 產生，和然後再將您自己與 Azure 金鑰保存庫的 HSM 保護的金鑰 toouse hello 資訊。

此功能不適用於 Azure China。

> [!NOTE]
> 如需 Azure 金鑰保存庫的詳細資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)  
>
> 如需入門教學課程，其中包括建立受 HSM 保護之金鑰的金鑰保存庫，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。
>
>

有關產生及透過 hello 網際網路傳輸受 HSM 保護金鑰的詳細資訊：

* 您可以產生 hello 金鑰從離線工作站，能減少 hello 攻擊面。
* hello 金鑰進行加密與金鑰交換金鑰 (KEK) 」 是傳送的 toohello Azure 金鑰保存庫 Hsm 之前會持續加密。 只有 hello 加密的金鑰版本會離開 hello 原始工作站。
* hello 工具組會繫結您的金鑰 toohello Azure 金鑰保存庫安全園地租用戶金鑰上設定屬性。 因此在 hello Azure 金鑰保存庫 Hsm 接收和解密金鑰後，只有這些 Hsm 可使用它。 無法匯出您的金鑰。 這個繫結是由 hello Thales Hsm 強制執行。
* hello 金鑰交換金鑰 (KEK) 」 是使用的 tooencrypt 您的金鑰在 hello Azure 金鑰保存庫 Hsm 內部產生並不是可匯出。 hello Hsm 強制執行可能沒有外部 hello Hsm hello KEK 版本。 此外，hello 工具組包含了 thales 該 hello KEK 無法匯出，且在 Thales 製造的正版 HSM 內部產生的證明。
* hello 工具組包含了 thales 的 hello Azure 金鑰保存庫安全園地也在 Thales 製造的正版 HSM 產生的證明。 這證明證明 Microsoft 正在使用正版硬體 tooyou。
* Microsoft 會在每個地理區域使用不同的 KEK 和不同的「安全世界」。 這項分隔可確保您的金鑰可以是只在加密該 hello 地區資料中心內。 例如，來自歐洲客戶的金鑰不能在北美或亞洲的資料中心使用。

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Thales HSM 和 Microsoft 服務的詳細資訊
Thales 是提供服務資料加密和網路安全性解決方案 toohello 金融服務、 高科技、 製造、 政府及科技。 40 年追蹤記錄，以保護公司和政府資訊中，Thales 解決方案會使用四個 hello 五個最大能源和太空公司。 另外還有 22 個北大西洋公約組織國家也在使用他們的解決方案，而且全世界有超過 80% 的付款交易都受其保障。

Microsoft 與 Thales tooenhance hello 狀態封面的 Hsm 的合作。 這些增強功能可讓您 tooget hello 一般託管服務的好處不必放棄您金鑰的控制權。 具體來說，這些增強功能可讓 Microsoft 管理 hello Hsm，如此不需要。 為雲端服務、 Azure 金鑰保存庫會依據迅速 toomeet 升高貴組織的使用方式。 在 hello 相同時間，在 Microsoft 的 Hsm 內部保護您的金鑰： 您保留 hello 金鑰生命週期的控制權，因為您產生 hello 金鑰，並將它傳輸 tooMicrosoft 的 Hsm。

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>實作 Azure 金鑰保存庫的自備金鑰 (BYOK)
使用 hello 下列資訊和程序，如果您將會產生您自己的 HSM 保護金鑰並將其傳輸 tooAzure 金鑰保存庫 — hello 攜帶您自己的金鑰 (BYOK) 案例。

## <a name="prerequisites-for-byok"></a>BYOK 的必要條件
請參閱 hello 下表的必要條件清單為 Azure 金鑰保存庫整合您自己的金鑰 (BYOK)。

| 需求 | 詳細資訊 |
| --- | --- |
| 訂用帳戶 tooAzure |toocreate Azure 金鑰保存庫，您需要 Azure 訂用帳戶：[申請免費試用版](https://azure.microsoft.com/pricing/free-trial/) |
| hello Azure 金鑰保存庫 Premium 服務層 toosupport 受 HSM 保護的金鑰 |如需 Azure 金鑰保存庫 hello 服務層和功能的詳細資訊，請參閱 hello [Azure 金鑰保存庫定價](https://azure.microsoft.com/pricing/details/key-vault/)網站。 |
| Thales HSM、智慧卡和支援軟體 |您必須擁有存取 tooa Thales 硬體安全性模組並具備 Thales Hsm 的基礎操作知識。 請參閱[Thales 硬體安全性模組](https://www.thales-esecurity.com/msrms/buy)相容模型或 HSM，如果您還沒有 toopurchase hello 清單。 |
| hello 下列硬體和軟體：<ol><li>離線 x64 工作站、至少為 Windows 7 的 Windows 作業系統，以及至少為 11.50 版的 Thales nShield 軟體。<br/><br/>如果此工作站執行 Windows 7，您必須[安裝 Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe)。</li><li>工作站連接的 toohello 網際網路且具有至少 Windows 作業系統的 Windows 7 和[Azure PowerShell](/powershell/azure/overview) **最小版本 1.1.0**安裝。</li><li>至少有 16 MB 可用空間的 USB 磁碟機或其他可攜式儲存裝置。</li></ol> |基於安全性理由，我們建議 hello 第一個工作站不是連接的 tooa 網路。 不過，在程式設計方面並不強迫採取這項建議。<br/><br/>請注意，hello 接下來的指示，在此工作站參照的 tooas hello 中斷連線的工作站。</p></blockquote><br/>此外，如果您的租用戶金鑰適用於生產網路中，我們建議您使用的第二部個別工作站 toodownload hello 工具組和上傳 hello 租用戶金鑰。 但為了測試用途，您可以使用如 hello 第一個 hello 相同的工作站。<br/><br/>請注意，在 hello 接下來的指示，此第二部工作站參照的 tooas hello 連線網際網路的工作站。</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>產生並傳輸您的金鑰 tooAzure 金鑰保存庫 HSM
您將使用下列五個步驟 toogenerate hello，並傳輸您的金鑰 tooan Azure 金鑰保存庫 HSM:

* [步驟 1：準備網際網路連線的工作站](#step-1-prepare-your-internet-connected-workstation)
* [步驟 2：準備中斷連線的工作站](#step-2-prepare-your-disconnected-workstation)
* [步驟 3：產生您的金鑰](#step-3-generate-your-key)
* [步驟 4：準備要傳輸的金鑰](#step-4-prepare-your-key-for-transfer)
* [步驟 5： 傳送您的金鑰 tooAzure 金鑰保存庫](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>步驟 1：準備網際網路連線的工作站
第一個步驟中，請勿 hello 下列程序，您會連接的 toohello 網際網路的工作站上。

### <a name="step-11-install-azure-powershell"></a>步驟 1.1：安裝 Azure PowerShell
從 hello 連線網際網路的工作站，下載並安裝 hello Azure PowerShell 模組包含 hello cmdlet toomanage Azure 金鑰保存庫。 這需要得最低版本為 0.8.13。

如需安裝指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

### <a name="step-12-get-your-azure-subscription-id"></a>步驟 1.2：取得您的 Azure 訂用帳戶識別碼
啟動 Azure PowerShell 工作階段，並使用下列命令的 hello 登入 tooyour Azure 帳戶：

        Add-AzureAccount
在 [hello] 快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱和密碼。 然後，使用 hello [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0)命令：

        Get-AzureSubscription
從 hello 輸出，找出 hello 識別碼 hello 訂用帳戶將用於 Azure 金鑰保存庫。 您稍後將需要此訂用帳戶識別碼。

請勿關閉 hello Azure PowerShell 視窗。

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>步驟 1.3： 下載 Azure 金鑰保存庫 hello BYOK 工具組
前往 Microsoft 下載中心 toohello 和[下載 hello Azure 金鑰保存庫 BYOK 工具組](http://www.microsoft.com/download/details.aspx?id=45345)地理區域或 Azure 的執行個體。 使用 hello 下列資訊 tooidentify hello 封裝名稱 toodownload 以及其對應的 SHA 256 封裝的雜湊：

- - -
**美國：**

KeyVault-BYOK-Tools-UnitedStates.zip

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**歐洲︰**

KeyVault-BYOK-Tools-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**亞洲︰**

KeyVault-BYOK-Tools-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**拉丁美洲︰**

KeyVault-BYOK-Tools-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**日本︰**

KeyVault-BYOK-Tools-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**韓國：**

KeyVault-BYOK-Tools-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**澳大利亞：**

KeyVault-BYOK-Tools-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure Government:**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-Tools-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**美國政府國防部：**

KeyVault-BYOK-Tools-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**加拿大：**

KeyVault-BYOK-Tools-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**德國：**

KeyVault-BYOK-Tools-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**印度：**

KeyVault-BYOK-Tools-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**英國：**

KeyVault-BYOK-Tools-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

您已下載 BYOK 工具組，從您的 Azure PowerShell 工作階段，使用 hello toovalidate hello 完整性[Get-filehash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet。

    Get-FileHash KeyVault-BYOK-Tools-*.zip

hello 工具組包含下列 hello:

* 具有以 **BYOK-KEK-pkg-**
* 具有以 **BYOK-SecurityWorld-pkg-**
* 名為 **verifykeypackage.py** 的 python 指令碼。
* 名為 **KeyTransferRemote.exe** 的命令列可執行檔和相關聯的 DLL。
* Visual C++ 可轉散發套件，名為 **vcredist_x64.exe**。

複製 hello 封裝 tooa USB 磁碟機或其他可攜式儲存裝置。

## <a name="step-2-prepare-your-disconnected-workstation"></a>步驟 2：準備中斷連線的工作站
第二個步驟中，請勿 hello 下列程序不是連接的 tooa 網路 （網際網路 hello 或您的內部網路） 的 hello 工作站上。

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>步驟 2.1： 準備中斷連線的 hello 工作站使用 Thales HSM
在 Windows 電腦上安裝 hello nCipher (Thales) 支援軟體，再附加 Thales HSM toothat 電腦。

確定該 hello Thales 工具位於您的路徑 (**%nfast_home%\bin**)。 例如，輸入 hello 下列：

        set PATH=%PATH%;"%nfast_home%\bin"

如需詳細資訊，請參閱隨附 hello Thales HSM 的 hello 使用者指南。

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>步驟 2.2： 安裝 hello BYOK 工具組在 hello 中斷連線的工作站上
複製 hello BYOK 工具組封裝從 hello USB 磁碟機或其他可攜式儲存裝置，並執行再 hello 遵循：

1. Hello 下載封裝中的 hello 檔案解壓縮至任何資料夾中。
2. 從該資料夾執行 vcredist_x64.exe。
3. 請遵循 hello 指示 toohello for Visual Studio 2013 安裝 hello Visual c + + 執行階段元件。

## <a name="step-3-generate-your-key"></a>步驟 3：產生您的金鑰
第三個步驟中，請勿 hello hello 中斷連線的工作站上，下列程序。 toocomplete 此步驟中您的 HSM 必須在初始化模式。 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>步驟 3.1： 變更 hello HSM 模式 too'I'
如果您使用 Thales nShield 邊緣，toochange hello 模式： 1。 使用 hello 模式按鈕 toohighlight hello 必要的模式。 2. 在幾秒內，按住不放 hello 清除 按鈕的秒數。 Hello 模式變更時，如果 hello 新模式 LED 停止閃爍，則維持亮燈。 hello 狀態 LED 可能不規則快閃數秒鐘，然後閃爍 hello 裝置已就緒時，定期。 否則，hello 裝置仍會留在 hello 目前的模式，與 hello 適當模式 LED 亮起。

### <a name="step-32-create-a-security-world"></a>步驟 3.2：建立安全世界
啟動命令提示字元並執行 Thales new-world 程式 hello。

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

此程式會**安全園地**檔案位於 %nfast_kmdata%\local\world，對應 toohello C:\ProgramData\nCipher\Key Management Data\local 資料夾對應。 您可以使用不同的值為 hello 仲裁，但是在本例中，您可以提示的 tooenter 三卡片和 pin，針對每個。 然後，任兩張卡片提供完整存取 toohello 安全園地。 這些卡片將成為 hello**系統管理員卡組**hello 新安全園地。

然後 hello 遵循：

* Hello world 檔案備份。 安全和保護 hello world 檔案、 hello 系統管理員卡及其 pin 碼，並確定沒有一個人可存取 toomore 比一張牌。

### <a name="step-33-change-hello-hsm-mode-tooo"></a>步驟 3.3： 變更 hello HSM 模式 too'O'
如果您使用 Thales nShield 邊緣，toochange hello 模式： 1。 使用 hello 模式按鈕 toohighlight hello 必要的模式。 2. 在幾秒內，按住不放 hello 清除 按鈕的秒數。 Hello 模式變更時，如果 hello 新模式 LED 停止閃爍，則維持亮燈。 hello 狀態 LED 可能不規則快閃數秒鐘，然後閃爍 hello 裝置已就緒時，定期。 否則，hello 裝置仍會留在 hello 目前的模式，與 hello 適當模式 LED 亮起。


### <a name="step-34-validate-hello-downloaded-package"></a>步驟 3.4： 驗證下載的 hello 套件
這個步驟是選擇性但建議使用，因此，您可以驗證下列 hello:

* 已從正版 Thales HSM 產生 hello 隨附於 hello 工具組的金鑰交換金鑰。
* 已在正版 Thales HSM 中產生的 hello 隨附於 hello 工具組的安全園地的 hello 雜湊。
* hello 金鑰交換金鑰為非可匯出。

> [!NOTE]
> toovalidate hello 下載封裝，hello HSM 必須連接、 電源已開啟，而且必須具有安全園地上 （例如您剛才建立的其中一個 hello)。
>
>

toovalidate hello 下載封裝：

1. 輸入一個 hello 下列程式碼，根據您的地理區域或 Azure 的執行個體，以執行 hello verifykeypackage.py 指令碼：

   * 北美洲：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * 歐洲：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * 亞洲：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * 拉丁美洲：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * 日本：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * 韓國︰

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * 澳大利亞：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * 如[Azure 政府](https://azure.microsoft.com/features/gov/)，它會使用的 Azure hello 美國政府執行個體：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * 美國政府國防部：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * 針對加拿大：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * 針對德國：

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * 針對印度︰

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > hello Thales 軟體包含 python，位於 %NFAST_HOME%\python\bin
     >
     >
2. 確認您看到 hello 下列表示成功驗證：**結果： 成功**

此指令碼會驗證 hello 簽章者鏈結，向上 toohello Thales 根金鑰。 此根金鑰的 hello 雜湊內嵌於 hello 指令碼，且其值必須為**59178a47 de508c3f 291277ee 184f46c4 f1d9c639**。 您也可以確認此值分別造訪 hello [Thales 網站](http://www.thalesesec.com/)。

您現在準備好 toocreate 新的金鑰。

### <a name="step-35-create-a-new-key"></a>步驟 3.5：建立新的金鑰
產生的金鑰使用 hello Thales **generatekey**程式。

執行下列命令 toogenerate hello 按鍵 hello:

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

當您執行此命令時，請使用下列指示：

* hello 參數*保護*toohello 值必須設定**模組**，如下所示。 這會建立受模組保護的金鑰。 hello BYOK 工具組不支援 OCS 保護的金鑰。
* 取代 hello 值*contosokey* hello **ident**和**contosokey**與任何字串值。 toominimize 系統管理負擔並降低 hello 風險的錯誤，我們建議您使用相同的兩個值的 hello。 hello **ident**值必須包含數字、 虛線和小寫字母。
* hello 的 pubexp 保留空白 （預設值） 在此範例中，但您可以指定特定的值。 如需詳細資訊，請參閱 hello Thales 文件。

此命令會使用名稱開頭為您的 %NFAST_KMDATA%\local 資料夾中建立信號化金鑰檔案**key_simple_**，後面接著 hello **ident** hello 命令中指定。 例如：**key_simple_contosokey**。 此檔案包含已加密的金鑰。

在安全的位置備份此語彙基元化金鑰檔案。

> [!IMPORTANT]
> 當您稍後將傳輸您的金鑰 tooAzure 金鑰保存庫時，Microsoft 無法將此金鑰後 tooyou，因此是極為重要，您的金鑰和安全園地安全地備份。 如需備份金鑰的指引及最佳作法，請連絡 Thales。
>
>

您會立即準備 tootransfer 您金鑰的 tooAzure 金鑰保存庫。

## <a name="step-4-prepare-your-key-for-transfer"></a>步驟 4：準備要傳輸的金鑰
第四個步驟中，請勿 hello hello 中斷連線的工作站上，下列程序。

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>步驟 4.1：使用降低權限建立金鑰的複本

開啟新的命令提示字元，變更 hello 目前的目錄 toohello 位置您解壓縮 hello BYOK zip 檔案。 tooreduce hello 權限，在您的金鑰，請從命令提示字元上執行 hello 下列程式碼，根據您的地理區域或 Azure 的執行個體的其中一個：

* 北美洲：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* 歐洲：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* 亞洲：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* 拉丁美洲：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* 日本：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* 韓國︰

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* 澳大利亞：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* 如[Azure 政府](https://azure.microsoft.com/features/gov/)，它會使用的 Azure hello 美國政府執行個體：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* 美國政府國防部：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* 針對加拿大：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* 針對德國：

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* 針對印度︰

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

當您執行此命令時，取代*contosokey* hello 與相同的值中指定**步驟 3.5： 建立新的金鑰**從 hello[產生您的金鑰](#step-3-generate-your-key)步驟。

系統會詢問 tooplug 您安全園地系統管理的卡片。

Hello 命令完成時，您會看到**結果： 成功**hello 降低權限金鑰副本 hello 名為 key_xferacId_ 的檔案，而且<contosokey>。

您可能會檢查 hello ACL 使用下列命令使用 hello Thales 公用程式：

* aclprint.py：

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe：

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  當您執行這些命令時，取代 contosokey 以相同的值中指定的 hello**步驟 3.5： 建立新的金鑰**從 hello[產生您的金鑰](#step-3-generate-your-key)步驟。

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>步驟 4.2：使用 Microsoft 的金鑰交換金鑰來加密您的金鑰
執行下列命令，根據您的地理區域或 Azure 的執行個體的 hello 的其中一個：

* 北美洲：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 歐洲：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 亞洲：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 拉丁美洲：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 日本：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 韓國︰

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 澳大利亞：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 如[Azure 政府](https://azure.microsoft.com/features/gov/)，它會使用的 Azure hello 美國政府執行個體：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 美國政府國防部：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 針對加拿大：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 針對德國：

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* 針對印度︰

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

當您執行此命令時，請使用下列指示：

* 取代*contosokey*用 toogenerate hello 索引鍵中的 hello 識別碼**步驟 3.5： 建立新的金鑰**從 hello[產生您的金鑰](#step-3-generate-your-key)步驟。
* 取代*SubscriptionID* hello hello 包含金鑰保存庫的 Azure 訂用帳戶 id。 擷取此值先前在**步驟 1.2： 取得您的 Azure 訂用帳戶 ID**從 hello[準備連線網際網路的工作站](#step-1-prepare-your-internet-connected-workstation)步驟。
* 以用於輸出檔案名稱的標籤取代 *ContosoFirstHSMKey*。

當成功完成時，它會顯示**結果： 成功**，而且具有下列名稱的 hello hello 目前資料夾中沒有新的檔案： KeyTransferPackage-*ContosoFirstHSMkey*.byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>步驟 4.3： 複製您金鑰傳輸封裝 toohello 連線網際網路的工作站
使用從 hello 上一個步驟 (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour 連線網際網路的工作站的 USB 磁碟機或其他可攜式儲存裝置 toocopy hello 輸出檔案。

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>步驟 5： 傳送您的金鑰 tooAzure 金鑰保存庫
最後一個步驟中，在 hello 連線網際網路的工作站上，使用 hello [Add-azurekeyvaultkey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello 金鑰傳輸封裝，您所複製的 hello 中斷連線的工作站 toohello Azure 金鑰保存庫 HSM:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

如果 hello 上傳成功時，您會看到您剛才加入的 hello 金鑰顯示的 hello 屬性。

## <a name="next-steps"></a>後續步驟
您現在可以在您的金鑰保存庫中使用這個受 HSM 保護的金鑰。 如需詳細資訊，請參閱 hello**如果您想 toouse 硬體安全性模組 (HSM)** > 一節中 hello[開始使用 Azure 金鑰保存庫](key-vault-get-started.md)教學課程。
