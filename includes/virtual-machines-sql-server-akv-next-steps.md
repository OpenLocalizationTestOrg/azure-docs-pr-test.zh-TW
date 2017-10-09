## <a name="next-steps"></a>後續步驟

啟用 Azure 金鑰保存庫整合之後，您可以在您的 SQL VM 上啟用 SQL Server 加密。 首先，您必須 toocreate 非對稱金鑰在金鑰保存庫和 SQL Server 中的對稱金鑰內 VM 上。 然後，您將無法 tooexecute T-SQL 陳述式 tooenable 加密您的資料庫和備份。

有數種形式的加密可供您利用：

* [透明資料加密 (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [加密的備份](https://msdn.microsoft.com/library/dn449489.aspx)
* [資料行層級加密 (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

hello 下列 TRANSACT-SQL 指令碼提供範例的每個區域。

### <a name="prerequisites-for-examples"></a>範例的必要條件

每個範例根據 hello 兩個必要條件： 從金鑰保存庫非對稱金鑰稱為**CONTOSO_KEY**呼叫 hello AKV 整合功能所建立的認證和**Azure_EKM_TDE_cred**。 hello 下列 TRANSACT-SQL 命令設定執行 hello 範例這些必要條件。

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

### <a name="transparent-data-encryption-tde"></a>透明資料加密 (TDE)

1. 建立 SQL Server 登入 toobe hello Database Engine 用於 TDE，然後加入 hello 認證 tooit。

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

1. 建立要用於 TDE 的 hello 資料庫加密金鑰。

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

### <a name="encrypted-backups"></a>加密的備份

1. 建立 hello 資料庫引擎用於加密備份所使用的 SQL Server 登入 toobe 並加入 hello 認證 tooit。

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

1. 使用 hello hello 金鑰保存庫中儲存的非對稱金鑰指定加密並備份 hello 資料庫。

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>資料行層級加密 (CLE)

此指令碼會建立 hello hello 金鑰保存庫中的非對稱金鑰來保護對稱金鑰，然後再使用 hello 資料庫中的 hello 對稱金鑰 tooencrypt 資料。

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

## <a name="additional-resources"></a>其他資源

如需有關如何 toouse 這些加密功能，請參閱[使用 EKM 的 SQL Server 加密功能](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM)。

請注意，本文章中的 hello 步驟假設您已經有 Azure 虛擬機器上執行的 SQL Server。 如果沒有，請參閱[在 Azure 中佈建 SQL Server 虛擬機器](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md)。 如需在 Azure VM 中執行 SQL Server 的其他指引，請參閱[Azure 虛擬機器上的 SQL Server 概觀](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)。
