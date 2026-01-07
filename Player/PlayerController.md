# 🎮 Player Controller

> **Prefab:** LunorisPlayer / LunoraPlayer  
> **Где настраивать:** HybridPlayerController компонент на prefab'e

---

## ✅ Current (As-Is)
- Гибридный контроллер: First Person + Third Person
- Переключение камеры по кнопке
- Спринт, прыжок, гравитация
- Интеграция с Cinemachine
- Input System (новая система ввода Unity)
- VContainer DI для PauseService

## 🧩 Known Issues / TODO
- [ ] Добавить крауч
- [ ] Улучшить плавность переключения камер
- [ ] Добавить coyote time для прыжков

## 💡 Notes
- При First Person модель игрока скрывается
- Third Person поддерживает смену плеча (Left/Right)

---

## 📊 Gameplay Flow

| Player Input | Game Response |
|--------------|---------------|
| WASD / Stick | Движение персонажа |
| Shift / L3 | Спринт |
| Space / A | Прыжок |
| Tab / Y | Переключение 1P ↔ 3P |
| Q / LB | Смена плеча камеры (3P) |
| Mouse / Right Stick | Вращение камеры |

---

## ⚙️ Parameters

| Параметр | Значение | Описание |
|----------|----------|----------|
| `MoveSpeed` | 4.0 м/с | Скорость ходьбы |
| `SprintSpeed` | 6.0 м/с | Скорость бега |
| `JumpHeight` | 1.2 м | Высота прыжка |
| `Gravity` | -15.0 | Своя гравитация |
| `RotationSmoothTime` | 0.12 с | Плавность поворота (3P) |
| `RotationSpeed` | 1.0 | Скорость поворота (1P) |
| `JumpTimeout` | 0.1 с | Кулдаун прыжка |
| `FallTimeout` | 0.15 с | Задержка перед fall state |
| `GroundedOffset` | -0.1 | Смещение проверки земли |
| `GroundedRadius` | 0.28 | Радиус проверки земли |

---

## 📹 Camera Modes

### First Person
- `FirstPersonCamera` — CinemachineCamera
- Модель игрока скрывается (`PlayerModel.SetActive(false)`)
- Камера привязана к `CinemachineCameraTarget`

### Third Person  
- `ThirdPersonCamera` — CinemachineCamera
- `CinemachineThirdPersonFollow` для orbit
- Поддержка смены плеча: `CameraSide` (0 = Left, 1 = Right)
- `CameraSideTransitionDuration` = 0.3 с

---

## 🎬 Анимации

| Состояние | Когда активируется |
|-----------|---------------------|
| Idle | Стоит на месте |
| Walk/Run | Движение (blend по скорости) |
| Jump | Прыжок |
| FreeFall | Падение |

---

## 🔗 Dependencies

| Система | Связь |
|---------|-------|
| **CharacterController** | Движение, коллизии |
| **PlayerInput** | Input System |
| **Cinemachine** | Камеры |
| **PauseService** | Блокировка при паузе |
| **StarterAssetsInputs** | Обёртка над Input |
| **FootstepSystem** | FMOD звуки шагов |

---

## 🔧 Components Required

```
[RequireComponent]
├── CharacterController
├── PlayerInput (если ENABLE_INPUT_SYSTEM)
└── StarterAssetsInputs
```

---

## 📁 Related Files

```
Assets/Scripts/
├── Player/
│   └── HybridPlayerController.cs
├── Camera/
│   ├── VirtualCameraSwitcher.cs
│   ├── ThirdPersonCameraOrbit.cs
│   └── FPCameraMovementLook.cs
├── Audio/
│   ├── FootstepSystem.cs
│   └── FMODFootsteps.cs
└── Services/
    └── PauseService.cs
```
