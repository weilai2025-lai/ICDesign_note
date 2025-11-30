# IC Design 面試準備筆記

## 1. Static Timing Analysis (STA) & Timing Closure (最核心)

履歷強調了在 NPU 專案中達到了 "Aggressive timing closure"，這類問題是面試官最愛問的。

### Setup / Hold Time 基礎

- **寫出 Setup 與 Hold time 的計算公式與 violation 判斷條件**
  
- **情境題：如果發生 Setup violation 該怎麼修？**
  - Upsize cell
  - Buffer insertion
  - Reduce logic depth 等

- **情境題：如果發生 Hold violation 該怎麼修？**
  - Add delay buffers

- **Setup 和 Hold 哪一個比較 critical？**
  - 為什麼 Setup 常用 Slow corner 檢查，而 Hold 常用 Fast corner？

### Skew & Jitter

- **解釋 Clock Skew, Jitter 與 Uncertainty 的差異**

- **什麼是 Useful Skew？如何利用它來幫助 Timing？**

### Clock 相關

- **為什麼要在 Clock path 上加 Buffer 而不是直接拉線？**
  - 控制 Slew
  - 控制 Skew
  - 控制 RC delay

- **什麼是 Clock Reconvergence Pessimism (CRPR/CPPR)？**

---

## 2. ASIC Design Flow & Backend (NPU 專案強項)

使用過 Innovus 跑過 Floorplan 到 Routing，需要能解釋每一個步驟的細節。

### Flow 總覽

- **請描述完整的 ASIC Design Flow（從 RTL 到 GDSII）**

- **Signoff 階段在做什麼？**
  - DRC (Design Rule Check)
  - LVS (Layout Versus Schematic)
  - IR/EM (IR Drop / Electromigration)
  - Signal Integrity

### Floorplan & Placement

- **Macro Placement 的策略是什麼？**
  - 把大顆的放在邊緣或靠近相關 I/O
  - 預留通道

- **什麼是 Congestion？**
  - 造成的原因有哪些？（Pin density, bad floorplan）
  - 如何解決？

### Clock Tree Synthesis (CTS)

- **CTS 的目標是什麼？**
  - Minimize Skew
  - Minimize Insertion Delay

### DRC / LVS / Reliability

- **你遇過哪些 DRC issue？如何解決？**
  - Spacing
  - Width
  - Antenna

- **什麼是 Antenna Effect？它是如何形成的？**
  - 電漿蝕刻導致電荷累積打穿 Gate Oxide

- **什麼是 Electromigration (EM)？如何預防？**
  - 加寬金屬線
  - 增加 Vias

---

## 3. Digital Logic & Circuits (基礎但必考)

測試對數位電路底層的理解，這是所有 IC Design 的基礎。

### 基本元件

- **Flip-Flop vs Latch 的差別？**

- **SRAM vs DRAM vs Register File 的差別與應用場景？**

- **畫出 NAND 和 NOR 的電晶體結構**
  - 解釋為什麼 PD 中通常偏好 NAND？
  - NAND 的串聯部分是 NMOS，導通性比 PMOS 好，面積效益較佳

### 信號問題

- **什麼是 Cross-talk？如何解決？**
  - Shielding
  - Spacing
  - Upsize driver

- **什麼是 Metastability（亞穩態）？**
  - 如何處理跨 Clock Domain (CDC) 的問題？
  - 兩級 Flip-Flop 同步器

---

## 4. Low Power Design (Advanced Low Power VLSI)

對應修課紀錄中的課程，在現代晶片設計非常加分。

### 功耗組成

- **Dynamic Power vs Leakage Power 的公式與成因？**

- **什麼是 Glitch？它如何影響功耗？**

### 省電技術

- **Clock Gating 的原理與好處？**

- **Multi-Vth (HVT/LVT) 的權衡？**
  - LVT：速度快但漏電多
  - HVT：省電但慢

---

## 5. Coding & Scripting

面試官對 "Basic data structure concept" 很嚴格，甚至有點 "Brutal"。雖然是硬體工程師，但現在的 DV 或 PD flow 都很吃程式能力。

### 演算法/腳本

- **遞迴 (Recursion) 問題**
  - 如何用遞迴將 x 遞減至 0

- **Scripting**
  - 如何 parse 兩個檔案找出共同的變數名稱？
  - Python/Perl 腳本題，在自動化 flow 很常見

---

## 參考資料

- NPU 專案經驗
- Innovus APR Flow 實作
- Advanced Low Power VLSI 課程
