# ブートプロセスとsystemd

## Linux起動の流れ

```text
電源ON
 ↓
BIOS / UEFI
 ↓
GRUB（ブートローダー）
 ↓
Linuxカーネル
 ↓
systemd
 ↓
ログイン・各種サービス起動
```

## systemd

Linux起動後にシステム全体を管理する仕組み。

- サービスの起動・停止
- システムの管理
- ログの管理

などを行う。

## unit

systemdが管理する対象のこと。

例：

- sshd.service
- httpd.service
- network.service