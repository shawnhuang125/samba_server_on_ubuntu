# Ubuntu Samba Server 實作指南

以下是在 Ubuntu 上建立 Samba Server 的完整實作指南，適合用於建立區域網路內的檔案共享服務，讓 Windows 或其他裝置可以存取 Ubuntu 主機上的資料夾。

---

## 🔧 一、安裝 Samba Server

```bash
sudo apt update
sudo apt install samba
```

---

## 📁 二、建立共享資料夾

```bash
sudo mkdir -p /srv/samba/share
sudo chown nobody:nogroup /srv/samba/share
sudo chmod 0775 /srv/samba/share
```

---

## ⚙️ 三、編輯 Samba 設定檔

```bash
sudo nano /etc/samba/smb.conf
```

新增以下段落：

```ini
[Share]
   path = /srv/samba/share
   browsable = yes
   read only = no
   guest ok = yes
```

---

## 🔐 四、建立 Samba 使用者（選擇性）

```bash
sudo adduser username
sudo smbpasswd -a username
```

對應的設定範例：

```ini
[PrivateShare]
   path = /srv/samba/private
   valid users = username
   read only = no
```

---

## 🚀 五、重新啟動 Samba 並測試

```bash
sudo systemctl restart smbd
sudo ufw allow 'Samba'
```

---

## 🖥️ 六、從 Windows 存取共享資料夾

在檔案總管網址列輸入：

```
\\<Ubuntu-IP>\Share
```

範例：

```
\\192.168.1.100\Share
```

---

## 🧪 七、測試與除錯指令

```bash
testparm
smbclient -L localhost
smbclient //localhost/Share -U username
```

---

如果你想要設定開機自動掛載、使用者分區、進階權限控制等，也可以進一步擴充。
