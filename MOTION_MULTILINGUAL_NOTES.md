# Motion / Multilingual Prototype v6

## 動き
- CSS: moving perspective grid / orbit / route dot
- JS: IntersectionObserverによるscroll reveal
- JS: JP / 中文の簡易language switch
- prefers-reduced-motion対応
- JavaではなくJavaScript。v1の動きは依存ライブラリなしのvanilla JSで十分。

## 「機能未完成でも動く」デモ
建替え相談 → AI整理 → 専門家接続 → 解体 → 次の建築
のpipelineをprototypeとして視覚化。
Backend/Supabaseなしでも「こう動く予定」を見せられる。

## 画像
現在は意図的に抽象placeholder。
正式版:
1. 本物の施工写真
2. ライセンス済みブランド写真
3. AI生成のブランド/コンセプト画像
のいずれかへ差し替える。

AI生成画像を「施工実績」と誤認させない。
AI / stock / conceptの場合は必要に応じてcaptionや配置で実績写真と分離する。

## 中国語
初期は完全翻訳サイトを作らず、
- 中文相談入口
- 中国語での初期ヒアリング
- partner routing
からpilot。

SEO / 実運用で需要が確認できたら `/zh/` の独立ページへ。
client-side language toggleだけでは中国語SEOには弱いので、本番ではURLを分ける。
