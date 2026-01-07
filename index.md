# Lunoris — Game Design Document (As-Is)

> **Что это:** Документация текущего состояния игры.  
> **Формат:** Вики-структура, короткие страницы, практические примеры.  
> **Цель:** Онбординг новых участников + фиксация "что реально работает".

---

## 🎮 О проекте

**Lunoris** — 3D приключенческая игра с элементами:
- Исследование открытого мира
- Механика сновидений (Dream Hub / Nightmare Hub)
- Компаньон-собака
- Гоночный/раннер режим с дрифтом
- Система прогрессии и квестов

**Персонажи:**
- **Lunoris** — главный герой (мужской)
- **Lunora** — альтернативный персонаж (женский)
- **Dog (Freddy)** — собака-компаньон

---

## 📂 Структура GDD

### 🧍 Player
| Страница | Описание |
|----------|----------|
| [Player Controller](Player/PlayerController.md) | Гибридное управление 1P/3P, движение, прыжки |
| [Camera System](Player/CameraSystem.md) | Cinemachine, переключение режимов |
| [Player Stats](Player/PlayerStats.md) | HP, Lucid Points, Shards |

### 🐕 Entities
| Страница | Описание |
|----------|----------|
| [Dog Companion](Entities/Dog.md) | AI собаки, патруль, следование, Lucid Points |
| [Ghost Enemy](Entities/Ghost.md) | Летающий враг, FSM, атака "сквозь" |
| [Easy Enemy](Entities/EasyEnemy.md) | Базовый враг с патрулём |
| [Hard Enemy](Entities/HardEnemy.md) | Продвинутый враг |

### 🏎️ Runner Mode (Car)
| Страница | Описание |
|----------|----------|
| [Car Controller (NWH)](Runner/CarController.md) | NWH Vehicle Physics 2 |
| [Boost System](Runner/BoostSystem.md) | 3-уровневая система бустов |
| [Drift QTE](Runner/DriftQTE.md) | QTE механика при Near Miss |
| [Near Miss Detector](Runner/NearMissDetector.md) | Детектор близкого проезда |
| [Road System](Runner/RoadSystem.md) | Генерация дороги, сегменты |
| [Obstacles](Runner/Obstacles.md) | Препятствия, столкновения |

### 🌍 World & Levels
| Страница | Описание |
|----------|----------|
| [World Segments](World/WorldSegments.md) | Стриминг сегментов мира |
| [Level Service](World/LevelService.md) | Загрузка уровней, переходы |
| [Hub System](World/HubSystem.md) | Dream Hub / Nightmare Hub |
| [Scenes Overview](World/Scenes.md) | Карта сцен проекта |

### 💾 Progression & Saving
| Страница | Описание |
|----------|----------|
| [Save System](Progression/SaveSystem.md) | SaveLoaderService, данные |
| [Objectives](Progression/Objectives.md) | Система квестов/целей |
| [Progress Tracking](Progression/ProgressTracking.md) | Lucid Points, Shards, уровни |

### 🎨 UI
| Страница | Описание |
|----------|----------|
| [HUD](UI/HUD.md) | PlayerStatsUI, ObjectivesUI |
| [Menus](UI/Menus.md) | Pause, MainMenu, Settings |
| [Loading Screens](UI/LoadingScreens.md) | Transitions, Video screens |
| [Retro Vision](UI/RetroVision.md) | Режим "ночного видения" |
| [Prompts](UI/Prompts.md) | Input prompts, подсказки |

### 🔊 Audio
| Страница | Описание |
|----------|----------|
| [FMOD Integration](Audio/FMOD.md) | BGM, SFX сервисы |
| [Footsteps](Audio/Footsteps.md) | Шаги, поверхности |
| [Dog Audio](Audio/DogAudio.md) | Звуки собаки |

### 🎭 Narrative
| Страница | Описание |
|----------|----------|
| [Dialogue System](Narrative/Dialogue.md) | Yarn Spinner |
| [Portraits](Narrative/Portraits.md) | UI диалогов |

### ⚙️ Core Systems
| Страница | Описание |
|----------|----------|
| [Event Bus](Core/EventBus.md) | GameEvents, подписки |
| [Pause System](Core/Pause.md) | PauseService, блокировки |
| [VContainer DI](Core/DependencyInjection.md) | Scopes, инъекции |
| [Interactions](Core/Interactions.md) | IInteractable |

### 🎬 Effects & VFX
| Страница | Описание |
|----------|----------|
| [Post Processing](Effects/PostProcessing.md) | Глаза, эффекты |
| [Visual Effects](Effects/VFX.md) | Частицы, dissolve |
| [Dream Levitation](Effects/DreamLevitation.md) | Левитация во снах |

---

## ✅ Текущий статус

| Система | Статус | Примечания |
|---------|--------|------------|
| Player Controller | ✅ Работает | 1P/3P, спринт, прыжок |
| Dog AI | ✅ Работает | Malbers integration |
| Ghost Enemy | ✅ Работает | FSM, атака |
| Runner Mode | ✅ Работает | NWH Physics 2 |
| Save System | ✅ Работает | JSON сериализация |
| Objectives | ✅ Работает | Event-based completion |
| Dialogue | 🔶 Базово | Yarn Spinner |
| World Streaming | ✅ Работает | Additive scenes |

---

## 🧩 Known Issues / TODO

- [ ] UI cursor иногда залипает после паузы
- [ ] Оптимизация стриминга террейна
- [ ] Добавить больше QTE комбинаций
- [ ] Баланс параметров врагов

---

## 💡 Как пользоваться этим GDD

1. **Новый участник** → Читай [Core Systems](Core/) сначала
2. **Работаешь над фичей** → Найди соответствующую страницу
3. **Баг/вопрос** → Смотри секцию "Edge Cases" на странице системы
4. **Добавляешь фичу** → Создай новую страницу по шаблону

---

## 📌 Быстрые ссылки

- [Шаблон страницы механики](Templates/MechanicTemplate.md)
- [Шаблон страницы Entity](Templates/EntityTemplate.md)
- [Техническая архитектура](Tech/Architecture.md)
