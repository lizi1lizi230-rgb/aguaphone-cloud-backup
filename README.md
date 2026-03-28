# Aguaphone 雲端備份倉庫

此倉庫用於存放 [Aguaphone](https://github.com/atuolan/aguaphone) 的雲端備份資料。

## 使用方式

### 1. Fork 此倉庫

點擊右上角的 **Fork** 按鈕，將此倉庫複製到你自己的帳號下。

### 2. 建立 Personal Access Token

1. 前往 [GitHub Settings → Developer settings → Fine-grained tokens](https://github.com/settings/tokens?type=beta)
2. 點擊 **Generate new token**
3. 設定：
   - Token name：`aguaphone-backup`（隨意）
   - Expiration：建議選 90 天或更長
   - Repository access：選 **Only select repositories** → 選擇你 fork 的 `aguaphone-cloud-backup`
   - Permissions → Repository permissions：
     - **Contents**：選擇「Read and write」（下拉選單）
4. 點擊 **Generate token**，複製產生的 token（以 `github_pat_` 開頭）

> ⚠️ Token 請妥善保管，不要分享給任何人。

### 3. 在 Aguaphone 中設定

1. 進入 **設定** 頁面
2. 找到 **GitHub 雲端備份** 區塊
3. 填入：
   - 倉庫名稱：`你的用戶名/aguaphone-cloud-backup`
   - Token：貼上剛才複製的 token
4. 點擊 **連接**

### 4. 備份與還原

- 點擊 **上傳備份到 GitHub** 即可備份
- 點擊 **從 GitHub 還原** 可查看並還原歷史備份

## 備份結構

```
backups/
  2026-03-28T12-00-00-000Z/
    manifest.json       ← 分片清單、校驗碼
    part_000.zip        ← 備份分片 0
    part_001.zip        ← 備份分片 1
    ...
```

每次備份會建立一個以時間戳命名的資料夾，內含壓縮分片和清單檔案。

## 注意事項

- 備份資料存放在你自己的 GitHub 私人倉庫中，只有你能存取
- 建議定期清理舊備份，避免倉庫過大
- GitHub 免費帳號的私人倉庫儲存空間上限為 5GB
- 如果備份超過 2GB，系統會自動使用流式上傳模式
