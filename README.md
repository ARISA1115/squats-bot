# workout-reminder-bot

ワークアウトチャレンジのリマインダーをSlackに自動送信するボットです。

## 概要

平日の決まった時間にSlackにワークアウトチャレンジのメッセージを自動送信します。GitHub Actionsで実行されます。

## 機能

- 平日の1時間ごと（9:00-18:00）に自動でSlackに通知
- スクワット、ランジ、プランクの3つの種目からランダムに1つを選んで通知
  - スクワット: 10回（通常）、15回（10%の確率で増量版）
  - ランジ: 10回（通常）、15回（10%の確率で増量版）
  - プランク: 30秒（通常）、45秒（10%の確率で増量版）
- GitHub Actionsで自動実行

## セットアップ

### 1. リポジトリのクローン

```bash
git clone <repository-url>
cd workout-reminder-bot
```

### 2. 環境変数の設定

`.env`ファイルを作成し、SlackのWebhook URLを設定します：

```bash
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### 3. 実行方法

1. GitHubリポジトリのSettings > Secrets and variables > Actionsに移動
2. `SLACK_WEBHOOK_URL`という名前でシークレットを追加
3. ワークフローが自動的にスケジュール実行されます

手動実行する場合は、GitHub Actionsのワークフローから「Run workflow」を選択してください。

## 実行スケジュール

### GitHub Actions

**平日（月〜金）の1時間ごと：**
- **JST 09:00, 10:00, 11:00, 12:00, 13:00, 14:00, 15:00, 16:00, 17:00, 18:00**
- 遅延を考慮して、各時刻の5分前にスケジュール設定されています

1日10回の通知が送信されます。

## ファイル構成

```
workout-reminder-bot/
├── .github/
│   └── workflows/
│       └── workout.yaml    # GitHub Actionsワークフロー
├── .gitignore              # Git除外設定
└── README.md
```

## 手動実行

GitHub Actionsのワークフローから「Run workflow」を選択して手動実行できます。

## 注意事項

- **GitHub Actionsのcronスケジュールには遅延が発生する可能性があります**（最大1時間程度）
  - 指定時刻（例：10:00）から数分〜数十分遅れて通知が届く場合があります
  - これはGitHub Actionsの制限であり、完全に正確な時刻実行は保証されません
  - 遅延を考慮して、各時刻の5分前にスケジュール設定されています