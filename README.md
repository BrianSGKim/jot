# /jot

A [Claude Code](https://claude.ai/claude-code) skill for quick-capturing ideas into scoped scratchpads.

Keep a running log of ideas, tidbits, and observations — separated by scope (work vs personal) — with optional git backup.

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

You'll be asked for your preferred language, scratchpad paths, and optional git repos.

## Usage

```
/jot --work <idea>              Save a work idea
/jot --me <idea>                Save a personal idea
/jot --list work                Show recent work ideas
/jot --list me                  Show recent personal ideas
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
/jot --work API 호출을 배치 처리해서 rate limiting 줄이기
/jot --list work
```

## How it works

- Ideas are appended to plain markdown files (`ideas.md`) with timestamps
- Two scopes: `--work` and `--me`, each with its own file and optional git repo
- Everything is user-scoped under `~/.claude/` — nothing touches project directories
- Git sync is manual (push when you want)
- All prompts and confirmations appear in your chosen language

## File structure

```
~/.claude/
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

업무와 개인 영역을 분리하여 아이디어, 메모, 관찰 사항을 기록할 수 있으며, 선택적으로 git 백업을 지원합니다.

## 설치

```bash
curl -o ~/.claude/commands/jot.md https://raw.githubusercontent.com/BrianSGKim/jot/main/jot.md
```

또는 `jot.md`를 `~/.claude/commands/`에 직접 복사하세요.

## 초기 설정

```
/jot --setup
```

선호 언어, 스크래치패드 경로, git 저장소(선택)를 설정합니다.

## 사용법

```
/jot --work <아이디어>            업무 아이디어 저장
/jot --me <아이디어>              개인 아이디어 저장
/jot --list work                 최근 업무 아이디어 보기
/jot --list me                   최근 개인 아이디어 보기
/jot --lang <en|ko|ja>           표시 언어 변경
/jot --setup                     재설정
/jot --help                      사용법 보기
```

## 요구 사항

- [Claude Code](https://claude.ai/claude-code)

---

# /jot (日本語)

アイデアを素早くメモするための [Claude Code](https://claude.ai/claude-code) スキルです。

仕事とプライベートのスコープを分けて、アイデア・気づき・メモを記録できます。オプションでgitバックアップにも対応。

## インストール

```bash
curl -o ~/.claude/commands/jot.md https://raw.githubusercontent.com/BrianSGKim/jot/main/jot.md
```

または `jot.md` を `~/.claude/commands/` に直接コピーしてください。

## 初期設定

```
/jot --setup
```

表示言語、スクラッチパッドのパス、gitリポジトリ（任意）を設定します。

## 使い方

```
/jot --work <アイデア>            仕事のアイデアを保存
/jot --me <アイデア>              個人のアイデアを保存
/jot --list work                 最近の仕事アイデアを表示
/jot --list me                   最近の個人アイデアを表示
/jot --lang <en|ko|ja>           表示言語を変更
/jot --setup                     再設定
/jot --help                      使い方を表示
```

## 必要なもの

- [Claude Code](https://claude.ai/claude-code)
