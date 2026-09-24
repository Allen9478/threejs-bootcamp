# Three.js 進階版課程（Vue 3 路線，8 週嚴格版）

> 目標：8 週後，做出一個部署上線、含後端 API 的 **3D 產品配置器**，並能通過初階前端面試中的 Three.js 問題。
> 版本紀錄：Three.js 版本 `r___`（安裝後填入）｜Vue `3.__`｜開始日期 `____/__/__`

---

## 一、總覽

| 項目 | 內容 |
|---|---|
| 總時數 | 8 週 × 約 18 小時 ≈ 144 小時 |
| 每週節奏 | 週一至五各 2.5h、週六 4h（專題）、週日 1.5h（驗收與複習） |
| 學習比例 | 30% 看教材、70% 動手寫 |
| 技術棧 | Vite、Vue 3（`<script setup>`）、TypeScript（第 5 週起）、Three.js、lil-gui、GSAP、Pinia、Vitest |
| 最終成果 | 3D 產品配置器（前端 + 後端 API + 上線） |

**課程結構**
- 第 1～4 週：純 Three.js（Vite + 原生 JS），先學紮實 3D 核心觀念
- 第 5～6 週：Vue 整合、效能與進階材質
- 第 7～8 週：畢業專題（前後端、上線、面試準備）

---

## 二、嚴格模式規則

1. **手打程式碼**：教學程式碼不准整段複製貼上，看懂後關掉教材再自己寫。
2. **每日 commit**：repo 設為 public，commit message 用 Conventional Commits（`feat:` / `fix:` / `refactor:`）。
3. **每日 3 行日誌**（寫在 `LOG.md`）：今天學到什麼、卡在哪、明天做什麼。
4. **30 分鐘卡關規則**：先 `console.log` 與 DevTools 除錯 30 分鐘 → 查官方文件與 discourse.threejs.org → 最後才問 AI。問 AI 只能問「為什麼」，不能要整段解答。
5. **週日驗收是關卡**：沒全過，下週前兩天補完才能繼續，不准跳過。
6. **每週一篇筆記**：用自己的話解釋一個核心概念，寫進 README 或部落格。
7. **版本鎖定**：`npm i three` 後把版本號記在 README。遇到 API 找不到，先查官方 Migration Guide。

---

## 三、Repo 建議結構

```
threejs-bootcamp/
├── README.md              # 課程總覽與進度（可直接放本檔）
├── LOG.md                 # 每日 3 行日誌
├── notes/                 # 每週一篇概念筆記
│   ├── week-01.md
│   └── ...
├── week-01-solar-system/  # 各週專題（各自是一個 Vite 專案）
├── week-02-pbr-showroom/
├── week-03-camera-tour/
├── week-04-model-viewer/
├── week-05-vue-viewer/
└── week-06-performance/
```

畢業專題（第 7～8 週）建議 **另開獨立 repo**（例如 `3d-product-configurator`），作品集會更清楚。

---

## 四、每週課程

### Week 1：Three.js 核心與場景圖

- [ ] **週一**：Vite 專案建立；Scene / Camera / Renderer / Mesh 四大核心；畫出第一個立方體
- [ ] **週二**：渲染迴圈 `requestAnimationFrame`；`Clock` 與 deltaTime；resize 處理（`camera.aspect`、`updateProjectionMatrix`、`setSize`）；`setPixelRatio(Math.min(devicePixelRatio, 2))`
- [ ] **週三**：座標系（右手座標）；position / rotation / scale；弧度與角度；`Vector3` 運算；`AxesHelper`、`GridHelper`
- [ ] **週四**：內建 Geometry；`BufferGeometry` 與 attributes（position / normal / uv）；Basic / Standard / Normal / Wireframe 材質差異
- [ ] **週五**：`Object3D` 與 `Group` 父子階層；世界座標與本地座標；lil-gui 除錯面板
- [ ] **週六｜專題 1：太陽系模型**（Group 階層、公轉自轉、lil-gui 調速度）
- [ ] **週日**：驗收

**驗收關卡**
- [ ] 不看文件，40 行內默寫出最小可運作的 Three.js 程式
- [ ] 能口頭解釋為什麼 resize 要更新 `aspect` 並呼叫 `updateProjectionMatrix`
- [ ] 太陽系動畫在 60Hz 與 144Hz 螢幕速度一致（用 deltaTime，不用「每幀加固定值」）
- [ ] 渲染迴圈內沒有每幀 `new` 物件

---

### Week 2：光源、陰影、貼圖、PBR

