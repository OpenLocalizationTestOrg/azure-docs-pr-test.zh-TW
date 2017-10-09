



根據您的環境和選擇，hello 指令碼可以建立所有 hello 的叢集基礎結構，包括 hello Azure 虛擬網路、 儲存體帳戶、 雲端服務、 網域控制站、 遠端或本機 SQL 資料庫、 前端節點和其他叢集節點。 或者，hello 指令碼可以使用預先存在的 Azure 基礎結構，並建立僅 hello HPC 叢集的節點。

如需規劃 HPC Pack 叢集的背景資訊，請參閱 hello[產品評估及規劃](https://technet.microsoft.com/library/jj899596.aspx)和[入門](https://technet.microsoft.com/library/jj899590.aspx)hello HPC Pack 2012 R2 TechNet 文件庫中的內容。

## <a name="prerequisites"></a>必要條件
* **Azure 訂用帳戶**： 您可以使用任一 hello Azure Global 或 Azure China 服務中的訂用帳戶。 您的訂用帳戶限制會影響叢集節點，您可以部署的 hello 數目和類型。 如需相關資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../articles/azure-subscription-service-limits.md)。
* **使用 Azure PowerShell 0.8.10 Windows 用戶端電腦或更新版本安裝並設定**： 請參閱[開始使用 Azure PowerShell](/powershell/azureps-cmdlets-docs)的安裝指示和步驟 tooconnect tooyour Azure 訂用帳戶。
* **HPC Pack IaaS 部署指令碼**： 下載並解壓縮 hello 最新版 hello 指令碼從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949)。 執行檢查 hello hello 指令碼版本`New-HPCIaaSCluster.ps1 –Version`。 這篇文章根據 4.5.2 版的 hello 指令碼。
* **指令碼組態檔**： 建立 hello 指令碼會使用 tooconfigure hello HPC 叢集的 XML 檔案。 資訊與範例，請參閱本文稍後的章節，hello hello 部署指令碼及伴隨的 Manual.rtf 檔案。

## <a name="syntax"></a>語法
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> 系統管理員身分執行 hello 指令碼。
> 
> 

### <a name="parameters"></a>參數
* **ConfigFile**： 指定 hello hello 設定檔 toodescribe hello HPC 叢集的檔案路徑。 請參閱本主題中，或在 hello hello 資料夾包含 hello 指令碼中的 Manual.rtf 檔案 hello 設定檔有關的詳細資訊。
* **AdminUserName**： 指定 hello 使用者名稱。 如果 hello 網域樹系由 hello 指令碼，這會成為所有 Vm 的 hello 本機系統管理員使用者名稱和 hello 網域系統管理員名稱。 如果 hello 網域樹系已存在，這指定 hello 網域使用者，如 hello 本機系統管理員使用者名稱 tooinstall HPC Pack 也一樣。
* **AdminPassword**： 指定 hello 系統管理員的密碼。 如果未指定 hello 命令列中，hello 指令碼會提示您 tooinput hello 密碼。
* **HPCImageName** （選擇性）： 指定使用 toodeploy hello HPC 叢集的 hello HPC Pack VM 映像名稱。 它必須是從 hello Azure Marketplace 提供 Microsoft HPC Pack 映像。 如果未指定 （通常） ﹜ 呤 hello 指令碼會選擇最新發行的 hello [HPC Pack 2012 R2 映像](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)。 hello 最新的映像為基礎的 HPC Pack 2012 R2 Update 3 安裝 Windows Server 2012 R2 Datacenter。
  
  > [!NOTE]
  > 若未指定有效的 HPC Pack 映像，部署將會失敗。
  > 
  > 
* **記錄檔**（選擇性）： 指定 hello 部署記錄檔路徑。 如果未指定，hello 指令碼會建立 hello 執行 hello 指令碼的 hello 電腦的暫存目錄中的記錄檔。
* **強制**（選擇性）： 隱藏所有 hello 確認提示。
* **NoCleanOnFailure** （選擇性）： 指定不會移除該 hello 未成功部署的 Azure Vm。 手動移除這些 Vm，然後再重新執行指令碼 toocontinue hello 部署 hello，或 hello 部署可能會失敗。
* **PSSessionSkipCACheck** （選擇性）： 已使用此指令碼部署的每個雲端服務，如自我簽署的憑證自動由 Azure 產生，並且 hello 雲端服務中的所有 hello Vm 都使用與此憑證 hello 預設 Windows遠端管理 (WinRM) 憑證。 toodeploy HPC 功能，在這些 Azure Vm 中的，預設 hello 指令碼中暫時安裝這些憑證 hello 本機電腦\\受信任的根憑證授權單位存放區的 hello 用戶端電腦 toosuppress hello 「 不受信任 CA 」 安全性指令碼執行期間發生錯誤。 hello 指令碼完成時，會移除 hello 憑證。 如果指定此參數，hello 憑證不會安裝在 hello 用戶端電腦上，並隱藏 hello 安全性警告。
  
  > [!IMPORTANT]
  > 此參數不建議用於生產部署。
  > 
  > 

### <a name="example"></a>範例
hello 下列範例會建立與使用組態檔的 HPC Pack 叢集*MyConfigFile.xml*，並指定安裝 hello 叢集系統管理員認證。

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>其他考量
* hello 指令碼可選擇啟用透過 hello HPC Pack web 入口網站或 hello HPC Pack REST API 提交作業。
* 如果您想 tooinstall 其他軟體或設定其他設定 hello 指令碼 （選擇性） 可以 hello 前端節點上執行自訂的前置和後置組態指令碼。

## <a name="configuration-file"></a>組態檔
hello hello 部署指令碼的組態檔是 XML 檔案。 hello 結構描述檔案 HPCIaaSClusterConfig.xsd 位於 hello HPC Pack IaaS 部署指令碼資料夾中。 **IaaSClusterConfig**是根項目 hello hello 組態檔，其中包含 hello hello hello 部署指令碼資料夾中的 Manual.rtf 檔案中的詳細資料 中描述的子元素。

