---
title: "組件 2016 aaaHPC 叢集在 Azure 中 |Microsoft 文件"
description: "了解 toodeploy HPC Pack 2016 在 Azure 中的叢集化"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>在 Azure 中部署 HPC Pack 2016 叢集

請遵循本文章 toodeploy 中的 hello 步驟[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) Azure 虛擬機器中的叢集。 HPC Pack 是建置在 Microsoft Azure 和 Windows Server 技術上的 Microsoft 免費 HPC 解決方案，並支援各種 HPC 工作負載。

使用其中一種 hello [Azure 資源管理員範本](https://github.com/MsHpcPack/HPCPack2016)toodeploy hello HPC Pack 2016 叢集。 您可以選擇多種叢集拓撲，當中包含不同數目的叢集前端節點，與 Linux 或 Windows 運算節點。

## <a name="prerequisites"></a>必要條件

### <a name="pfx-certificate"></a>PFX 憑證

Microsoft HPC Pack 2016 叢集需要 hello HPC 節點之間的個人資訊交換 (PFX) 憑證 toosecure hello 通訊。 hello 憑證必須符合下列需求的 hello:

* 它必須有能夠進行金鑰交換的私密金鑰
* 金鑰使用方法包含數位簽章和金鑰加密
* 增強金鑰使用方法包含用戶端驗證和伺服器驗證

如果您還沒有符合這些需求的憑證，您可以從憑證授權單位要求 hello 憑證。 或者，您可以使用下列命令 toogenerate hello 自我簽署的憑證 hello 的作業系統執行 hello 命令，並使用私密金鑰匯出 hello PFX 格式憑證為基礎的 hello。

* **Windows 10 或 Windows Server 2016**，執行內建的 hello **New-selfsignedcertificate** PowerShell cmdlet，如下所示：

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **適用於作業系統比 Windows 10 或 Windows Server 2016 更早**，下載 hello[自我簽署的憑證的產生器](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/)從 Microsoft 指令碼中心 hello。 將其內容解壓縮，然後執行下列 PowerShell 命令提示字元命令的 hello:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>上傳憑證 tooan Azure 金鑰保存庫

在部署之前 hello HPC 叢集上, 傳 hello 憑證 tooan [Azure 金鑰保存庫](../../key-vault/index.md)為下列 hello 部署期間使用資訊的密碼，並記錄 hello:**保存庫名稱**， **保存庫的資源群組**，**憑證 URL**，和**憑證指紋**。

以下範例 PowerShell 指令碼 tooupload hello 憑證。 如需有關上傳憑證 tooan Azure 金鑰保存庫的詳細資訊，請參閱[開始使用 Azure 金鑰保存庫](../../key-vault/key-vault-get-started.md)。

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a>支援的拓撲

選擇其中一個 hello [Azure 資源管理員範本](https://github.com/MsHpcPack/HPCPack2016)toodeploy hello HPC Pack 2016 叢集。 以下是三個受支援叢集拓撲的高層架構。 高可用性拓撲包含多個叢集前端節點。

1. 包含 Active Directory 網域的高可用性叢集

    ![AD 網域中的 HA 叢集](./media/hpcpack-2016-cluster/haad.png)



2. 不包含 Active Directory 網域的高可用性叢集

    ![不包含 AD 網域的 HA 叢集](./media/hpcpack-2016-cluster/hanoad.png)

3. 包含單一前端節點的叢集

   ![包含單一前端節點的叢集](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>部署叢集

toocreate hello 叢集中，選擇的範本，然後按一下 **部署 tooAzure**。 在 hello [Azure 入口網站](https://portal.azure.com)，hello 步驟中所述，請指定 hello 範本參數。 每個範本建立 hello HPC 叢集基礎結構所需的所有 Azure 資源。 資源包括 Azure 虛擬網路、公用 IP 位址、負載平衡器 (僅適用於高可用性叢集)、網路介面、可用性設定組、儲存體帳戶和虛擬機器。

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>步驟 1： 選取 hello 訂用帳戶、 位置和資源群組

hello**訂用帳戶**和 hello**位置**必須維持相同，指定當您上傳 PFX 憑證 （請參閱必要條件）。 我們建議您建立**資源群組**hello 部署。

### <a name="step-2-specify-hello-parameter-settings"></a>步驟 2： 指定 hello 參數設定

輸入或修改 hello 範本參數的值。 按一下 hello 圖示下一步 tooeach 參數的說明資訊。 另請參閱 hello 指導[可用的 VM 大小](sizes.md)。

指定您記錄中的下列參數的 hello 的 hello 必要條件的 hello 值：**保存庫名稱**，**保存庫的資源群組**，**憑證 URL**，和**憑證指紋**。

### <a name="step-3-review-legal-terms-and-create"></a>步驟 3. 檢閱法律條款並建立
按一下**檢查 法律條款**tooreview hello 條款。 如果您同意，請按一下**購買**，然後按一下**建立**toostart hello 部署。

## <a name="connect-toohello-cluster"></a>Toohello 叢集連線
1. Hello HPC Pack 叢集部署之後，請繼續 toohello [Azure 入口網站](https://portal.azure.com)。 按一下**資源群組**，與叢集部署中的 hello 尋找 hello 資源群組。 您可以找到 hello 前端節點的虛擬機器。

    ![Hello 入口網站中的叢集前端節點](./media/hpcpack-2016-cluster/clusterhns.png)

2. 按一下一個前端節點 （在高可用性叢集上，按一下任何 hello 前端節點）。 在**Essentials**，您可以找到 hello 公用 IP 位址或 hello 叢集的完整 DNS 名稱。

    ![叢集連線設定](./media/hpcpack-2016-cluster/clusterconnect.png)

3. 按一下**連接**toolog tooany 的 hello 與您指定的系統管理員的使用者名稱中使用遠端桌面的前端節點上。 如果您部署的 hello 叢集是 Active Directory 網域中，hello 使用者名稱為 hello 表單的<privateDomainName> \<adminUsername > (例如，hpc.local\hpcadmin)。

## <a name="next-steps"></a>後續步驟
* 提交工作 tooyour 叢集。 請參閱[提交作業 tooHPC 在 Azure 中的 HPC Pack 叢集](hpcpack-cluster-submit-jobs.md)和[管理使用 Azure Active Directory 在 Azure 中的 HPC Pack 2016 叢集](hpcpack-cluster-active-directory.md)。