- [ ] **週一**：Ambient / Directional / Point / Spot / Hemisphere 光；各種 LightHelper
- [ ] **週二**：陰影：`castShadow` / `receiveShadow`、`shadow.mapSize`、shadow camera 範圍、`bias` / `normalBias`、`CameraHelper` 除錯
- [ ] **週三**：`TextureLoader`；UV；wrap / repeat；mipmap 與 filter；**色彩空間**（顏色貼圖設 `SRGBColorSpace`，法線 / roughness 等資料貼圖維持線性）
- [ ] **週四**：`MeshStandardMaterial`：roughness / metalness / normalMap / aoMap；`MeshPhysicalMaterial` 簡介（clearcoat）
- [ ] **週五**：HDRI 環境貼圖（`scene.environment`、`PMREMGenerator`）；`toneMapping`（ACESFilmic）；`outputColorSpace`。HDR 載入器名稱依版本而異（RGBELoader / HDRLoader），以你安裝版本的文件為準
- [ ] **週六｜專題 2：PBR 展示台**（roughness × metalness 球體矩陣、貼圖地板、陰影、HDRI 環境光）
- [ ] **週日**：驗收

**驗收關卡**
- [ ] 能解釋貼圖「太白或太暗」的成因與修正方式
- [ ] 陰影無 shadow acne（條紋）與 peter-panning（陰影浮空）
- [ ] 能說出 Basic 與 Standard 材質的本質差異（是否受光照 / PBR）
- [ ] 能說出陰影對效能的代價來源

---

### Week 3：相機、控制、動畫

- [ ] **週一**：Perspective vs Orthographic；fov / near / far；z-fighting 成因與對策；`lookAt`
- [ ] **週二**：`OrbitControls`：damping、角度與距離限制、`target`、`autoRotate`；為什麼要 `controls.update()`
- [ ] **週三**：動畫：deltaTime、lerp / damp、easing；GSAP tween 與 timeline；相機飛行時 `camera.position` 與 `controls.target` 同步動畫
- [ ] **週四**：`Quaternion` vs `Euler`（萬向鎖）；`MathUtils`；`Box3` 計算包圍盒並「自動取景」
- [ ] **週五**：pointer 事件；滑鼠視差；捲動驅動相機（scroll-driven）
- [ ] **週六｜專題 3：相機導覽**（按鈕或捲動切換 3 個視角，平滑飛行，飛行中可被打斷）
- [ ] **週日**：驗收

**驗收關卡**
- [ ] 相機飛行中再點另一個視角，不會跳動或卡住（處理 tween 衝突）
- [ ] 能說出 `near` 設太小會造成什麼問題
- [ ] 能用 `Box3` 讓任意大小的物件都自動置中取景

---

### Week 4：互動與模型載入

- [ ] **週一**：`Raycaster`；pointer 座標轉 NDC；`intersectObjects`；hover 與 click
- [ ] **週二**：互動進階：高亮（emissive）；`recursive` 選項；`userData` 綁定資料；觸控支援；區分「點擊」與「拖曳」（避免與 OrbitControls 衝突）
- [ ] **週三**：glTF / GLB 結構（scene / nodes / meshes / materials / animations）；`GLTFLoader`（`three/addons/loaders/GLTFLoader.js`）；找免費模型（Khronos glTF-Sample-Assets、Sketchfab CC 授權、Poly Pizza），並確認授權
- [ ] **週四**：模型處理：`traverse` 遍歷；材質替換；縮放正規化與置中；`DRACOLoader`；`LoadingManager` 進度條；用 gltf-transform 壓縮模型
- [ ] **週五**：`AnimationMixer` / `AnimationAction`；`crossFadeTo` 切換動畫；`mixer.update(delta)`
- [ ] **週六｜專題 4：互動模型檢視器**（載入進度條、hover 高亮、點擊聚焦、動畫切換）
- [ ] **週日**：驗收

**驗收關卡**
- [ ] 能口述 Raycaster 完整流程（螢幕座標 → NDC → 射線 → 相交檢測）
- [ ] 拖曳旋轉時不會誤觸發 click
- [ ] 模型載入失敗時有錯誤提示，不是白畫面
- [ ] 能說明 glTF 為何被視為 Web 3D 標準格式

---

### Week 5：Vue 整合 ★ 本課程重點

