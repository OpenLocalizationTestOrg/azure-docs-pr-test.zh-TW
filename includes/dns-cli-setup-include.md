## <a name="set-up-azure-cli-for-azure-dns"></a>設定適用於 Azure DNS 的 Azure CLI

### <a name="before-you-begin"></a>開始之前

確認您擁有 hello 開始您的組態之前，下列項目。

* Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。
* 安裝 hello hello Azure CLI，適用於 Windows、 Linux 或 MAC 最新版本 詳細的資訊將會位於[安裝 hello Azure CLI](../articles/cli-install-nodejs.md)。

### <a name="sign-in-tooyour-azure-account"></a>Azure 帳戶登入 tooyour

開啟主控台視窗，並驗證您的認證。 如需詳細資訊，請參閱[登入從 hello Azure CLI tooAzure](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>切換 CLI 模式

Azure DNS 使用 Azure Resource Manager。 請確定切換 CLI 模式 toouse Azure 資源管理員命令。

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>選取 hello 訂用帳戶

請檢查 hello hello 帳戶的訂用帳戶。

```azurecli
azure account list
```

選擇 Azure 訂用帳戶 toouse。

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>建立資源群組

Azure Resource Manager 需要所有的資源群組指定一個位置。 這當做 hello 預設位置，該資源群組中的資源。 不過，因為所有的 DNS 資源全域，不是地區，hello 所選擇的資源群組位置沒有任何影響 Azure DNS。

如果您使用現有的資源群組，則可略過此步驟。

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>註冊資源提供者

hello Azure DNS 服務是由 hello Microsoft.Network 資源提供者管理。 您的 Azure 訂用帳戶必須是已註冊的 toouse 這個資源提供者才能使用 Azure DNS。 每個訂用帳戶只需執行一次此作業。

```azurecli
azure provider register --namespace Microsoft.Network
```

