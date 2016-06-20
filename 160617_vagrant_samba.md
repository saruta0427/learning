# VagrantでSELinux状態のsambaアクセスをする

環境
vagrant CentOS 6.5
windows7

## vagrant環境の作成

vagrant環境作成コマンド  
`$ vagrant box add box_name box_path`

インストールできるboxのOS一覧  
http://www.vagrantbox.es/

CentOS 6.5の環境を作る場合のコマンド  
`$ vagrant box add centos65 https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box`

vagrantファイルの作成  
`$ vagrant init`

```
Vagrant.configure(2) do |config|
  config.vm.box = "centos65"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network "public_network"
end
```

上記の行をコメント状態から解除してconfig.vm.boxに先ほど追加したbox名を入れる

仮想サーバー立ち上げ  
`$ vagrant up`

SSH接続  
WindowsならSSHクライアントを使用する  
接続先はVagrant initで作成されたVagrantfileに記載されている  
デフォルトでは192.168.33.10  
user name vagrant  
pass vagrant  

## CentOSでsambaのセットアップ

### vagrantのcentosにログイン後

sambaをインストール  
`$ sudo yum -y install samba`

Linux上のユーザーをsambaに追加しパスワードをセット  
ここではユーザーvagrantを追加  
`$ sudo pdbedit -a vagrant`

ユーザーのパスワードを決定  
`sudo smbpasswd -a vagrant`

次に共有するフォルダを作る  
名前は何でもいい  
`$ mkdir share`

成功したときフォルダ内に何もないと寂しいので適当にファイルを追加  
`$ touch share/success`

次にsambaの設定ファイルを編集する  
`$ sudo vi /etc/samba/smb.conf`

Share Definitionsに以下の記述を追加する  
```
[share]
        path = /home/vagrant/share
        writable = yes
        force user = vagrant
        force group = vagrant
```

ここで共有するディレクトリを定義する

次にworkgroupをコメントアウトするか削除する  
`;      workgroup = MYGROUP`

次のコマンドでsambaを起動させる。  
```
$ sudo /etc/rc.d/init.d/smb start
$ sudo /etc/rc.d/init.d/nmb start
```
### Windowsからsambaアクセス  
Win + R でファイルを開く  
またはエクスプローラーのアドレスを入れる  
`\\192.168.33.10\share`  
サーバーアドレス+登録ディレクトリ名  
[share]という記述がディレクトリ名を定義している  

この段階でsuccessファイルの入ったshareフォルダが開ける

## SELinuxの有効化

`$ sudo vi /etc/selinux/config`
> SELINUX=enforcing

SSHクライアントの接続を切ってvagrantを再起動  
`$ vagrant reload`

再びログインして確認  
`$ getenforce`  
Enforcingと表示されればSELinuxが有効化されている  

次にiptableを起動させる  
`$ sudo /etc/init.d/iptables start`  
するとアクセスできないと注意される  

ホームディレクトリへのアクセスを許可する  
`$ sudo setsebool -P samba_enable_home_dirs 1 `  

これでSELinuxを有効にした状態でsambaアクセスができるようになった
