# setup

Digitaloceanに登録しパーソナルアクセストークン、公開鍵を登録しておく
パーソナルアクセストークン作成時、write権限にチェック入れるの忘れずに

Digitaloceanのトークン、鍵IDの設定をpopcorn.tfに書く(set variablesの所)

鍵のIDは以下で確認できる

    curl -X GET "https://api.digitalocean.com/v2/account/keys" \
      -H "Authorization: Bearer $TOKEN"

## create instance

ドロップレットの作成とprovisionが同時に行われる

    $ terraform apply

## provision

2回目以降はansible-playbookコマンドで行う

    $ ansible-playbook -i hosts popcorn.yml --user=root --private-key=~/.ssh/id_rsa

## アクセス

/etc/hostsに以下を追記

    [terraform apply時に得たグローバルIPアドレス] popcorn

ブラウザで確認

    http://popcorn/

ログイン(鍵を登録してある場合パスワード認証はできない)

    $ ssh -i ~/.ssh/id_rsa root@popcorn
