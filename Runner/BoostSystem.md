# 🏎️ Car Boost System

> **Режим:** Runner Mode (гоночные уровни)  
> **Где настраивать:** Компонент CarBoostSystemNWH на машине

---

## ✅ Current (As-Is)
- 3-уровневая система бустов
- Автоматическая остановка буста при столкновении
- Интеграция с NWH Vehicle Physics 2
- FMOD звуки буста
- Визуальные эффекты для каждого уровня
- VContainer DI для ObstacleService

## 🧩 Known Issues / TODO
- [ ] Плавный переход между уровнями буста
- [ ] Больше VFX вариаций
- [ ] Добавить trail эффекты

## 💡 Notes
- Буст работает бесконечно до столкновения или провала QTE
- При Level 3 — переход на верхний этаж дороги

---

## 📊 Gameplay Flow

| Trigger | Response |
|---------|----------|
| QTE Success | +1 уровень буста |
| Boost activated | Увеличение мощности двигателя |
| Collision | Сброс буста |
| QTE Fail | Сброс буста |
| Level 3 reached | Триггер RoadLevelSwitcher |

---

## 🚀 Boost Levels

| Level | Эффект | Визуал |
|-------|--------|--------|
| 0 | Нет буста | Нет эффектов |
| 1 | +X% мощности | Лёгкое свечение |
| 2 | +Y% мощности | Интенсивное свечение |
| 3 | +Z% мощности | Максимум + переход наверх |

*Конкретные значения в `BoostLevelDataNWH[]`*

---

## ⚙️ Parameters

| Параметр | Описание |
|----------|----------|
| `vehicleController` | NWH VehicleController |
| `boostLevels[3]` | Массив настроек уровней |
| `transitionSpeed` | 0.3 — плавность эффектов |
| `enableDebugLogs` | true — логирование |

### BoostLevelDataNWH

```csharp
[Serializable]
public class BoostLevelDataNWH {
    float powerMultiplier;   // Множитель мощности
    GameObject[] meshes;     // Активируемые меши
    GameObject[] effects;    // VFX
    // ... звуки, материалы
}
```

---

## 🔄 State

```
Level 0 (No Boost)
    ↓ QTE Success
Level 1
    ↓ QTE Success
Level 2
    ↓ QTE Success
Level 3 → Upper Road Trigger
    ↓ Collision / QTE Fail (any level)
Level 0
```

---

## 🎯 API

```csharp
// Активировать буст уровня N
boostSystem.ActivateBoost(int level);

// Деактивировать буст
boostSystem.DeactivateBoost();

// Получить текущий уровень
int level = boostSystem.CurrentBoostLevel;

// Буст активен?
bool active = boostSystem.IsBoostActive;

// События
boostSystem.OnBoostActivated += (level) => { };
boostSystem.OnBoostDeactivated += (level) => { };
```

---

## 🔗 Dependencies

| Компонент | Связь |
|-----------|-------|
| **VehicleController** | NWH Physics — изменение мощности |
| **ObstacleService** | Подписка на столкновения |
| **DriftQTESystemNWH** | Источник активации буста |
| **RoadLevelSwitcherNWH** | Переключение этажей при L3 |
| **FMOD** | Звуки буста |

---

## 🎬 Visual Effects

| Level | Mesh/Effect | Описание |
|-------|-------------|----------|
| 1 | `boostLevels[0].meshes` | Лёгкие эффекты |
| 2 | `boostLevels[1].meshes` | Средние эффекты |
| 3 | `boostLevels[2].meshes` | Максимальные эффекты |

*Все эффекты выключены по умолчанию в Awake*

---

## 📁 Related Files

```
Assets/Scripts/Runner/
├── CarBoostSystemNWH.cs       ← Main
├── DriftQTESystemNWH.cs       ← QTE trigger
├── RoadLevelSwitcherNWH.cs    ← Level 3 handler
├── ObstacleService.cs         ← Collision events
└── CarRecoveryManagerNWH.cs   ← Recovery blocking
```
