# 社團檔案整理報告 (Club Files Organization Report)

## 一、整理總覽
* **來源資料夾**：`practice/01-club-files/input/`（共 12 個檔案，原檔全數保留未作任何更動）
* **輸出資料夾**：`practice/01-club-files/output/`
* **分類數量**：3 大功能分類資料夾
* **檔案留存規則**：嚴格遵守「不刪除、不覆蓋、原樣保留不同版本與完全相同副本」之原則。

---

## 二、分類架構與對應檔案

### 1. `01-planning-and-proposals/`（企畫與活動方案）
* `proposal_final.txt`：企畫第 1 版（室外活動，30 分鐘）
* `proposal_final2.txt`：企畫第 2 版（室內活動，20 分鐘）
* `meeting_notes.txt`：會議紀錄（下次會議需討論室內或室外方案）
* `rain_plan.txt`：雨天備案（下雨時另議室內方案）
* `next_steps.txt`：後續待辦事項（比較兩個提案，兩者皆未核定）

### 2. `02-logistics-and-budget/`（器材與預算）
* `budget_draft.txt`：紙張預算草案（預估 100 單位，尚未核定）
* `equipment_list.txt`：器材清單（麥克筆 4 支、圖畫紙 2 包）
* `equipment_backup.txt`：器材清單備份（內容與清單相同）

### 3. `03-publicity-and-feedback/`（宣傳與回饋）
* `announcement.txt`：行前通知（提醒自備筆記本，時間地點待定）
* `announcement_copy.txt`：行前通知複本（內容完全相同）
* `poster_text.txt`：宣傳海報文案（一起來做張小卡片）
* `feedback_questions.txt`：活動回饋問卷題目

---

## 三、疑似重複與多版本分析

1. **內容完全相同的檔案（透過 MD5 雜湊驗證）**：
   * `announcement.txt` 與 `announcement_copy.txt`（MD5: `8A382293D766BE1CCC1408F510A2118C`）
   * `equipment_list.txt` 與 `equipment_backup.txt`（MD5: `51C6AE39FA9250CD545E74224041F6F5`）
   * **處理說明**：兩組檔案經字節比對皆 100% 相同，但在整理後各別獨立保留完整複本，不予刪除。

2. **名稱相近但內容不同的版本**：
   * `proposal_final.txt`（長度 132 bytes，MD5: `59D45B7F0664BA8BCB6019B1BC247668`）：規劃為「室外活動 30 分鐘」。
   * `proposal_final2.txt`（長度 131 bytes，MD5: `92FAF7F7813B58D7DB45410CC4397FBE`）：規劃為「室內活動 20 分鐘」。
   * **處理說明**：檔名雖然都包含「final」，但內容為完全不同的活動備案。AI 不擅自依據「final2」或修改時間認定定稿，兩者皆完整保留於企畫分類中。

---

## 四、待確認問題（需人為決策事項）
1. **活動提案尚未定案**：目前同時存在室外版（`proposal_final.txt`）與室內版（`proposal_final2.txt`），依據 `meeting_notes.txt` 與 `next_steps.txt` 紀錄，兩者皆未核定，需由社團下次會議表決。
2. **時間地點尚未確認**：通知檔 `announcement.txt` 載明「時間地點尚未決定」，後續發佈正式通知前須補齊具體時地資訊。
3. **預算尚未核准**：`budget_draft.txt` 載明紙張費用 100 單位為「尚未核定費用」，需送交幹部或學校審核。

---

## 五、實際執行的檢查與限制
* **已完成之檢查**：
  * 比對 `input/` 12 檔與 `output/` 各分類複本之檔案大小與 MD5 雜湊，確認複製過程 100% 完整無誤。
  * 確認 `manifest.json` 涵蓋全部 12 筆來源與目標映射。
  * 確認 `input/` 原始檔案皆完好未損。
* **尚未確認之部分**：
  * 兩個方案最終採用何者、重複的備份檔後續是否由幹部手動清理，留待使用者與社團人工判斷。
