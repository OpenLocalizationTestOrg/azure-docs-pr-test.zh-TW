## <a name="next-steps"></a><span data-ttu-id="02dfc-101">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02dfc-101">Next steps</span></span>

<span data-ttu-id="02dfc-102">啟用 Azure 金鑰保存庫整合之後，您可以在您的 SQL VM 上啟用 SQL Server 加密。</span><span class="sxs-lookup"><span data-stu-id="02dfc-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="02dfc-103">首先，您必須 toocreate 非對稱金鑰在金鑰保存庫和 SQL Server 中的對稱金鑰內 VM 上。</span><span class="sxs-lookup"><span data-stu-id="02dfc-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="02dfc-104">然後，您將無法 tooexecute T-SQL 陳述式 tooenable 加密您的資料庫和備份。</span><span class="sxs-lookup"><span data-stu-id="02dfc-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="02dfc-105">有數種形式的加密可供您利用：</span><span class="sxs-lookup"><span data-stu-id="02dfc-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="02dfc-106">透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="02dfc-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="02dfc-107">加密的備份</span><span class="sxs-lookup"><span data-stu-id="02dfc-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="02dfc-108">資料行層級加密 (CLE)</span><span class="sxs-lookup"><span data-stu-id="02dfc-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="02dfc-109">hello 下列 TRANSACT-SQL 指令碼提供範例的每個區域。</span><span class="sxs-lookup"><span data-stu-id="02dfc-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="02dfc-110">範例的必要條件</span><span class="sxs-lookup"><span data-stu-id="02dfc-110">Prerequisites for examples</span></span>

<span data-ttu-id="02dfc-111">每個範例根據 hello 兩個必要條件： 從金鑰保存庫非對稱金鑰稱為**CONTOSO_KEY**呼叫 hello AKV 整合功能所建立的認證和**Azure_EKM_TDE_cred**。</span><span class="sxs-lookup"><span data-stu-id="02dfc-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="02dfc-112">hello 下列 TRANSACT-SQL 命令設定執行 hello 範例這些必要條件。</span><span class="sxs-lookup"><span data-stu-id="02dfc-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="02dfc-113">透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="02dfc-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="02dfc-114">建立 SQL Server 登入 toobe hello Database Engine 用於 TDE，然後加入 hello 認證 tooit。</span><span class="sxs-lookup"><span data-stu-id="02dfc-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="02dfc-115">建立要用於 TDE 的 hello 資料庫加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="02dfc-115">Create hello database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="02dfc-116">加密的備份</span><span class="sxs-lookup"><span data-stu-id="02dfc-116">Encrypted backups</span></span>

1. <span data-ttu-id="02dfc-117">建立 hello 資料庫引擎用於加密備份所使用的 SQL Server 登入 toobe 並加入 hello 認證 tooit。</span><span class="sxs-lookup"><span data-stu-id="02dfc-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="02dfc-118">使用 hello hello 金鑰保存庫中儲存的非對稱金鑰指定加密並備份 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="02dfc-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="02dfc-119">資料行層級加密 (CLE)</span><span class="sxs-lookup"><span data-stu-id="02dfc-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="02dfc-120">此指令碼會建立 hello hello 金鑰保存庫中的非對稱金鑰來保護對稱金鑰，然後再使用 hello 資料庫中的 hello 對稱金鑰 tooencrypt 資料。</span><span class="sxs-lookup"><span data-stu-id="02dfc-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="02dfc-121">其他資源</span><span class="sxs-lookup"><span data-stu-id="02dfc-121">Additional resources</span></span>

<span data-ttu-id="02dfc-122">如需有關如何 toouse 這些加密功能，請參閱[使用 EKM 的 SQL Server 加密功能](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM)。</span><span class="sxs-lookup"><span data-stu-id="02dfc-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="02dfc-123">請注意，本文章中的 hello 步驟假設您已經有 Azure 虛擬機器上執行的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="02dfc-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="02dfc-124">如果沒有，請參閱[在 Azure 中佈建 SQL Server 虛擬機器](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="02dfc-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="02dfc-125">如需在 Azure VM 中執行 SQL Server 的其他指引，請參閱[Azure 虛擬機器上的 SQL Server 概觀](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="02dfc-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
