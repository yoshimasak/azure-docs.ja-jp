---
title: Azure AD とのパスワード ハッシュ同期とは | Microsoft Docs
description: パスワード ハッシュ同期について説明します。
services: active-directory
author: billmath
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.topic: overview
ms.date: 12/05/2018
ms.subservice: hybrid
ms.author: billmath
ms.collection: M365-identity-device-management
ms.openlocfilehash: 83e172e61411c7c1c098706b5ff4566f565d6bf1
ms.sourcegitcommit: 25a60179840b30706429c397991157f27de9e886
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66253855"
---
# <a name="what-is-password-hash-synchronization-with-azure-ad"></a>Azure AD とのパスワード ハッシュ同期とは
パスワード ハッシュ同期は、ハイブリッド ID を実現するために使用されるサインイン方法の 1 つです。 Azure AD Connect では、オンプレミスの Active Directory インスタンスからクラウドベースの Azure AD インスタンスに、ユーザー パスワードのハッシュを同期します。

パスワード ハッシュ同期は、Azure AD Connect Sync によって実装されるディレクトリ同期の拡張機能です。この機能を使用して、Office 365 などの Azure AD サービスにサインインすることができます。 このサービスにサインインするときに使用するパスワードは、オンプレミスの Active Directory インスタンスにサインインするときに使うものと同じです。

![What is Azure AD Connect](./media/how-to-connect-password-hash-synchronization/arch1.png)

パスワード ハッシュ同期では、ユーザーが覚えておく必要があるパスワードの数を減らして 1 つだけにすることができます。 パスワード ハッシュの同期では次のことが可能です。

* ユーザーの生産性が向上する。
* ヘルプデスクのコストが削減される。  

サインイン方法として [Active Directory フェデレーション サービス (AD FS) とのフェデレーション](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect)を使用する場合、必要に応じて、バックアップとしてパスワード ハッシュ同期を設定することができます。

環境でパスワード ハッシュ同期を使用するには、以下のことを行う必要があります。

* Azure AD Connect をインストールする。  
* オンプレミスの Active Directory インスタンスと Azure Active Directory インスタンスとの間のディレクトリ同期を構成する。
* パスワード ハッシュ同期を有効にする。



詳細については、「[What is hybrid identity?](whatis-hybrid-identity.md)」 (ハイブリッド ID とは) を参照してください。




## <a name="next-steps"></a>次の手順

- [ハイブリッド ID とは](whatis-hybrid-identity.md)
- [Azure AD Connect と Connect Health とは](whatis-azure-ad-connect.md)
- [パススルー認証 (PTA) とは](how-to-connect-pta.md)
- [フェデレーションとは](whatis-fed.md)
- [シングル サインオンとは](how-to-connect-sso.md)
- [パスワード ハッシュ同期のしくみ](how-to-connect-password-hash-synchronization.md)
