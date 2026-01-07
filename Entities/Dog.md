# 🐕 Entity: Dog (Companion)

> **Тип:** Friendly NPC / Companion  
> **Prefab:** `Prefabs/GamePlay/Lucid Point Dog.prefab`  
> **Модель:** `External/Freddy_dog_Ch/` или `External/Dog/`

---

## ✅ Current (As-Is)
- Собака следует за игроком
- Патрулирует по waypoints когда игрок далеко
- Реагирует на Lucid Points (подбирает, анимация)
- AI на базе Malbers Animations + ScriptableObject states
- Интегрирован FMOD для звуков

## 🧩 Known Issues / TODO
- [ ] Иногда застревает на геометрии
- [ ] Нужна анимация "лежит и ждёт"
- [ ] Улучшить pathfinding на сложных террейнах

## 💡 Notes
- Использует MalbersAnimations.Scriptables для AI состояний
- Lucid Points — коллекционные объекты, которые собака находит

---

## 📊 Gameplay Flow

| Player Does | Dog Does |
|-------------|----------|
| Стоит на месте | Патрулирует рядом |
| Идёт далеко | Следует за игроком |
| Вызывает (кнопка) | Бежит к игроку |
| Рядом Lucid Point | Поворачивает голову, идёт к нему |
| Подошёл к Lucid Point | Анимация "подбирает" |

---

## 🧠 AI States (ScriptableObjects)

| State Asset | Описание |
|-------------|----------|
| `Dog Follow Player MAIState.asset` | Следование за игроком |
| `DogPatrol MAIState.asset` | Патруль по точкам |
| `DogGoToLucidPoint MAIState.asset` | Идёт к Lucid Point |
| `Dog Point PickUp Animation MAIState.asset` | Анимация подбора |
| `DogWayPoints.asset` | Waypoints для патруля |

---

## 🔗 Dependencies

| Система | Связь |
|---------|-------|
| **Malbers Animations** | AI Brain, States |
| **Lucid Points** | Коллекционные объекты |
| **FMOD** | DogAudioController |
| **Player** | Целевой Transform для follow |
| **Objectives** | Может тригерить цели |

---

## 🎵 Audio

**Скрипт:** `Scripts/Audio/DogAudioController.cs`

| Событие | Звук |
|---------|------|
| Шаги | Footsteps по поверхности |
| Bark | Лай при призыве |
| Pickup | Звук подбора Lucid Point |

---

## 🎯 Tuning / Parameters

| Параметр | Значение | Где настраивать |
|----------|----------|----------------|
| Follow Distance | 3-5 м | Malbers AI Brain |
| Stop Distance | 1.5 м | Malbers AI Brain |
| Patrol Radius | По waypoints | DogWayPoints.asset |
| Look At Speed | Настраиваемо | D_LookAtPlayer.asset |
| Lucid Detection | Авто | D_LookAtLucidPoints.asset |

---

## 📸 Visual References

| Описание | Файл |
|----------|------|
| Модель собаки | `External/Freddy_dog_Ch/` |
| Альтернативная модель | `External/Dog/` |
| Prefab в игре | `Prefabs/GamePlay/Lucid Point Dog.prefab` |

*TODO: добавить скриншоты/гифки собаки в игре*

---

## 🔧 Ключевые файлы

| Тип | Путь |
|-----|------|
| Prefab | Prefabs/GamePlay/Lucid Point Dog |
| AI States | Scripts/DogAI/*.asset |
| Модель | External/Freddy_dog_Ch/ |
| Аудио | Scripts/Audio/DogAudioController |
