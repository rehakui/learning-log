# 2026-06-15 仮想化環境の確認（VirtualBox / KVM）

## 背景

Mac上のVirtualBoxでAlmaLinuxを動かしている環境で、KVMが利用されているかを確認した。

現在の構成：

```text
Mac（ホストOS）
 └─ VirtualBox
      └─ AlmaLinux（ゲストOS）
```

---

## 仮想化環境の確認

### CPU・仮想化情報の確認

```bash
lscpu
```

結果（一部）

```text
Hypervisor vendor: KVM
Virtualization type: full
```

### 用語

- **Hypervisor vendor** : 仮想マシンを管理しているハイパーバイザー
- **Virtualization type** : 仮想化方式

### 今回の結果

```text
Hypervisor vendor: KVM
```

- KVM系ハイパーバイザーとして認識している

```text
Virtualization type: full
```

- 完全仮想化（Full Virtualization）
- ゲストOSを修正せずに動作させる方式

---

## KVMモジュールの確認

```bash
lsmod | grep kvm
```

結果

```text
（何も表示されない）
```

### 意味

KVMモジュールはロードされていない。

つまり、AlmaLinux内でKVMは動作していない。

---

## 仮想化ソフトの確認

```bash
systemd-detect-virt
```

結果

```text
oracle
```

### 意味

Oracle VirtualBox上で動作していることを示す。

---

## 学んだこと

### 仮想化ソフトと仮想化方式は別

仮想化ソフト

- VirtualBox
- VMware
- KVM
- Hyper-V

仮想化方式

- Full Virtualization（完全仮想化）
- Paravirtualization（準仮想化）

---

### 今回の環境

```text
Mac
 └─ VirtualBox
      └─ AlmaLinux
```

### 結論

- `Virtualization type: full`
  - 完全仮想化で動作している

- `systemd-detect-virt`
  - `oracle`
  - 実際の仮想化ソフトは VirtualBox

- `lsmod | grep kvm`
  - 結果なし
  - AlmaLinux内でKVMモジュールは動作していない

---

## 仮想化環境の確認でよく使うコマンド

```bash
lscpu
systemd-detect-virt
lsmod | grep kvm
```

### 補足

`Hypervisor vendor: KVM` と表示されても、

```bash
lsmod | grep kvm
```

で何も表示されなければ、ゲストOS内でKVMモジュールが動作していることにはならない。

実際にどの仮想化ソフト上で動いているかは、

```bash
systemd-detect-virt
```

でも確認できる。