# Ubuntu Samba Server 實作指南

以下是在 Ubuntu 上建立 Samba Server 的完整實作指南，適合用於建立區域網路內的檔案共享服務，讓 Windows 或其他裝置可以存取 Ubuntu 主機上的資料夾。

---

## 一、安裝 Samba Server

```bash
sudo apt update
sudo apt install samba
```
- 先更新系統套件
- ![image](https://github.com/user-attachments/assets/c752c01f-bc8d-4d1a-87bf-ae528192bc01)
- 安裝samba套件
- ![image](https://github.com/user-attachments/assets/3c365f58-fc23-46b9-a5cf-a1104f8d2fa4)

---

## 二、建立共享資料夾

```bash
sudo mkdir -p /srv/samba/share
sudo chown nobody:nogroup /srv/samba/share
sudo chmod 0775 /srv/samba/share
```
- ![image](https://github.com/user-attachments/assets/353888a0-e361-4b00-96f6-b1120910e7f3)
- ![image](https://github.com/user-attachments/assets/2e623e7b-5225-48f2-add0-01efc5b610c3)

---

## 三、編輯 Samba 設定檔

```bash
sudo nano /etc/samba/smb.conf
```

新增以下段落：

```ini
[Share]
   path = /srv/samba/share
   browsable = yes
   read only = no
   valid users = username
```
- ![image](https://github.com/user-attachments/assets/6c704e3c-fe8c-4e1c-9cef-586987931670)

---

## 四、建立 Samba 使用者（選擇性）

```bash
sudo adduser username
sudo smbpasswd -a username
```
- 建立Samba使用者
- ![image](https://github.com/user-attachments/assets/00a172e8-15a4-4892-97c9-341317016fce)
- 一直按下`ENTER`可略過填入資訊
- ![image](https://github.com/user-attachments/assets/9d8e06e0-b917-4d80-8354-5bd5289a3acd)


對應的設定範例：

```ini
[PrivateShare]
   path = /srv/samba/private
   valid users = username
   read only = no
```
- ![image](https://github.com/user-attachments/assets/281fc071-33c4-4428-b144-6c035e12a3b7)

---

## 五、重新啟動 Samba 

```bash
sudo systemctl restart smbd
sudo ufw allow 'Samba'
```
- ![image](https://github.com/user-attachments/assets/486f59ff-23d4-424d-b00b-a851491f2c05)
---

## 六、從 Windows 存取共享資料夾

在檔案總管網址列輸入：

```
\\<Ubuntu-IP>\Share
```
- ![image](https://github.com/user-attachments/assets/bb601a34-dcd1-4b08-944a-2cfb0c561aa8)
- ![image](https://github.com/user-attachments/assets/0cef9e26-8b21-45fa-9e8a-254051428d21)
- ![image](https://github.com/user-attachments/assets/d81b2fdc-2cd0-4704-9467-3c792a0ede1c)
- ![image](https://github.com/user-attachments/assets/7bf0276b-d964-4765-9c51-060c79852b3c)

---



