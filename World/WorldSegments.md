# 🌍 World Segments

> **Где настраивать:** SegmentLoader на объекте в Main сцене

---

## ✅ Current (As-Is)
- Additive Scene Loading для сегментов мира
- Distance-based streaming (опционально)
- Поддержка нескольких сегментов одновременно
- Интеграция с Cozy Weather для биомов
- События загрузки/выгрузки

## 🧩 Known Issues / TODO
- [ ] Оптимизация переходов между сегментами
- [ ] Seamless terrain stitching
- [ ] LOD для далёких сегментов

## 💡 Notes
- Сегменты — это отдельные сцены, загружаемые аддитивно
- Streaming включается через `enableStreaming`
- Требует `streamingReference` (обычно игрок)

---

## 📊 Flow

| Trigger | Action |
|---------|--------|
| Scene Start (loadOnStart) | Загрузка всех сегментов |
| Player moves (streaming ON) | Проверка дистанции до сегментов |
| Player near segment | `LoadSegment(sceneName)` |
| Player far from segment | `UnloadSegment(sceneName)` |
| All segments loaded | `OnAllSegmentsLoaded` event |

---

## ⚙️ Parameters (SegmentLoader)

| Параметр | Значение | Описание |
|----------|----------|----------|
| `segments` | List<SegmentInfo> | Список сегментов |
| `loadOnStart` | true | Загружать при старте |
| `enableStreaming` | false | Дистанционная загрузка |
| `streamingDistance` | 500.0 | Дистанция стриминга |
| `streamingReference` | Transform | Точка отсчёта (игрок) |

---

## 📦 Настройка сегмента

| Поле | Описание |
|------|----------|
| Scene Name | Имя сцены для загрузки |
| Center Position | Центр сегмента (для streaming) |
| Is Loaded | Статус загрузки |

---

## 📂 Структура сцен

| Папка | Содержимое |
|-------|------------|
| ELAR_MasterScene | Основная сцена |
| Ally_EchoGarden_Segments | Сегменты Echo Garden |
| Elar_OpenWorld | Open World сегменты |
| Reworked Tutorial | Туториал |

---

## 🔗 Dependencies

| Компонент | Связь |
|-----------|-------|
| **SceneManager** | Additive loading |
| **Cozy Weather** | BiomeCozyController |
| **Terrain** | TerrainSegmentManager |
| **Player Transform** | streamingReference |

---

## 🌦️ Biome Integration (Cozy Weather)

`BiomeCozyController.cs` управляет погодой в зависимости от сегмента:

| Сегмент | Биом/Погода |
|---------|-------------|
| Echo Garden | Туман, мягкий свет |
| Nightmare Zone | Тёмное небо, гроза |
| Dream Hub | Ясно, тёплые тона |

---

## 📁 Related Files

```
Assets/Scripts/WorldSegments/
├── SegmentLoader.cs
├── SegmentConfig.cs
├── TerrainSegmentManager.cs
├── BiomeCozyController.cs
└── Editor/
    ├── TerrainGridCreator.cs
    └── TerrainSeamFixer.cs
```
