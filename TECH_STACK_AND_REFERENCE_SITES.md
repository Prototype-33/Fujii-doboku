# 藤井土木 — 推奨Web / AI / 業務ツール構成
作成日: 2026-09-26

> 原則: 最初から全部入れない。v1は「公式サイト + 問い合わせ + 検索 + 記録」まで。
> 数字が出てから「AI振り分け / パートナーポータル / 課金 / 高度分析」を追加する。

## 1. 最小構成（公開サイト v1）

### UI / Design reference
- Material Design 3
  - コンポーネント、余白、階層、アクセシビリティの参照。
  - Googleっぽい見た目にするためではなく、設計原則の確認用。
- Apple Human Interface Guidelines
  - 情報階層、可読性、インタラクションの参照。
- Lighthouse / PageSpeed Insights
  - パフォーマンス、SEO、アクセシビリティ確認。

### Frontend
- Next.js または静的HTML
- Tailwind CSS
- shadcn/ui（必要な部品だけ）
- GitHub
  - ソース、履歴、ロールバック。

### Hosting
- Vercel
  - Next.jsとの相性が良い。
  - 会社運用ならProを基本候補にする。
- 代替: Cloudflare Pages / Workers
  - 静的サイト中心なら有力。

### Domain / DNS
- Cloudflare Registrar
  - ドメインを原価販売。
  - DNS / SSL / DNSSECと相性が良い。
- ドメイン所有者は必ず会社。
- 制作者個人のアカウントへ永続依存させない。

### Company email
- Google Workspace
  - info@...
  - estimate@...
  - partner@...
  等。
- 普通の社員・取引先メールはResendではなくWorkspaceを使用。

### Search / Local
- Google Business Profile
- Google Search Console
- sitemap.xml
- robots.txt
- Schema.org JSON-LD
- 会社名・住所・電話（NAP）を各媒体で一致させる。

## 2. 問い合わせを取りこぼさない構成

### Transactional email
- Resend
  - Web問い合わせ通知
  - 自動受付メール
  - パートナー通知
  - 見積受付通知

### Spam prevention
- Cloudflare Turnstile
  - 問い合わせフォームのbot対策。

### 初期CRM
最初は作り込まず、
- Google Forms / 独自フォーム
- Google Sheets
で十分。

必須フィールド:
- lead_id
- 日時
- 名前 / 会社
- 電話 / メール
- 住所
- 建物種別
- 希望時期
- 問い合わせ種別
- 紹介元
- 担当者
- 次アクション
- 見積金額
- 受注 / 失注
- 失注理由
- 粗利（後から）
- 再紹介元

## 3. AI intake / CRMへ進む段階

### Database / Backend
- Supabase
  - PostgreSQL
  - Storage
  - Auth
  - Edge Functions
  - Realtime
をまとめて持てる。

v1では不要。
「問い合わせ件数が増えた」「パートナーごとの案件管理が必要」「AI振り分けを入れる」
段階で導入する。

### Authentication
優先順位:
1. ログイン不要なら何も入れない
2. Supabase Auth
3. Clerk

Clerkは認証UXを強くしたいパートナーポータル段階で候補。
SupabaseとClerkを最初から両方入れない。

### AI intake
顧客入力:
- 土地所在地
- 既存建物
- 建替え / 売却 / 活用
- 予算
- 時期
- 希望用途

AI出力:
- 解体候補
- 建築士相談
- 不動産相談
- 施工会社相談
- 資金相談
- 不足情報
- 人間確認が必要な項目

AIは正式見積、法令判断、融資判断、契約判断をしない。

## 4. 分析

### まず入れる
- Google Search Console
- Google Analytics 4

見る:
- 指名検索
- 「江戸川区 解体」等の流入
- 問い合わせ率
- 電話CTA
- 施工実績ページ閲覧
- 法人向けページ閲覧

### プロダクト化後
- PostHog
  - AI intake funnel
  - 途中離脱
  - partner routing
  - feature usage
  - experiment

単純な会社サイトだけならPostHogは不要。

## 5. 課金

### Stripe
追加するタイミング:
- 有料Pre-development相談
- coordination fee
- 月額partner plan
- SaaS化

解体工事代金そのものをWebカード決済するために最初から入れる必要はない。

## 6. 現場 / 社内

### Field management
候補:
- KANNA
- ANDPAD

先に現状ヒアリング:
- LINE中心か
- 紙中心か
- 現場写真がどこにあるか
- 誰が予定を持っているか

システム導入前に現在フローを把握する。

### Accounting
候補:
- freee
- Money Forward Cloud

ただし現在の税理士のシステムを確認。
会計を独自開発しない。

### Documents
- Google Drive
  - 案件単位フォルダ
  - 見積
  - 契約
  - 図面
  - 写真
  - 届出
  - 請求
- 必要になればOCR / AI検索を追加。

### Automation
軽量:
- Google Apps Script
- Make

高度:
- n8n
- Supabase Edge Functions
- Vercel Functions / Cron

最初から複数の自動化基盤を混在させない。

## 7. 監視・品質

- Sentry
  - Web/アプリのエラー監視。
- Uptime monitoring
  - 本格運用後。
- Lighthouse
  - Web品質。
- axe系ツール
  - accessibility。

## 8. 写真 / Content

### 実績写真
- 本物の施工写真を優先。
- AI生成画像を施工実績として表示しない。

必要:
- 解体前
- 養生
- 重機
- 作業員
- 搬出
- 近隣対応
- 完工後
- 打合せ

### CMS
最初はGitHub内Markdownで十分。
スタッフ自身が頻繁に更新したい段階でCMSを検討。

候補:
- Sanity
- microCMS
- Supabaseベースの簡易管理画面

## 9. 推奨構成 — Phase別

### Phase 0: 1週間
GitHub
+ Next.js/静的HTML
+ Vercel
+ Cloudflare Registrar/DNS
+ Google Workspace
+ Google Business Profile
+ Search Console
+ 問い合わせフォーム
+ Resend
+ Turnstile

### Phase 1: 1か月
上記
+ Google Sheets CRM
+ Drive
+ Calendar
+ 見積前フォーム
+ 紹介元管理
+ GA4

### Phase 2: 3〜6か月
上記
+ Supabase
+ AI intake
+ partner DB
+ automated follow-up
+ Sentry
+ PostHog（必要な場合）

### Phase 3: 6〜12か月
上記
+ Partner portal
+ Auth
+ Stripe
+ referral ledger
+ opportunity dashboard
+ project origination engine

## 10. 「入れない」判断も重要

v1では不要:
- Clerk
- Stripe
- PostHog
- 大規模CMS
- 独自会計
- 独自給与
- 独自電子契約
- 複雑なAI agent
- 全国marketplace

理由:
まだlead volumeと顧客行動が分からないため。

## 11. アカウント所有権

会社所有:
- Domain
- DNS
- Vercel/Cloudflare production
- Google Workspace
- Google Business Profile
- Search Console
- Supabase production
- Stripe
- Resend production
- Analytics
- GitHub organization / repository

制作者はAdmin/Editorとして招待。

個人アカウントしか権限を持たない構造は禁止。

## 12. 最初に払う費用の考え方

最小pilot:
- Domain
- Company email
- 必要ならVercel Pro
程度。

Supabase / Resend / Clerk / Turnstile等は低トラフィックなら無料枠から検証可能なものが多い。
ただし本番業務データは、バックアップ・SLA・サポート要件を見て有料化する。

重要なのは月額を0円にすることではなく、
「数千円〜数万円の固定費で、一件の工事・一件の紹介を生む」構造にすること。
