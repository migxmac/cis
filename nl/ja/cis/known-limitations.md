---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 既知の制限事項

 * IBM は Chrome を使用することをお勧めします。

 * Firefox および Safari では、証明書が *アップロードされた* 日付、*変更された* 日付、*期限切れ* 日を表示できません。

 * ページ・ルールの URL 照合を編集すると、そのルールは最も低い優先順位になります。
 
 * ドメインを構成していなくても、**「信頼性」>「グローバル・ロード・バランサー (Global Load Balancers)」**に移動して、ロード・バランサー・プールとヘルス・チェックを作成できます。ただし、**「ロード・バランサーを作成 (Create load balancer)」**を選択し、ロード・バランサーを構成して**「1 リソースをプロビジョニング (Provision 1 Resource)」**をクリックすると、ドメインが必要なため、その要求は拒否されます。この機能の制限により、ユーザーはロード・バランサーの作成フローでプールとモニターの目的を理解できます。
 
 * Early Access プログラムは 1 アカウントにつき 1 インスタンスに制限されています。リソース・インスタンスを作成してドメインを追加すると、CIS の新しいリソース・インスタンスを追加できなくなります。この制限は、試用ドメインを削除してから再び同じリソース・インスタンスにドメインを追加しようとした場合にも適用されます。この操作を行うと、エラーが表示されます。

 * ドメインを追加するときに、現在、IBM のシステムは既存のドメイン・レコードを収集したりインポートしたりしません。

 * この Early Access プログラムの場合、別のプロバイダーで NS レコードを使用するサブドメインの委任だけをサポートしています。CNAME による委任はサポートしていません。
