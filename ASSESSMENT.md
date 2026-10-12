# 雙人鍵盤對打：實作自評

## 基本資料

- 作者：[陳郁璿]
- 起始版本：[week-05 的 commit hash]
- 完成版本：[本次功能最後一筆 commit hash]

## 我的做法
- 按鍵怎麼分開：[複製 IA_Move和 IA_Attack1，改一下檔案名字。在IMC_Combat把方向鍵從IA_Move刪掉，IA_P2Move裡加上方向鍵，Modifier照抄WASD的設定（↑ Swizzle、↓ Swizzle + Negate、← Negate、→ 不加）。Num7對應到IA_P2Attack這樣 1P 就只剩WASD和 U]
- 2P 怎麼控制角色：[這方面不是很清楚，知道1P的控制是在PlayerController、移動是取相機的Yaw算出Forward／Right向量，再對 CPU 呼叫 Add Movement Input，所以方向才會跟 1P 一樣照畫面決定，其他的部份自己還要再花時間了解。]
- 出拳後怎麼恢復移動：[在Add Movement Input前用Branch分支檢查CPU的 Is Attacking，如果在攻擊時就不移動，所以要接在false那邊。方向鍵按住時Triggered每一幀都會觸發，所以要等到出拳結束後會自動繼續移動。]

## 驗收結果

結果填「通過／未通過／未測試」；觀察欄記錄實際看到的情況。

| 項目 | 結果 | 實際觀察 |
|---|---|---|
| 1. 兩組方向鍵同時操作，移動、繞行、推擠正常 | [通過] | [2PCPU的移動速度比較快一點，移動的距離也更遠] |
| 2. 同時按 U／Num7，兩方同時出拳 | [通過] | [同時出拳，其他的來不及觀察到] |
| 3. 按住 → 再按 Num7，2P 出拳後繼續移動 | [通過] | [一開始按住→再按 Num7，2P會一直向畫面的右方滑動，問了一AI後加了一個branch和判斷是否在攻擊中的boolean值，重新連接過後應該是做出來了] |

## 重要 commit

列出幾筆能看出實作過程的 commit，不必貼完整 git log。

| Commit | 這次完成什麼 |
|---|---|
| [hash] | [加2p的方向鍵和攻擊鍵] |
| [hash] | [2p攻擊] |
| [hash] | [2p可以出拳移動] |
| [hash] | [應該是做好了] |

## 遇到的問題與目前限制

- [自己看不太懂程式碼，所以請AI用Blueprint能做出來的方式一步一步教自己做。因為自己問的問題比較多 分了好幾天才做好]
- [Is Attacking的Target不知道該接哪裡，造成編譯錯誤，接上Get Opponent後解決，應該是要判斷2P的攻擊狀態]