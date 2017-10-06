---
title: "aaaSecure 您金鑰保存庫 |Microsoft 文件"
description: "管理金鑰保存庫的存取權限，來管理保存庫以及金鑰和密碼。 金鑰保存庫，和如何 toosecure 您金鑰保存庫的驗證和授權模型"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>保護您的金鑰保存庫
Azure 金鑰保存庫是用來保護雲端應用程式加密金鑰和密碼 (例如憑證、連接字串、密碼) 的雲端服務。 由於此資料區分和重要商務資料，您想要 toosecure 存取 tooyour 金鑰保存庫，如此只有獲得授權的應用程式，而使用者可以存取金鑰保存庫。 這篇文章會提供金鑰保存庫存取模型的概觀，說明驗證和授權，並描述 toosecure 存取 tookey 為您的雲端應用程式，並以範例的保存庫。

## <a name="overview"></a>概觀
存取 tooa 金鑰保存庫由兩個不同的介面： 管理平面和資料飛機。 對於這兩個平面適當的驗證和授權都需要之前 （使用者或應用程式） 的呼叫端可以取得存取 tookey 保存庫。 授權會判斷哪些作業 hello 呼叫端允許 tooperform 時，驗證就會建立 hello 的 hello 的呼叫端的身分識別。

管理平面和資料平面都會使用 Azure Active Directory 來進行驗證。 至於授權，管理平面使用角色型存取控制 (RBAC)，資料平面則使用金鑰保存庫存取原則。

以下是以概略認識 hello 所討論的主題：