- [ ] **週一**：Vue 3 + Vite + TS 專案；`onMounted` 建立、`onBeforeUnmount` 銷毀；canvas 用 template ref；用 `ResizeObserver` 監聽容器（取代 `window.resize`）
- [ ] **週二**：**響應式陷阱**：Three 物件（scene / mesh / renderer）不要放進 `ref` / `reactive`，會被 Proxy 深層代理，造成效能問題與奇怪 bug；改用 `shallowRef` 或 `markRaw`。原則：Vue 狀態驅動 Three，不要反過來
- [ ] **週三**：封裝 composable：`useThreeScene`、`useResizeObserver`、`useGLTF`；**按需渲染**（只在 controls 變動或動畫進行時 render，靜止時不跑迴圈）
- [ ] **週四**：完整 `dispose`：自寫 `disposeObject(obj)`（traverse 釋放 geometry / material / texture）；`renderer.dispose()`、`forceContextLoss()`；移除事件監聽；取消 `requestAnimationFrame`；用 `renderer.info.memory` 驗證
- [ ] **週五**：Pinia 管理配置狀態（顏色、材質、選中部件）；Vue Router 切頁；HTML overlay（`Vector3.project()` 投影或 `CSS2DRenderer`）；Vue 元件做 tooltip
- [ ] **週六｜專題 5：把專題 4 重構為 Vue 元件化**（`<ThreeCanvas>`、`<ModelViewer>`、`<ColorPanel>`、`<HotspotOverlay>`）
- [ ] **週日**：驗收

**驗收關卡**
- [ ] 來回切換路由 20 次，`renderer.info.memory` 的 geometries / textures 數量不持續成長
- [ ] 專案中沒有任何 Three 物件被放進 `ref` / `reactive`
- [ ] 能解釋為什麼 Three 物件不適合被 Vue 深層響應式代理
- [ ] 改 Pinia 的顏色，模型即時更新，且沒有每次都重建材質
- [ ] 元件卸載後 DevTools 看不到殘留的事件監聽與迴圈

---

### Week 6：效能、進階材質、生態認識

- [ ] **週一**：效能觀念：draw call、三角面數、`renderer.info`；工具：stats.js、Chrome Performance、Spector.js
- [ ] **週二**：優化手法：`InstancedMesh`；共用 geometry / material；`mergeGeometries`；貼圖尺寸與 KTX2 壓縮；LOD；DPR 上限；陰影與光源數量控制
- [ ] **週三**：材質進階：`MeshPhysicalMaterial`（transmission、clearcoat）；`envMapIntensity`；做出皮革 / 金屬 / 木頭 / 玻璃四種可切換材質
- [ ] **週四**：後處理入門：`EffectComposer`、`OutlinePass`（選取外框）、Bloom、`OutputPass`；理解其效能代價
- [ ] **週五**：生態認識：TresJS 文件精讀，用它重做最小範例並比較優缺點（1.5h）；Shader 概念認識：`ShaderMaterial`、uniforms、簡單 fragment 特效（1h，只求看得懂）
- [ ] **週六｜專題 6：效能挑戰**（1 萬個 `InstancedMesh` 穩定 60fps，並與未優化版本對照 draw call / fps 數據，寫進 README）
- [ ] **週日**：驗收

**驗收關卡**
- [ ] 有優化前後的量化數據（draw calls、fps、記憶體）
- [ ] 能說出至少 5 種降低 GPU 或 CPU 負擔的手法
- [ ] 能說明 TresJS 與原生 Three.js 的取捨

---

### Week 7：畢業專題（上）：規劃、核心功能、後端

**專題：3D 產品配置器**（例如球鞋、椅子、耳機等）

- [ ] **週一**：需求文件：User Story、資料模型、線框圖；選模型（授權清楚）；檢查模型（mesh 命名、面數 < 10 萬、材質數量）並用 gltf-transform 優化
- [ ] **週二**：專案骨架：`<ThreeCanvas>`、載入流程、Loading 畫面、錯誤與空狀態
- [ ] **週三**：配置功能：顏色 / 材質切換（Pinia）、部件顯示隱藏、預設組合
- [ ] **週四**：相機與互動：預設視角按鈕、hotspot 標註、點擊聚焦
- [ ] **週五**：後端 API（用你熟悉的 Node / Express 等）：`GET` 產品與選項資料、`POST` 儲存配置、產生分享連結
- [ ] **週六**：前後端整合：分享連結可還原配置；截圖匯出（渲染後立即 `toBlob`）
- [ ] **週日**：中期驗收：對照需求文件逐條打勾，自我 code review

---

### Week 8：畢業專題（下）：品質、上線、面試準備

- [ ] **週一**：RWD 與觸控；行動裝置降級策略（降 DPR、關陰影與後處理）
- [ ] **週二**：效能與記憶體：路由切換無洩漏；Three.js 相關頁面 lazy load；bundle analyzer；Lighthouse
- [ ] **週三**：可及性與健壯性：鍵盤操作、`prefers-reduced-motion`、WebGL 不支援的 fallback、canvas 的 `aria-label`
- [ ] **週四**：品質：Vitest 測試純函式（`disposeObject`、座標投影、顏色轉換）；ESLint + Prettier；TS strict
- [ ] **週五**：部署：前端 Vercel / Netlify，後端 Render / Railway / Fly；README 寫架構圖、Demo GIF、技術決策與效能數據
- [ ] **週六**：面試準備：對著錄音機講解專案 10 分鐘；自測下方 20 題；整理履歷寫法
- [ ] **週日**：最終驗收

