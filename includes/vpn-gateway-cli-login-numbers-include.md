1. 登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。 如需有關登入的詳細資訊，請參閱[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)。

  ```azurecli
  az login
  ```
2. 如果您有多個 Azure 訂用帳戶，列出 hello 訂閱 hello 帳戶。

  ```azurecli
  az account list --all
  ```
3. 指定您想 toouse hello 訂用帳戶。

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```