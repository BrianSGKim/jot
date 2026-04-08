# /jot

A [Claude Code](https://claude.ai/claude-code) skill for quick-capturing ideas into scoped scratchpads.

You know the feeling — you're deep in a task and a small idea hits you. Something you want to explore later, a concept worth revisiting, a micro-insight that'll vanish if you don't write it down. So you `/remind` yourself on Slack, scribble in a notebook, or dump it into a messy Notion page. Since Claude Code is already open anyway, `/jot` lets you capture that thought without breaking your flow — and it'll be there when you're ready to dig deeper.

Supports English, Korean, and Japanese.

---

## Install

```bash
curl -o ~/.claude/commands/jot.md https://raw.githubusercontent.com/BrianSGKim/jot/main/jot.md
```

Or manually: copy `jot.md` to `~/.claude/commands/`.

## Setup

```
/jot --setup
```

You'll be asked for your preferred language, scratchpad paths, and optional git repos. Setup also adds a line to `~/.claude/CLAUDE.md` so your ideas are automatically scanned during planning and brainstorming.

## Usage

```
/jot --work <idea>              Save a work idea
/jot --me <idea>                Save a personal idea
/jot --list work                Show recent work ideas
/jot --list me                  Show recent personal ideas
/jot --remove work              Remove a work idea (shows list to pick from)
/jot --remove me                Remove a personal idea
/jot --lang <en|ko|ja>          Change display language
/jot --work --newrepo <url>     Change work git repo
/jot --me --newrepo <url>       Change personal git repo
/jot --setup                    Reconfigure
/jot --help                     Show usage
```

## Examples

```
/jot --work batch API calls to reduce rate limiting
/jot --me check out that ceramics studio in Itaewon
/jot --list work
/jot --remove work
```

## How it works

- Ideas are appended to plain markdown files (`ideas.md`) with timestamps and a project tag from the current working directory
- Two scopes: `--work` and `--me`, each with its own file and optional git repo
- Everything is user-scoped under `~/.claude/` — nothing touches project directories
- Setup adds a line to `~/.claude/CLAUDE.md` so Claude automatically scans your ideas when planning or brainstorming
- Git sync is manual (push when you want)
- All prompts and confirmations appear in your chosen language

## File structure

```
~/.claude/
  CLAUDE.md                # jot scan instruction (added by --setup)
  commands/jot.md          # the skill
  jot-config.json          # paths, repos, language
  jot/work/ideas.md        # work scratchpad
  jot/me/ideas.md          # personal scratchpad
```

## Requirements

- [Claude Code](https://claude.ai/claude-code)

## License

MIT

---

# /jot (한국어)

아이디어를 빠르게 기록하는 [Claude Code](https://claude.ai/claude-code) 스킬입니다.

작업 중에 문득 떠오르는 아이디어가 있잖아요. 나중에 깊게 파고 싶은 컨셉, 잊기 전에 적어둬야 할 마이크로 인사이트. 그래서 Slack에 `/remind`로 남기거나, 공책에 끄적이거나, Notion에 지저분하게 적어두곤 하죠. 어차피 Claude Code가 항상 열려 있으니, `/jot`으로 흐름 끊기지 않고 바로 기록하세요 — 나중에 꺼내볼 준비가 됐을 때 거기 있을 겁니다.

영어, 한국어, 일본어를 지원합니다.

## 설치

```bash
curl -o ~/.claude/commands/jot.md https://raw.githubusercontent.com/BrianSGKim/jot/main/jot.md
```

또는 `jot.md`를 `~/.claude/commands/`에 직접 복사하세요.

## 초기 설정

```
/jot --setup
```

선호 언어, 스크래치패드 경로, git 저장소(선택)를 설정합니다. 설정 시 `~/.claude/CLAUDE.md`에 한 줄이 추가되어, 기획이나 브레인스토밍 시 아이디어가 자동으로 스캔됩니다.

## 사용법

```
/jot --work <아이디어>            업무 아이디어 저장
/jot --me <아이디어>              개인 아이디어 저장
/jot --list work                 최근 업무 아이디어 보기
/jot --list me                   최근 개인 아이디어 보기
/jot --remove work               업무 아이디어 삭제 (목록에서 선택)
/jot --remove me                 개인 아이디어 삭제
/jot --lang <en|ko|ja>           표시 언어 변경
/jot --work --newrepo <url>      업무 git 저장소 변경
/jot --me --newrepo <url>        개인 git 저장소 변경
/jot --setup                     재설정
/jot --help                      사용법 보기
```

## 예시

```
/jot --work API 호출을 배치 처리해서 rate limiting 줄이기
/jot --me 이태원 도자기 공방 가보기
/jot --list work
/jot --remove work
```

## 작동 방식

- 아이디어는 타임스탬프 및 현재 작업 디렉토리의 프로젝트 태그와 함께 마크다운 파일(`ideas.md`)에 추가됩니다
- 두 가지 스코프: `--work`와 `--me`, 각각 별도의 파일과 선택적 git 저장소를 가짐
- 모든 데이터는 `~/.claude/` 아래에 사용자 범위로 저장 — 프로젝트 디렉토리에는 영향 없음
- 설정 시 `~/.claude/CLAUDE.md`에 한 줄이 추가되어, 기획이나 브레인스토밍 시 Claude가 아이디어를 자동으로 스캔합니다
- Git 동기화는 수동 (원할 때 push)
- 모든 안내와 확인 메시지는 설정된 언어로 표시됩니다

## 파일 구조

```
~/.claude/
  CLAUDE.md                # jot 스캔 지시 (--setup으로 추가)
  commands/jot.md          # 스킬 파일
  jot-config.json          # 경로, 저장소, 언어 설정
  jot/work/ideas.md        # 업무 스크래치패드
  jot/me/ideas.md          # 개인 스크래치패드
```

## 요구 사항

- [Claude Code](https://claude.ai/claude-code)

---

# /jot (日本語)

アイデアを素早くメモするための [Claude Code](https://claude.ai/claude-code) スキルです。

作業中にふと浮かぶアイデア、ありますよね。後で深掘りしたいコンセプト、今メモしないと消えてしまうちょっとした気づき。Slackの`/remind`に残したり、ノートに走り書きしたり、Notionに雑に書き留めたり。Claude Codeはどうせ開いているのだから、`/jot`で流れを止めずにサッと記録 — 後で振り返る準備ができた時、ちゃんとそこにあります。

英語・韓国語・日本語に対応しています。

## インストール

```bash
curl -o ~/.claude/commands/jot.md https://raw.githubusercontent.com/BrianSGKim/jot/main/jot.md
```

または `jot.md` を `~/.claude/commands/` に直接コピーしてください。

## 初期設定

```
/jot --setup
```

表示言語、スクラッチパッドのパス、gitリポジトリ（任意）を設定します。セットアップ時に `~/.claude/CLAUDE.md` に一行追加され、企画やブレインストーミング時にアイデアが自動的にスキャンされます。

## 使い方

```
/jot --work <アイデア>            仕事のアイデアを保存
/jot --me <アイデア>              個人のアイデアを保存
/jot --list work                 最近の仕事アイデアを表示
/jot --list me                   最近の個人アイデアを表示
/jot --remove work               仕事のアイデアを削除（一覧から選択）
/jot --remove me                 個人のアイデアを削除
/jot --lang <en|ko|ja>           表示言語を変更
/jot --work --newrepo <url>      仕事用gitリポジトリを変更
/jot --me --newrepo <url>        個人用gitリポジトリを変更
/jot --setup                     再設定
/jot --help                      使い方を表示
```

## 例

```
/jot --work API呼び出しをバッチ処理してrate limitingを減らす
/jot --me 梨泰院の陶芸工房に行ってみる
/jot --list work
/jot --remove work
```

## 仕組み

- アイデアはタイムスタンプと現在の作業ディレクトリのプロジェクトタグ付きでマークダウンファイル（`ideas.md`）に追記されます
- 2つのスコープ：`--work`と`--me`、それぞれ独立したファイルとオプションのgitリポジトリを持ちます
- すべてのデータは`~/.claude/`配下にユーザースコープで保存 — プロジェクトディレクトリには影響しません
- セットアップ時に`~/.claude/CLAUDE.md`に一行追加され、企画やブレインストーミング時にClaudeがアイデアを自動的にスキャンします
- Git同期は手動（バックアップしたい時にpush）
- すべての案内・確認メッセージは設定された言語で表示されます

## ファイル構成

```
~/.claude/
  CLAUDE.md                # jotスキャン指示（--setupで追加）
  commands/jot.md          # スキルファイル
  jot-config.json          # パス、リポジトリ、言語設定
  jot/work/ideas.md        # 仕事用スクラッチパッド
  jot/me/ideas.md          # 個人用スクラッチパッド
```

## 必要なもの

- [Claude Code](https://claude.ai/claude-code)
