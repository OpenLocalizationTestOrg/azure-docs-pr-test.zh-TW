建立部署認證以 hello [az webapp 部署使用者集合](/cli/azure/webapp/deployment/user#set)命令。

若為 FTP 和本機 Git 部署 tooa web 應用程式需要部署使用者。 hello 使用者名稱和密碼是帳戶層級。 _它們與您的 Azure 訂用帳戶認證不同。_

下列命令，取代在 hello *\<使用者名稱 >*和*\<密碼 >*與新的使用者名稱和密碼。 hello 使用者名稱必須是唯一的。 hello 密碼必須至少為八個字元，以下列三個元素的 hello 的兩個： 字母、 數字、 符號。 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

如果您收到` 'Conflict'. Details: 409`錯誤，變更 hello 使用者名稱。 如果您收到 ` 'Bad Request'. Details: 400` 錯誤，請使用更強的密碼。

您只需建立此部署使用者一次；可以用於所有 Azure 部署。

> [!NOTE]
> 記錄 hello 使用者名稱和密碼。 您需要它們 toodeploy hello web 應用程式更新版本。
>
>