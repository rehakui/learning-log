# 2026-06-16 ブートプロセスとsystemd

## プロセス
実行中のプログラムのこと。

## ブートプロセス
Linuxが電源ONから利用可能になるまでの起動手順。

電源ON
↓
BIOS/UEFI
↓
GRUB
↓
Linuxカーネル
↓
systemd
↓
各種サービス起動
↓
ログイン可能

## systemd
Linuxのサービスやシステム全体を管理する仕組み。

主な役割
- サービスの起動・停止
- 起動順序の管理
- システム状態の管理

## 仮想化学習メモ

### KVMとは
Linuxカーネルに組み込まれた仮想化機能。

### KVMを確認するコマンド

```bash
lscpu
systemd-detect-virt
lsmod
cat /proc/cpuinfo
```

### 今回分かったこと

- KVMはCPUの仮想化支援機能（VT-x / VMX など）が必要
- VirtualBox上の仮想マシンではKVMが利用できない場合がある
- 複数のコマンドを使って原因を切り分けられる

### 学習メモ

今の段階なら、

KVMとは何か
↓
KVMを確認するコマンド
↓
なぜ自分の環境では使えないのか

まで理解できていれば十分。

今回、

- lscpu
- systemd-detect-virt
- lsmod
- /proc/cpuinfo
- VT-x（VMX）

を使って原因を切り分けられたのは、講義をただ真似するより学習効果が高かった。