---
name: jawsug-slack-post
description: JAWS-UG の運営 Slack（make-jawsug）のチャンネルや DM を、ブラウザを操作できる AI（Claude in Chrome など）で読む・投稿する。「Slack のこのスレ読んで」「#jawsug_tokyo_lunch に投稿して」「◯◯さんにメンションして返信して」と頼まれたときに使う。
---

# JAWS-UG 運営 Slack へブラウザから投稿する

JAWS-UG の運営 Slack は、AI のコネクタからは読み書きできない。
ブラウザで Slack を開き、頼んだ人のログインのまま操作する。

## 開き方

- `https://make-jawsug.slack.com/archives/<チャンネルID>/p...` のリンクは、開くとデスクトップアプリへ飛ばされ、ブラウザでは読めない
- `archives` を `messages` に替えて `https://make-jawsug.slack.com/messages/<チャンネルID>/p...` で開くと、ブラウザの Slack（`app.slack.com/client/...`）でそのチャンネルが開く（スレッドまでは開かないので、目当ての投稿を探して開く）
- 読むだけなら、開いたあとページの文字を取り出せば足りる。スレッドは「◯件の返信」を押して開く

## 投稿の手順

**キーボードの入力（文字を打つ・Enter・Tab）で書かない。** Slack の入力欄では Enter が送信になる。メンションの候補を Tab で確定したときに、そこまでの文が先に送信されたこともある。
文字はページの中で JavaScript から入れ、送信ボタンだけを最後にクリックする。

1. 入力欄を1回クリックする（ここだけは本物のクリック）
2. 文字を入れる

   ```js
   document.execCommand('insertText', false, '1行目の文')
   document.execCommand('insertParagraph')        // 改行（空行は2回）
   document.execCommand('insertText', false, '2行目の文')
   ```

3. メンションは、`@名前の一部` を入れて候補を出し、目当ての候補をクリックする

   ```js
   document.execCommand('insertText', false, '@ますの/t')
   // 1〜2秒待ってから
   const o = [...document.querySelectorAll('[role=listbox] [role=option]')]
     .find(x => x.innerText.startsWith('ますの'))
   for (const t of ['mousedown', 'mouseup', 'click']) o.dispatchEvent(new MouseEvent(t, { bubbles: true }))
   ```

   - 候補を選ぶと、名前の後ろに空白が1つ自動で入る。続きの文の頭に空白を足さない
   - 表示名は「名前/ID[支部]」の形が多い。日本語の名前で候補が出ないときは、ローマ字の ID で探す
4. 入力欄の全文を読み直し、頼んだ人に見せた文面と一致するか確かめる

   ```js
   document.querySelector('[data-qa="message_input"] .ql-editor').innerText
   ```

5. 送信ボタン（紙飛行機）をクリックする
6. 投稿されたメッセージを画面で見て、1つの投稿に収まっているかを確かめる

途中でやめるときは、入力欄を空にしておく（`selectAll` → `delete`）。下書きが頼んだ人の Slack に残るため。

## 文面の決まり

- 投稿する前に、全文を頼んだ人に見せて「送って」をもらう
- AI が代わりに書いた投稿は、冒頭で「こんにちは、Claude Codeです。◯◯に代わりご連絡します。」のように名乗る（◯◯は、運営メンバーの間で通っている呼び名）
- チャンネルへ流すかスレッドへ返すかは、頼んだ人の指定に従う。指定が無ければ聞く
- 投稿を直すときは、メッセージの「その他」から「メッセージを編集する」で直す。直した投稿には「（編集済み）」が付く
