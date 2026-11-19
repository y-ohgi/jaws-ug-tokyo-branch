# connpass ページの作り方・直し方

ランチタイムLT会の説明欄・参加者への情報は、AI に頼むだけで作れます。
使える AI に合わせて、次の3つのどれかで進めてください。

| 使える AI | やり方 |
|---|---|
| コーディングエージェント（Claude Code・Codex・Kiro など）でこのリポジトリを開ける | 人に頼むのと同じ言葉で頼むだけ。エージェントが [スキル](../.claude/skills/connpass-lunch-lt/SKILL.md) と [雛形](./lunch-lt/template/) を読んで作ります |
| ブラウザを操作できる AI（Claude in Chrome など）だけ | 前回の connpass の URL を渡して「これと同じ見た目で◯◯して」と頼む |
| チャットの AI（無料の ChatGPT など）だけ | [ChatGPT などで作るとき](./lunch-lt/chatgpt-prompt.md) のプロンプトと雛形を貼り、返ってきた HTML を connpass に貼る |

## 頼み方の例

> #41 の 12:25〜12:35 の枠を、ますのさんの「◯◯」に差し替えて、connpass にも反映して

> #42 に LT 枠を1つ足して。12:50〜13:00、登壇者は TBD で

> 次の #43 のページを作って。通常回で LT は4本

ブラウザを操作できる AI なら、connpass の URL（編集画面か公開ページ）も一緒に渡します。
東京支部の運営は全員 connpass の管理者なので、AI は前回の編集画面から説明欄の HTML をそのまま読めます。

## 置いてあるもの

- `lunch-lt/template/`：説明欄（通常回・支部コラボ会）と参加者への情報の雛形。今の見た目そのままで、回ごとに埋める所を伏せ字にしてあります
- `../.claude/skills/connpass-lunch-lt/SKILL.md`：エージェント向けの説明。説明欄の組み立て、見た目の決まり、connpass の癖
- `lunch-lt/chatgpt-prompt.md`：チャットの AI に貼るプロンプト

このリポジトリは公開されています。参加者だけに見せる URL（配信・アンケート）と、公開前の回の中身は書かないでください。
