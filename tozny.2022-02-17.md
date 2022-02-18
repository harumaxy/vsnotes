---
tags:
  - tozny
---

# Tozny

オレゴン州ポートランドのスタートアップ企業
SEcurity as a Service
仕事で使ってる認証プラットフォーム
TozID とも呼ばれてる

https://id.tozny.com/<company_id>


Tonzy トンズィー
じゃなくて
Tozny トズニー

# Overview

https://tozny.com/

Encrypted Data Lifecycle Management, Identity & Access Control, and Privileged Access Management Solutions
暗号化されたデータライフサイクル管理、認証とアクセスコントロール、または特権アクセス管理ソリューション

オンプレ、ハイブリッドクラウド、マルチクラウドへの柔軟なセルフホスティング

# TozID

https://tozny.com/tozid/

Tozny が提供しているアクセス制御ツール

# TozStore

https://tozny.com/tozstore

Tozny が提供している、暗号化データベース
`E3DB`という名前らしい
ブラウザ、デバイス、組み込みPCレベルで暗号化したデータを保存する
End to End のセキュリティ

TozID に統合されている


## Zero Knowledge identification

暗号化ベースでゼロナレッジ
というのは、どういうことか

- ユーザー(アプリ)はパスワードで情報を制御できる
- Tozny はパスワードを保存したり、ネットワーク上に送信しない
  - データ共有リスクを軽減

### 仕組み
TozID ツールにおいて
- パスワード = 秘密鍵
  - ユーザー(アプリ)がデータへのアクセスを細かく制御する
    - 特定人物や特定アプリのみに情報ロックを解除
- 要するに、暗号化されたメッセージングアプリ

### 余談
- SSO (シングルサインオン)
- SAML
- OpenID

の標準的なID構造で既存のIDフレームワークに接続できる

# 参考URL

https://techcrunch.com/2020/02/13/tozny-introduces-encrypted-identity-tool-as-part-of-security-service-platform/


