# Build ruby env by Ansible
- Ansibleによるrails環境の作成

## Description
- CentOSサーバーに対してrails環境を構築する
- ansbile実行環境が必要

## Requirement ｵｽｽﾒ
- vagrant 1.8+
- CentOS  7.1+
- Ansible 2.0+
	- `$ yum install ansible --enablerepo=epel-testing -y`

## Usage
1. ansible実行サーバーと対象サーバーを準備。対象は実行サーバーでもよい
2. 実行サーバーに、本リポジトリをcloneして下記ファイルを変更する
	- praivete.key作成
		- 対象サーバーの秘密鍵を入れる ex./vagrant/.vagrant/machines/default/virtualbox/private_key
	- hosts
		- IPアドレスを対象サーバーに指定する
	- ansible.cfg
		- remote_userを対象サーバのユーザー名に変更
	- group_vars/conf.yml
		- リポジトリ等
3. 実行サーバーにてansibleコマンド実行
	- `$ ansible-playbook web-rails-app.yml`
	- `$ ansible-playbook web-project-conf.yml`
4. failedが出なければ成功。rubyインストールなので結構遅い
5. serverspec当てて動作確認 => https://github.com/qeema/serverspec

## その他
- 疎通の確認がしたい→成功時はponggが返ってくる
	- `$ ansible webserver -m ping`
- playbook実行時のデバッグで詳細が見たい
	- `$ ansible-playbook web-rails-app.yml -vvvv`