**畢業專題驗收清單**
- [ ] 線上可存取，手機與桌機皆正常
- [ ] 載入有進度條，失敗有提示
- [ ] 顏色 / 材質即時切換，配置可存檔並以連結分享還原
- [ ] 至少 3 個 hotspot，點擊可聚焦與顯示資訊
- [ ] 切換路由無記憶體洩漏（附 `renderer.info` 驗證截圖）
- [ ] README 包含架構、GIF、效能數據、技術取捨
- [ ] 測試通過，無 ESLint 錯誤

---

## 五、面試自測 20 題

**Three.js 基礎**
1. Three.js 渲染一幀的流程是什麼？
2. Scene、Camera、Renderer 各自負責什麼？
3. 為什麼 resize 要更新 `camera.aspect` 與投影矩陣？
4. `Mesh` = `Geometry` + `Material`，那 `Object3D` 是什麼？
5. `MeshBasicMaterial` 與 `MeshStandardMaterial` 的差異？
6. 色彩空間為什麼會影響貼圖顏色？
7. 如何讓動畫在不同更新率的螢幕上速度一致？
8. Raycaster 如何判斷點到哪個物件？
9. glTF 的優勢是什麼？為什麼要用 Draco / KTX2？
10. Euler 與 Quaternion 的差異？

**Vue 整合**

11. 為什麼不能把 Three 物件放進 `reactive`？該用什麼？
12. Vue 元件卸載時，Three.js 需要清理哪些東西？
13. 為什麼用 `ResizeObserver` 比 `window.resize` 好？
14. 什麼是按需渲染？何時適用？
15. 如何避免 HMR 造成的 WebGL context 洩漏？

**效能與工程**

16. 什麼是 draw call？如何降低？
17. `InstancedMesh` 的原理與限制？
18. 如何偵測與驗證記憶體洩漏？
19. 行動裝置上你會做哪些降級？
20. 如果模型有 50 MB，你會怎麼處理載入體驗？

---

## 六、學習資源

| 資源 | 用途 | 費用 |
|---|---|---|
| threejs.org 官方文件與 Examples | 主力參考，每個範例有原始碼 | 免費 |
| Discover three.js（discoverthreejs.com） | 觀念紮實，適合第 1～3 週。部分內容較舊，注意版本差異 | 免費 |
| Three.js Journey（Bruno Simon） | 最完整的系統課程，可作為第 1～6 週主教材 | 付費 |
| discourse.threejs.org | 卡關時查詢 | 免費 |
| gltf-transform、gltf.report | 模型檢查與壓縮 | 免費 |
| TresJS 官方文件 | 第 6 週生態認識 | 免費 |

---

## 七、常見坑速查

- **版本不一致**：舊教學用 `texture.encoding`，新版是 `texture.colorSpace`
- **貼圖顏色怪**：顏色貼圖用 sRGB，資料貼圖（normal / roughness / ao）用線性
- **畫面模糊或很卡**：檢查 `devicePixelRatio` 是否有設上限
- **陰影瑕疵**：先用 `CameraHelper` 看 shadow camera 範圍，再調 `bias` / `normalBias`
- **Vue 裡效能異常**：檢查 Three 物件是否被 `ref` / `reactive` 包住
- **記憶體持續上升**：`renderer.info.memory` 是第一個檢查點
- **模型載入後過大或偏移**：用 `Box3` 做正規化與置中

---

## 八、課後延伸（找到工作後再學）

GLSL Shader 深入、React Three Fiber + drei、物理引擎（Rapier）、WebGPU 渲染器、Blender 建模基礎。

---

## 九、每週進度追蹤

| 週次 | 專題完成 | 驗收通過 | 筆記完成 | 備註 |
|---|---|---|---|---|
| Week 1 | ☐ | ☐ | ☐ | |
| Week 2 | ☐ | ☐ | ☐ | |
| Week 3 | ☐ | ☐ | ☐ | |
| Week 4 | ☐ | ☐ | ☐ | |
| Week 5 | ☐ | ☐ | ☐ | |
| Week 6 | ☐ | ☐ | ☐ | |
| Week 7 | ☐ | ☐ | ☐ | |
| Week 8 | ☐ | ☐ | ☐ | |
