---
title: レジストリ認証オプション
description: Azure Active Directory ID でのサインイン、サービス プリンシパルの使用、オプションの管理者資格情報の使用など、Azure コンテナー レジストリのための認証オプション。
ms.topic: article
ms.date: 12/21/2018
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fbe77dee4104e3c654aad58db82765733b2c3e1d
ms.sourcegitcommit: 2a2af81e79a47510e7dea2efb9a8efb616da41f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76264511"
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>プライベート Docker コンテナー レジストリによる認証

Azure コンテナー レジストリでの認証には複数の方法があり、それぞれ 1 つ以上のレジストリ使用シナリオに適用できます。

[個々のログイン](#individual-login-with-azure-ad)によって直接レジストリに対して認証を受けるなどの方法が推奨されます。またはアプリケーションやコンテナー オーケストレーターで Azure Active Directory (Azure AD) [サービス プリンシパル](#service-principal)を使用して無人 ("ヘッドレス") 認証を実行することができます。

## <a name="individual-login-with-azure-ad"></a>Azure AD での個々のログイン

開発ワークステーションとの間でのイメージのプッシュやプルなど、レジストリを直接操作するときは、[Azure CLI](/cli/azure/install-azure-cli) で [az acr login](/cli/azure/acr?view=azure-cli-latest#az-acr-login) コマンドを使用して認証します。

```azurecli
az acr login --name <acrName>
```

`az acr login` を使用してログインすると、CLI では [az login](/cli/azure/reference-index#az-login) の実行時に作成されたトークンを使用して、レジストリとのセッションがシームレスに認証されます。 この方法でログインすると、資格情報がキャッシュされるので、セッションの以降の `docker` コマンドではユーザー名やパスワードが不要になります。 

レジストリのアクセスでは、`az acr login` で使用されるトークンは **3 時間**有効なため、`docker` コマンドを実行する前に常にレジストリにログインすることをお勧めします。 トークンの有効期限が切れた場合は、`az acr login` コマンドを再度使用して再認証することで、トークンを更新できます。 

Azure ID で `az acr login` を使用すると、[ロールベースのアクセス](../role-based-access-control/role-assignments-portal.md)が可能になります。 Azure AD の自分個人の ID でレジストリにログインすることが推奨されるシナリオもあります。 サービス間のシナリオの場合や、個々のアクセスの管理は行わないワークグループのニーズを処理する場合は、[Azure リソース用のマネージド ID](container-registry-authentication-managed-identity.md) でログインすることもできます。

## <a name="service-principal"></a>サービス プリンシパル

[サービス プリンシパル](../active-directory/develop/app-objects-and-service-principals.md)をレジストリに割り当てた場合、アプリケーションやサービスではヘッドレス認証にそれを使用できます。 サービス プリンシパルを使用すると、レジストリへの[ロールベースのアクセス](../role-based-access-control/role-assignments-portal.md)が可能になります。1 つのレジストリに複数のサービス プリンシパルを割り当てることができます。 複数のサービス プリンシパルを割り当てることで、アプリケーションごとに異なるアクセスを定義できます。

コンテナー レジストリでは次のロールを使用できます。

* **AcrPull**: プル

* **AcrPush**: プルとプッシュ

* **所有者**: プル、プッシュ、他のユーザーへのロールの割り当て

ロールの完全な一覧については、「[Azure Container Registry のロールとアクセス許可](container-registry-roles.md)」をご覧ください。

Azure コンテナー レジストリを使用した認証のためのサービス プリンシパルを作成する CLI スクリプトと、サービス プリンシパルの使用に関するガイダンスについては、「[サービス プリンシパルによる Azure Container Registry 認証](container-registry-auth-service-principal.md)」を参照してください。

## <a name="admin-account"></a>管理者アカウント

各コンテナー レジストリには管理者ユーザー アカウントが含まれており、このアカウントは既定で無効になっています。 Azure portal で、または Azure CLI や他の Azure ツールを使用して、管理者ユーザーを有効にし、その資格情報を管理できます。

> [!IMPORTANT]
> 管理者アカウントは、主にテストのために、1 人のユーザーがレジストリにアクセスすることを目的としています。 管理者アカウントの資格情報を複数のユーザーで共有しないことをお勧めします。 管理者アカウントで認証するすべてのユーザーが、レジストリへのプル/プッシュアクセス権を持つ 1 人のユーザーとして表示されます。 このアカウントを変更したり、無効にしたりすると、その資格情報を使用するすべてのユーザーのレジストリ アクセスが無効になります。 ユーザーおよびヘッドレス シナリオ用のサービス プリンシパルには、個人 ID を使用することをお勧めします。
>

管理者アカウントには、再生成できる 2 つのパスワードを指定します。 2 つのパスワードにより、一方のパスワードを再生成している間に、もう一方のパスワードを使用してレジストリへの接続を維持できます。 管理者アカウントが有効になっている場合は、レジストリに対する基本認証についてのメッセージが表示されたら、ユーザー名とどちらかのパスワードを `docker login` コマンドに渡すことができます。 次に例を示します。

```
docker login myregistry.azurecr.io 
```

ログイン資格情報の管理のベスト プラクティスについては、[docker login](https://docs.docker.com/engine/reference/commandline/login/) コマンドのリファレンスを参照してください。

既存のレジストリの管理者ユーザーを有効にするには、Azure CLI で [az acr update](/cli/azure/acr?view=azure-cli-latest#az-acr-update) コマンドの `--admin-enabled` パラメーターを使用します。

```azurecli
az acr update -n <acrName> --admin-enabled true
```

Azure Portal で管理者ユーザーを有効にするには、レジストリに移動し、 **[設定]** の **[アクセス キー]** を選択して、 **[管理者ユーザー]** の **[有効にする]** を選択します。

![Azure Portal の管理者ユーザーを有効にする UI][auth-portal-01]

## <a name="next-steps"></a>次のステップ

* [Azure CLI を使用した最初のイメージのプッシュ](container-registry-get-started-azure-cli.md)

<!-- IMAGES -->
[auth-portal-01]: ./media/container-registry-authentication/auth-portal-01.png