[使用 Azure Active Directory 驗證](#authentication-using-azure-active-directory)-本章節將說明如何呼叫者向 Azure Active Directory tooaccess 管理平面和資料飛機透過金鑰保存庫。 

[管理平面和資料平面](#management-plane-and-data-plane) - 管理平面和資料平面是用來存取金鑰保存庫的兩個存取平面。 這兩個存取平面各支援特定作業。 本章節描述 hello 存取端點，支援，及存取控制方法的每個平面所使用的作業。 

[管理平面存取控制](#management-plane-access-control)-我們將探討允許存取 toomanagement 平面作業使用以角色為基礎的存取控制這一節。

[平面資料的存取控制](#data-plane-access-control)-本節描述如何 toouse 金鑰保存庫的存取原則 toocontrol 資料平面存取。

[範例](#example)-這個範例說明如何 toosetup 存取控制對金鑰保存庫 tooallow 三個不同小組 （安全性小組、 開發人員/operators 和稽核員） tooperform 特定工作 toodevelop，管理和監視 Azure 中的應用程式.

## <a name="authentication-using-azure-active-directory"></a>使用 Azure Active Directory 進行驗證
當您在 Azure 訂用帳戶中建立金鑰保存庫時，它會自動關聯於 hello 訂用帳戶的 Azure Active Directory 租用戶。 （使用者和應用程式） 的所有呼叫端必須是在此租用戶 tooaccess 註冊此金鑰保存庫。 應用程式或使用者必須向 Azure Active Directory tooaccess 金鑰保存庫。 這適用於 tooboth 管理平面和資料飛機存取。 在這兩種情況中，應用程式可透過兩種方式存取金鑰保存庫︰

* **使用者 + 應用程式的存取** - 這通常適用於代表登入之使用者存取金鑰保存庫的應用程式。 舉例來說，Azure PowerShell 和 Azure 入口網站便是這類存取。 有兩種方式 toogrant 存取 toousers： 其中一種方式 toogrant 存取 toousers 讓他們可以從任何應用程式存取金鑰保存庫，而 hello 另一種方式 toogrant 使用者存取 tookey 保存庫才會使用特定的應用程式 （參考的 tooas 複合身分識別）。 
* **僅限應用程式存取**-應用程式，執行服務精靈服務時，背景工作等 hello 應用程式的身分識別會授與存取 toohello 金鑰保存庫。

在這兩種類型的應用程式中，hello 應用程式向 Azure Active Directory 使用任何 hello[支援的驗證方法](../active-directory/active-directory-authentication-scenarios.md)並取得語彙基元。 使用驗證方法，取決於 hello 應用程式類型。 然後 hello 應用程式會使用此 token，並將傳送 REST API 要求 tookey 保存庫。 如果管理平面存取 hello 要求會透過 Azure 資源管理員端點傳送。 當存取資料平面，hello 應用程式直接交談 tooa 金鑰保存庫端點。 查看詳細 hello[整個驗證流程](../active-directory/active-directory-protocols-oauth-code.md)。 

hello hello 應用程式要求權杖的資源名稱會有所不同 hello 應用程式是否存取管理平面或資料平面。 因此 hello 資源名稱是管理平面或資料平面端點，就是在更新版本的區段中，根據 hello Azure 環境的 hello 表所述。

一個單一的機制來驗證 tooboth 管理和資料飛機會有它自己的優點：

* 組織可以集中控制存取 tooall 金鑰保存庫中組織
* 如果使用者離職後，就立即無法存取 tooall hello 組織中的金鑰保存庫
* 組織可以自訂驗證，透過 Azure Active Directory (例如，啟用 multi-factor authentication 提高安全性) 中的 hello 選項

## <a name="management-plane-and-data-plane"></a>管理平面和資料平面
Azure 金鑰保存庫是一項可透過 Azure Resource Manager 部署模型取得的 Azure 服務。 當您建立金鑰保存庫時，就會獲得虛擬容器以供您在其中建立其他物件，像是金鑰、密碼和憑證。 然後您可以存取金鑰保存庫中，使用管理平面和資料飛機 tooperform 特定作業。 管理平面介面是您的金鑰保存庫本身，例如建立、 刪除、 更新金鑰保存庫屬性以及設定資料平面的存取原則，使用的 toomanage。 資料平面介面是使用的 tooadd、 刪除、 修改及使用 hello 金鑰、 密碼，以及儲存在金鑰保存庫中的憑證。

hello 管理平面和資料飛機介面是透過不同的端點 （請參閱資料表） 存取。 hello hello 資料表中的第二個資料行描述這些端點在不同的 Azure 環境的 hello DNS 名稱。 hello 第三個資料行描述您可以從每個存取平面執行 hello 作業。 每個存取平面也有自己的存取控制機制︰管理平面使用 Azure Resource Manager 角色型存取控制 (RBAC) 來設定存取控制，資料平面則使用金鑰保存庫存取原則來設定存取控制。

| 存取平面 | 存取端點 | 作業 | 存取控制機制 |
| --- | --- | --- | --- |
| 管理平面 |**全域：**<br> management.azure.com:443<br><br> **Azure 中國︰**<br> management.chinacloudapi.cn:443<br><br> **Azure 美國政府︰**<br> management.usgovcloudapi.net:443<br><br> **Azure 德國︰**<br> management.microsoftazure.de:443 |建立/讀取/更新/刪除金鑰保存庫 <br> 設定金鑰保存庫的存取原則<br>設定金鑰保存庫的標籤 |Azure Resource Manager 角色型存取控制 (RBAC) |
| 資料平面 |**全域：**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure 中國︰**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure 美國政府︰**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure 德國︰**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |針對金鑰︰解密、加密、解除包裝金鑰、包裝金鑰、驗證、簽署、取得、列出、更新、建立、匯入、刪除、備份、還原<br><br> 針對密碼︰取得、列出、設定、刪除 |金鑰保存庫存取原則 |

hello 管理平面和資料飛機存取控制獨立工作。 例如，如果您想 toogrant 應用程式存取 toouse 金鑰的金鑰保存庫中，您只需要 toogrant 資料平面存取權限使用金鑰保存庫的存取原則並沒有管理平面為需要存取此應用程式。 相反地，如果您想使用者 toobe 無法 tooread 保存庫屬性和標記，但是沒有任何存取 tookeys、 密碼或憑證，您可以授與這位使用者，並需要使用 RBAC 和沒有存取 toodata 平面 'read' 存取。

## <a name="management-plane-access-control"></a>管理平面存取控制
hello 管理平面包含會影響本身的 hello 金鑰保存庫的作業。 例如，您可以建立或刪除金鑰保存庫。 您可以取得訂用帳戶中的保存庫清單。 您可以擷取金鑰保存庫屬性 （例如 SKU 標記)，並設定金鑰保存庫的存取原則以控制 hello 使用者和應用程式可以存取金鑰和秘密 hello 金鑰保存庫中。 管理平面存取控制會使用 RBAC。 請參閱 hello 的金鑰保存庫執行的作業，可以透過管理平面在前面章節中的 hello 資料表中的完整清單。 

### <a name="role-based-access-control-rbac"></a>角色型存取控制 (RBAC)
每一個 Azure 訂用帳戶都具有 Azure Active Directory。 使用者、 群組和應用程式從這個目錄可以授與存取 toomanage hello Azure 訂用帳戶中的使用資源 hello Azure Resource Manager 部署模型。 這種類型的存取控制是參照的 tooas 角色型存取控制 (RBAC)。 toomanage 這存取，您可以使用 hello [Azure 入口網站](https://portal.azure.com/)，hello [Azure CLI 工具](../cli-install-nodejs.md)， [PowerShell](/powershell/azureps-cmdlets-docs)，或使用 hello [Azure 資源管理員 REST Api](https://msdn.microsoft.com/library/azure/dn906885.aspx).

使用 hello Azure Resource Manager 模型時，您建立金鑰保存庫資源群組和控制存取 toohello 管理平面中的此金鑰保存庫使用 Azure Active Directory。 例如，您可以授與使用者或群組能夠 toomanage 金鑰保存庫中特定資源群組。

您可以將適當的 RBAC 角色指派，以授與存取 toousers、 群組和應用程式在特定範圍。 例如，toogrant 存取 tooa 使用者 toomanage 金鑰保存庫就像是將預先定義的角色 '金鑰保存庫參與者' 指派 toothis 使用者在特定範圍。 hello 範圍在此情況下會是訂用帳戶、 資源群組或只特定的金鑰保存庫。 在訂用帳戶層級指派角色適用於 tooall 資源群組與該訂用帳戶內的資源。 在資源群組層級指派角色適用於 tooall 該資源群組中的資源。 指派特定資源的角色僅適用於 toothat 資源。 有數個預先定義的角色 (請參閱[RBAC： 內建角色](../active-directory/role-based-access-built-in-roles.md))，和 hello 如果預先定義的角色不符合您需求，您也可以定義您自己的角色。

> [!IMPORTANT]
> 請注意，是否使用者具有參與者權限 (RBAC) tooa 金鑰保存庫管理平面，她可以授與自己存取 toodata 平面，藉由設定金鑰保存庫的存取原則控制存取 toodata 平面。 因此，建議您使用 tootightly 控制著具有 '參與者' 存取 tooyour 金鑰保存庫 tooensure 只有獲得授權的人員可以存取和管理您的金鑰保存庫、 金鑰、 密碼和憑證。
> 
> 

## <a name="data-plane-access-control"></a>資料平面存取控制
hello 金鑰保存庫資料平面包含會影響在金鑰保存庫，例如金鑰、 密碼，以及憑證的 hello 物件的作業。  這包括金鑰作業 (例如建立、匯入、更新、列出、備份和還原金鑰)、密碼編譯作業 (例如簽署、驗證、加密、解密、包裝和解除包裝)，以及為金鑰設定標籤和其他屬性。 同樣地，針對密碼所包含的是取得、設定、列出、刪除。

資料平面的存取權是藉由設定金鑰保存庫的存取原則來授與。 使用者、 群組或應用程式必須具有該金鑰的保存庫金鑰保存庫 toobe 無法 tooset 存取原則的管理平面的參與者權限 (RBAC)。 使用者、 群組或應用程式可以授與存取金鑰或金鑰保存庫中的機密 tooperform 特定作業。 金鑰保存庫的 too16 存取原則項目上的金鑰保存庫支援。 建立 Azure Active Directory 安全性群組，並加入使用者 toothat 群組 toogrant 資料平面存取 tooseveral 使用者 tooa 金鑰保存庫。

### <a name="key-vault-access-policies"></a>金鑰保存庫存取原則
個別金鑰保存庫的存取原則授與權限 tookeys、 密碼和憑證。 例如，您可以提供使用者存取 tooonly 索引鍵中，但沒有機密資料的權限。 不過，權限 tooaccess 金鑰或密碼或憑證是在 hello 保存庫層級。 換句話說，金鑰保存庫存取原則不支援物件層級權限。 您可以使用[Azure 入口網站](https://portal.azure.com/)，hello [Azure CLI 工具](../cli-install-nodejs.md)， [PowerShell](/powershell/azureps-cmdlets-docs)，或使用 hello[管理 REST Api 的金鑰保存庫](https://msdn.microsoft.com/library/azure/mt620024.aspx)tooset 存取原則用於金鑰的保存庫。

> [!IMPORTANT]
> 請注意，金鑰保存庫的存取原則會套用在 hello 保存庫層級。 比方說，當使用者被授與權限 toocreate 及 delete 鍵，她可以執行這些作業在所有的索引鍵上該金鑰的保存庫中。
> 
> 

## <a name="example"></a>範例
假設您正在開發的應用程式使用 SSL 憑證、使用 Azure 儲存體來儲存資料，並使用 RSA 2048 位元金鑰來進行簽署作業。 假設此應用程式正在 VM (或 VM 擴展集) 中執行。 您可以使用所有 hello 應用程式密碼，並使用金鑰保存庫 toostore hello 啟動程序使用的憑證是 hello 與 Azure Active Directory 的應用程式 tooauthenticate 金鑰保存庫 toostore。

因此，以下是所有 hello 金鑰和秘密 toobe 儲存在金鑰保存庫中的摘要。

* **SSL 憑證** - 用於 SSL
* **儲存體金鑰**-使用 tooget 存取 tooStorage 帳戶
* **RSA 2048 位元金鑰** - 用於簽署作業
* **啟動程序憑證**-用於 tooauthenticate tooAzure Active Directory、 tooget 存取 tookey 保存庫 toofetch hello 儲存體金鑰和使用 hello RSA 金鑰簽章。

現在讓我們來符合 hello 人管理、 部署和稽核此應用程式。 在此範例中，我們會使用三種角色。

* **安全性小組**-這些通常是從 hello '辦公室的 hello CSO （首席安全性主管）' 的 IT 人員，或對等，負責 hello 的機密資料的適當保管例如 SSL 憑證，用於簽章，連接字串的 RSA 金鑰資料庫儲存體帳戶金鑰。
* **開發人員/operators** -這些是 hello 同仁開發此應用程式，然後再將它部署在 Azure 中。 一般而言，它們不屬於 hello 安全性小組，並因此它們不應該有存取 tooany 敏感性資料，例如 SSL 憑證的 RSA 金鑰，但在部署的 hello 應用程式應該有存取 toothose。
* **稽核員**-這通常是一組不同的人，與 hello 開發人員和一般的 IT 人員隔離。 他們的責任 tooreview 正確使用和維護的憑證、 金鑰等，並確認與資料安全性標準符合。 

一個多個角色的此應用程式，但所述，相關這裡 toobe hello 範圍外而且 hello 訂用帳戶 （或資源群組），也就是系統管理員。 訂用帳戶管理員設定 hello 安全性小組的初始存取權限。 這裡我們假設該 hello 訂用帳戶系統管理員已授與存取 toohello 安全性小組 tooa 資源群組中所有 hello 這個應用程式 reside 所需的資源。

現在我們來看看每個角色在此應用程式的 hello 內容中執行哪些動作。

* **安全性小組**
  * 建立金鑰保存庫
  * 開啟金鑰保存庫記錄
  * 新增金鑰/密碼
  * 建立金鑰備份以用於災害復原
  * 設定金鑰保存庫的存取原則 toogrant 權限 toousers 和應用程式 tooperform 特定作業
  * 定期輪替金鑰/密碼
* **開發人員/操作員**
  * 取得參考 toobootstrap 和 SSL 憑證 （指紋），儲存體金鑰 （密碼 URI） 和簽署金鑰 (金鑰 URI) 從安全性小組
  * 開發和部署以程式設計方式存取金鑰和密碼的應用程式
* **稽核員**
  * 檢閱使用方式記錄 tooconfirm 正確的金鑰/秘密金鑰用法和與資料安全性標準符合

現在讓我們來看看何種存取權限 tookey 保存庫所需的每個角色 （和 hello 應用程式） tooperform 指派的工作。 

| 使用者角色 | 管理平面權限 | 資料平面權限 |
| --- | --- | --- |
| 安全性小組 |金鑰保存庫參與者 |金鑰︰備份、建立、刪除、取得、匯入、列出、還原 <br> 密碼︰全部 |
| 開發人員/操作員 |金鑰保存庫部署權限，以便在部署的 hello Vm 可以從 hello 金鑰保存庫擷取密碼 |None |
| 稽核員 |None |金鑰︰列出<br>密碼︰列出 |
| 應用程式 |None |金鑰︰簽署<br>密碼︰取得 |

> [!NOTE]
> 稽核員需要清單的金鑰和密碼的權限，讓它們可以檢查屬性金鑰和秘密，不會發出 hello 記錄檔、 標記，例如啟動和到期日。
> 
> 

權限 tookey 保存庫，除了這三個角色也需要存取 tooother 資源。 例如，toobe 無法 toodeploy Vm （或 Web 應用程式等）。開發人員/運算子也需要 '參與者' 存取 toothose 資源類型。 稽核員必須 hello 金鑰保存庫的記錄檔的儲存位置的讀取權限 toohello 儲存體帳戶。

Hello 這篇文章的焦點會保護存取 tooyour 金鑰保存庫，因為我們只說明 hello 相關 toothis 主題的相關部分，並略過部署憑證、 存取金鑰和密碼以程式設計方式等詳細資料。這些詳細資料已在其他地方做過說明。 部署憑證儲存在金鑰保存庫 tooVMs 涵蓋[部落格文章](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/)，而且沒有[範例程式碼](https://www.microsoft.com/download/details.aspx?id=45343)可用，說明如何啟動程序 toouse 憑證 tooauthenticate tooAzure AD tooget存取 tookey 保存庫。

大部分的 hello 存取權限可授與使用 Azure 入口網站，但 toogrant 細微權限，您可能需要 toouse Azure PowerShell （或 Azure CLI） tooachieve hello 期望的結果。 

下列 PowerShell 程式碼片段的 hello 假設：

* hello Azure Active Directory 系統管理員建立安全性群組，代表 hello 三個角色，也就是 Contoso 安全性團隊，Contoso 應用程式 Devops，Contoso 應用程式的稽核。 hello 管理員也已加入其所屬使用者 toohello 群組。
* **ContosoAppRG**是 hello 資源群組所有 hello 資源都所在的位置。 **contosologstorage** hello 記錄檔來儲存。 
* 金鑰保存庫**ContosoKeyVault**和用於金鑰保存庫的記錄檔的儲存體帳戶**contosologstorage** hello 必須位於相同的 Azure 位置

第一個 hello 訂用帳戶管理員指派 「 '金鑰保存庫參與者' 和 ' 使用者存取系統管理員 角色 toohello 安全性小組。 這允許 hello 安全性小組 toomanage 存取 tooother 資源，並管理 hello ContosoAppRG 的資源群組中的金鑰保存庫。

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

hello 下列指令碼將說明如何 hello 安全性小組可以建立金鑰保存庫、 設定記錄，及設定其他的角色和 hello 應用程式的存取權限。 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

hello 自訂角色定義，只可指派 toohello 訂用帳戶建立 hello ContosoAppRG 資源群組的位置。 如果 hello 相同的自訂角色會使用其他訂用帳戶中的其他專案，它的範圍可能會有多個加入的訂閱。

hello 「 部署/動作 」 權限的 hello 開發人員/運算子的 hello 自訂角色指派是已設定領域的 toohello 資源群組。 如此一來，只有 hello Vm 會建立 hello 'ContosoAppRG' 會收到 hello 機密資料 （的 SSL 憑證和啟動程序的憑證） 的資源群組中。 開發人員/操作團隊成員會建立其他資源群組中的所有 Vm 不會無法 tooget 這些密碼即使他們知道 hello 密碼 Uri。

此範例描述的是簡單案例。 真實生活案例可能更複雜，而且您可能需要 tooadjust 權限 tooyour 金鑰保存庫根據您的需求。 例如，在本例中，我們假設該安全性小組將會提供 hello 金鑰和秘密參考 （Uri 和指紋） 在其應用程式的開發人員/運算子小組需要 tooreference。 因此，它們不需要開發人員/operators toogrant 平面的任何資料存取。 另請注意，此範例的內容著重在保護金鑰保存庫。 類似考量 toosecure [Vm](https://azure.microsoft.com/services/virtual-machines/security/)，[儲存體帳戶](../storage/common/storage-security-guide.md)和其他 Azure 資源太。

> [!NOTE]
> 注意︰此範例示範生產環境中會如何鎖定金鑰保存庫的存取權。 hello 開發人員應該有自己的訂用帳戶或資源群組具有完整權限 toomanage 其保存庫、 Vm 與儲存體帳戶他們用來開發 hello 應用程式。
> 
> 

## <a name="resources"></a>資源
* [Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)
  
  這篇文章說明 hello Azure Active Directory 角色型存取控制和其運作方式。
* [RBAC：內建角色](../active-directory/role-based-access-built-in-roles.md)
  
  本文詳細說明所有 hello 中 RBAC 中可用的內建角色。
* [了解資源管理員部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)
  
  本文說明 hello 資源管理員部署和傳統部署模型，並說明 hello 優點 hello 資源管理員和資源群組
* [使用 Azure PowerShell 管理角色型存取控制](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  這篇文章說明如何 toomanage 角色型存取控制使用 Azure PowerShell
* [管理角色型存取控制以 hello REST API](../active-directory/role-based-access-control-manage-access-rest.md)
  
  本文將說明如何 toouse hello REST API toomanage RBAC。
* [來自Ignite 且適用於 Microsoft Azure 的角色型存取控制](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  這是連結 tooa 大會 hello 2015 MS Ignite 影片在 Channel 9 上。 在此工作階段，它們討論存取管理和報告功能，在 Azure 中，並瀏覽保護存取 tooAzure 訂用帳戶使用 Azure Active Directory 的最佳作法。
* [授權存取 tooweb 應用程式使用 OAuth 2.0 和 Azure Active Directory](../active-directory/active-directory-protocols-oauth-code.md)
  
  本文說明向 Azure Active Directory 進行驗證的完整 OAuth 2.0 流程。
* [金鑰保存庫管理 REST API](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  這份文件是 hello hello REST Api toomanage 您金鑰保存庫以程式設計的方式，包括設定金鑰保存庫的存取原則。
* [金鑰保存庫 REST API](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  連結 tookey 保存庫 REST API 參考文件。
* [金鑰存取控制](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  連結 tooSecret 存取控制項的參考文件。
* [密碼存取控制](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  連結 tooKey 存取控制項的參考文件。
* 使用 PowerShell [設定](https://msdn.microsoft.com/library/mt603625.aspx)和[移除](https://msdn.microsoft.com/library/mt619427.aspx)金鑰保存庫存取原則
  
  連結的 PowerShell cmdlet toomanage 金鑰保存庫的存取原則的 tooreference 說明文件。

## <a name="next-steps"></a>後續步驟
如需適用於系統管理員的開始使用教學課程，請參閱[開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。

如需金鑰保存庫使用方法記錄的詳細資訊，請參閱 [Azure 金鑰保存庫記錄](key-vault-logging.md)。

如需搭配 Azure 金鑰保存庫使用金鑰和密碼的詳細資訊，請參閱[關於金鑰和密碼](https://msdn.microsoft.com/library/azure/dn903623.aspx)。

如果您有金鑰保存庫相關的問題，請瀏覽 hello [Azure 金鑰保存庫論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

