# Build ruby env by Ansible
Ansibleによるrails環境の作成-

## Description
- CentOSサーバーに対してrails環境を構築する
- ansbile実行環境が必要

## Requirement
- CentOS  7.1+
- Ansible 2.0+
-- yum install ansible --enablerepo=epel-testing -y

## Usage
1. ansible実行サーバーと対象サーバー二台を準備(以下virtualbox+vagrantを想定)
2. 実行サーバーより、本リポジトリをcloneして下記ファイルを変更する
- praivete.key
-- ansible対象のサーバーの鍵に変更 ex./vagrant/.vagrant/machines/default/virtualbox/private_key
- hosts
-- ansible_ssh_hostをansible当てたいサーバーのIPアドレスに指定する
- ansible.cfg
-- remote_userを対象サーバのユーザー名に変更(デフォルトはvagrant)
- web-rails-app.yml
-- varsのproject_dir => ローカルのrailsプロジェクトディレクトリ
3. 実行サーバーにてansibleコマンド実行
`$ ansible-playbook web-rails-app.yml`
4. failedが出なければ完成。rubyインストールなので結構遅い

## その他
- 疎通の確認がしたい→成功時はponggが返ってくる
`$ ansible webserver -m ping`
- playbook実行時のデバッグで詳細が見たい
`$ ansible-playbook web-rails-app.yml -vvvv`
