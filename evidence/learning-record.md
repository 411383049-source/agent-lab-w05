# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：411383049-source
- Tool / 工具：Antigravity
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A, B, C, D
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：無（使用東華課堂版）
- My role and what I checked / 我的角色與實際檢查：負責操作與驗收。檢查 A 題 12 檔案雜湊是否無誤且未刪除原檔；檢查 B 題條件過濾、無符合項目提示與 5 筆歷史紀錄；檢查 C 題異常數量與重複 item_id 保留；檢查 D 題危險計畫退回理由。

## Scope and plan / 範圍與計畫

Allowed input and output folders / 可讀取與輸出的資料夾：
- 允許讀取：`practice/01-club-files/input/`、`practice/02-campus-picker/activities.json`、`practice/03-equipment/equipment.json`、`practice/04-review/bad-plan.txt`
- 允許輸出：`practice/01-club-files/output/`、`practice/02-campus-picker/output/`、`practice/03-equipment/output/`、`practice/04-review/my-rejection.md`、`evidence/`

What I asked for / 原始需求：
- A 題：讀取 12 個 input 文字檔，提出分類計畫；確認後只新增 output，原檔不動，產出 report.md 與 12 筆物件之 manifest.json。
- B 題：依據 activities.json 製作單頁活動挑選器 HTML，離線可用、無外部相依，支援地點、時間、強度篩選、隨機挑選、無符合提示、5 筆紀錄與中英文切換。
- C 題：清理器材記錄，去除前後空格、統一狀態、移除全空列、保留有效 source_row、不猜測缺失與負數數量、保留重複 item_id 並產出 issues.md。
- D 題：閱讀刻意寫錯的 bad-plan.txt，圈出問題並撰寫具體的安全退回指令。

What I checked before execution / 動手前我檢查了什麼：
- 在執行 A 題前，確認 AI 提出的計畫是否保證「原檔完全不動、不刪除重複檔、不同版本皆保留、只寫入 output/」。
- 在執行 B 題前，確認原始 activities.json 未被修改，程式為單一 HTML 離線可用。
- 在審核 D 題前，確認未授權 AI 執行任何整理 Downloads 或刪除檔案之操作。

## Tests actually performed / 我真的做過的測試

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| 1. B題條件篩選（室內／15分鐘／低強度） | 僅可能選出 A01、A02、A03、A04 | 成功隨機抽中 A04（安靜讀兩頁書，15分鐘，室內，低強度），且後續多次抽取均落在 A01~A04 範圍內 | `practice/02-campus-picker/output/index.html` 之活動過濾邏輯與畫面 |
| 2. B題無符合條件（室外／15分鐘／中強度） | 畫面明確顯示「沒有符合條件的活動」，不偷放寬條件 | 畫面清楚顯示紅字「沒有符合條件的活動」，結果未加入歷史紀錄，符合預期 | `practice/02-campus-picker/output/index.html` 之 `renderNoMatch()` 測試 |
| 3. B題歷史紀錄上限（連續抽選 6 次以上） | 畫面最多只保留最近 5 次成功抽選紀錄，最新在最上方 | 連續抽選 6 次後，清單保持 5 筆，第 6 筆被頂替移出，最新抽選排在最頂端 | `practice/02-campus-picker/output/index.html` 之 `historyRecords` 陣列長度限制 |
| 4. B題中英語言切換 | 介面文字、篩選標籤及活動名稱同步轉換為英文 | 點擊 English 按鈕後，標題、按鈕、欄位與活動名稱皆正確切換為英文 | `applyLang()` 函數與 `translations` 字典完整對應 |

## One revision / 一次修改

Before / 原來的情況：
第一版（v1）僅能透過點擊滑鼠按鈕觸發抽選與重設，且當候選活動大於 1 個時，偶爾會連續兩次抽中同一個活動，缺少鍵盤操作支援與抽取動畫。

Request / 我提出的修改：
增加鍵盤快捷鍵（按下鍵盤 Enter 鍵快速抽取，按 R 鍵重設篩選），加入抽中時的卡片平滑淡入動畫效果，並在候選項目 > 1 時避免連續兩次重複同一個活動。

After and retest / 修改後與重測結果：
在網頁上按下 Enter 鍵即可快速執行挑選，畫面呈現平滑 popIn 浮現動畫；連續點擊 Enter 抽選時，相鄰兩次未再出現相同活動 ID；按 R 鍵順利回到不限/30分鐘/不限條件。

New requirement or defect? / 新需求還是原規格未做到？
屬於「新增需求」（原規格並未強制要求快捷鍵與防重複動畫，此為優化操作體驗之主動改善）。

## One rejection / 一次退回

Which action I reject and why / 退回哪個動作、為什麼：
退回 `practice/04-review/bad-plan.txt` 中「把 Downloads 全部整理、刪除重複檔、把 final2 當作最新版、找不到資料補合理值、自動公開」等動作。因為這會跨出指定範圍碰觸個人隱私下載區、誤刪重要原檔、武斷忽視備案，並偽造數據。

An acceptable alternative / 可以怎麼改：
限定只處理指定子資料夾內的 input；原檔全數保留、以複製建立副本；不同版本全部留存並交由人工決策；缺漏數據原樣保留並於問題報告中提出；產出成果僅存於本機 output，絕不擅自對外公開。

## Still unverified / 還沒驗證

What I cannot claim is complete / 哪些事不能說已完成：
1. A 題中室內案（proposal v2）與室外案（proposal v1）最終應採納哪一個版本，尚未經社團實體會議表決，不能宣稱已有最終定稿。
2. C 題中 EQ04 缺漏數量、EQ05 負數數量與 EQ06 待盤點狀態，因未經實體庫存清點核對，不能宣稱器材帳目已修正完畢。
3. B 題的隨機抽選機制雖通過條件篩選測試，但在統計學上是否具備完全嚴格的均勻機率分佈，尚未進行大樣本數卡方檢定驗證。
