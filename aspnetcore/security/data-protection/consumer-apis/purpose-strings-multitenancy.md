---
title: 目的の階層と ASP.NET Core におけるマルチ テナント機能
author: rick-anderson
description: ASP.NET Core データ保護 Api に関連する、目的の文字列の階層とマルチ テナント機能について説明します。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/consumer-apis/purpose-strings-multitenancy
ms.openlocfilehash: a1ca2c32f95a86b877cbbe94d106d23b86800443
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="purpose-hierarchy-and-multi-tenancy-in-aspnet-core"></a>目的の階層と ASP.NET Core におけるマルチ テナント機能

以降、`IDataProtector`は暗黙的にも、`IDataProtectionProvider`目的を連結することができます。 この意味で`provider.CreateProtector([ "purpose1", "purpose2" ])`は等価`provider.CreateProtector("purpose1").CreateProtector("purpose2")`です。

これにより、データ保護システムを通じていくつか興味深い階層リレーションシップです。 先ほどの例の[Contoso.Messaging.SecureMessage](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-contoso-purpose)、SecureMessage コンポーネントを呼び出すことができます`provider.CreateProtector("Contoso.Messaging.SecureMessage")`1 回に必要な先行プライベートに結果をキャッシュし、`_myProvide`フィールドです。 呼び出しを使用して、将来の保護機能を作成し、できます`_myProvider.CreateProtector("User: username")`、個々 のメッセージをセキュリティで保護するこれらの保護機能に使用されるとします。

これを反転もできます。 独自の認証および状態管理システム (CMS 必然的に) 複数のテナント、および各テナントを構成できますホストの 1 つの論理アプリケーションを検討してください。 包括的なアプリケーションが 1 つのマスター プロバイダー、および呼び出し`provider.CreateProtector("Tenant 1")`と`provider.CreateProtector("Tenant 2")`に、データ保護システムの分離された独自スライスを各テナントに付与します。 テナントは独自のニーズに基づく独自個々 の保護機能を派生し、でしたとどの程度厳密に関係なく、作成はできません衝突の保護機能、他のテナントでシステムで。 視覚的に、これは次のようです。

![マルチ テナント機能の目的](purpose-strings-multitenancy/_static/purposes-multi-tenancy.png)

>[!WARNING]
> 包括的なアプリケーションを制御する Api は、個々 のテナントを使用し、テナントが、サーバー上の任意のコードを実行できないことを前提です。 テナントが任意のコードを実行できる、分離の保証を中断するプライベート リフレクションを実行する可能性がありますかマスター_キー生成情報を直接読み取るし、どのようなサブキーを派生する可能性がありますがだけ状況が該当します。

データ保護システムは、既定の既定の構成におけるマルチ テナント機能の並べ替えを実際に使用します。 既定では、マスター_キー生成情報は、ワーカー プロセス アカウントのユーザー プロファイル フォルダー (または IIS アプリケーション プール id のレジストリ、) に格納されます。 実際には、単一のアカウントを使用して、複数のアプリケーションを実行する非常に一般的なマスター_キー生成情報の共有をこれらすべてのアプリケーションが終了するため。 これを解決するには、データ保護システムは、全体的な目的のチェーンの最初の要素としてごとのアプリケーション固有の識別子を自動的に挿入されます。 この暗黙的な目的の機能を[個々 のアプリケーションの分離](xref:security/data-protection/configuration/overview#per-application-isolation)上の図と同じで、システム、および保護機能の作成プロセス内で一意のテナントとして各アプリケーションを効果的に扱うことで別のです。
