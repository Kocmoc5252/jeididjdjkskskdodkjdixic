# Standoff 2 — Offsets `v0.39.1`

> **Источник:** `dump.cs` (IL2CPP)
> **Автор:** kocmoc
> **Обновлено:** v0.39.0 → **v0.39.1** (патч: структура классов не изменилась, сместились только номера строк дампа и часть обфусцированных имён)

---

## Содержание

| # | Класс | Описание | Строка dump.cs |
|---|-------|----------|----------------|
| 1 | [`PhotonPlayer`](#1-photonplayer) | Сетевой игрок (Photon networking) | `1201275` |
| 2 | [`ObjectPlayer`](#2-objectplayer) | Базовый класс для сетевых объектов | `42605` |
| 3 | [`CharacterPlayer`](#3-characterplayer) | Персонаж игрока (обёртка над PlayerController) | `31423` |
| 4 | [`Controller`](#4-controller) | Базовый класс всех игровых контроллеров | `31485` |
| 5 | [`PlayerController`](#5-playercontroller) | Основной контроллер игрока | `32107` |
| 6 | [`HitController`](#6-hitcontroller) | Базовый хит-контроллер | `39725` |
| 7 | [`PlayerHitController`](#7-playerhitcontroller) | Хит-контроллер в мультиплеере | `40101` |
| 8 | [`DummyHitController`](#8-dummyhitcontroller) | Хит-контроллер для локальной симуляции | `39548` |
| 9 | [`PropHitController`](#9-prophitcontroller) | Хит-контроллер для объектов (гранаты, пропсы) | `161628` |
| 10 | [`WeaponryController`](#10-weaponrycontroller) | Контроллер оружия (слоты, переключение) | `33851` |
| 11 | [`WeaponController`](#11-weaponcontroller) | Конкретное оружие (ствол, магазин, параметры) | `68515` |
| 12 | [`MovementController`](#12-movementcontroller) | Контроллер передвижения | `37531` |
| 13 | [`AimController`](#13-aimcontroller) | Контроллер прицеливания (Aim / FOV) | `40828` |
| 14 | [`PlayerMainCamera`](#14-playermaincamera) | Основная камера игрока | `32710` |
| 15 | [`PlayerSoundController`](#15-playersoundcontroller) | Звуки игрока | `35292` |
| 16 | [`NetworkController`](#16-networkcontroller) | Сетевой контроллер игрока | `31755` |

---

## 1. PhotonPlayer

**Строка:** `1201275` · Сетевой игрок (Photon networking)

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x10` | `_logger` | `ILogger` | |
| `+0x18` | `actorID` | `int` | уникальный ID игрока в комнате |
| `+0x20` | `nameField` | `string` | никнейм |
| `+0x28` | `<UserId>` | `string` | userId |
| `+0x30` | `IsLocal` | `bool` | это локальный игрок? |
| `+0x31` | `<IsInactive>` | `bool` | неактивен? |
| `+0x38` | `<CustomProperties>` | `Hashtable` | кастомные Photon-свойства |
| `+0x40` | `TagObject` | `object` | тег |

---

## 2. ObjectPlayer

**Строка:** `42605` · Базовый класс для сетевых объектов (`abstract`)

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x20` | `GEDDEHEFBDAGFCE` | `List<BBFCAFECCGGCBHE>` | |
| `+0x28` | `<FFCFFCAAADECBGD>` | `float` | |
| `+0x2C` | `<EEDCCFHAGBEFCDF>` | `float` | |
| `+0x30` | `DBDHAGBFCFCFHBE` | `float` | |
| `+0x34` | `GCEEEBAAGCECDHA` | `float` | |
| `+0x38` | `AGEABBBFHDEAFAH` | `float` | |
| `+0x40` | `AEFEBCBDBAEHEDC` | `HFCCGEEEFHABCGE` | |

---

## 3. CharacterPlayer

**Строка:** `31423` · Персонаж игрока (обёртка над `PlayerController`)
**Наследуется от:** `ObjectPlayer` (base at `+0x20`)

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x48` | `ACAGHGBEBCGBHHC` | `BEGDFDADGECHECB` | |
| `+0x50` | `GABACFFAABEFCCC` | `PlayerController*` | основной контроллер |
| `+0x58` | `GDFGHHGHCBBHBAD` | `bool` | |

---

## 4. Controller

**Строка:** `31485` · Базовый класс всех игровых контроллеров (`abstract`)
**Наследуется от:** `PhotonBehavior`

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x28` | `ADHFDDCHCAFCADF` | `GECFBGHHEAEHDCD` | состояние/тип |
| `+0x2C` | `BDDADFCBCECACBG` | `HCCHCCBHFHGHFGG` | команда: T/CT/Spec |
| `+0x30` | `HGCFCAEBDBGHCCD` | `BipedMap` | кости персонажа |
| `+0x38` | `FFHBCDAHBEGAEHF` | `Transform` | |
| `+0x40` | `GCHDDCCADFBGFCF` | `PhotonPlayer*` | **ВЛАДЕЛЕЦ этого контроллера** |
| `+0x48` | `ABAGCGDFHCHBDHA` | `int` | |
| `+0x4C` | `ECFBFGABHDFBCFH` | `int` | |
| `+0x50` | `HHAFBHAACAEFDED` | `bool` | |
| `+0x51` | `<HFACGADCCCFGGDE>` | `bool` | IsMine? |
| `+0x52` | `<BBEGFBCADEDFBHD>` | `bool` | |

---

## 5. PlayerController

**Строка:** `32107` · Основной контроллер игрока (главная структура для чита)

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x08` | `MaxCtHealth` | `static int` | макс HP за CT |
| `+0x0C` | `MaxCtArmor` | `static int` | макс броня за CT |
| `+0x10` | `MaxTrHealth` | `static int` | макс HP за TR |
| `+0x14` | `MaxTrArmor` | `static int` | макс броня за TR |
| `+0x28` | `_mainCameraHolder` | `Transform` | |
| `+0x30` | `_fpsCameraHolder` | `GameObject` | |
| `+0x38` | `_fpsDirective` | `GameObject` | |
| `+0x40` | `EECDDBDHECGABHA` | `PlayerLevelZonesController` | |
| `+0x48` | `AHGFBEBFHAEAFDE` | `PlayerCharacterView` | |
| `+0x50` | `HHHAEDDEGBABGED` | `PlayerCharacterView` | |
| `+0x58` | `FFABAHHGFAHAGGA` | `GFCECCCDBFCABFA` | |
| `+0x60` | `CCFHFFADCEDHAAG` | `EFHFAEADHEFDHBB` | |
| `+0x68` | `HCBCDAEHFGCAEBH` | `AGHGGFAEGBDCHBF` | |
| `+0x70` | `HAGHHCEACEHBEGH` | `FAAGEBEFFEDBHDA` | |
| `+0x78` | `ADGDDDGCBFEDDCF` | `bool` | |
| `+0x79` | `BDDGDCHAHDACCBH` | `HCCHCCBHFHGHFGG` | команда |
| `+0x7C` | `<EFCABGBCFBCAGBC>` | `float` | **Health, хп игрока!** |
| `+0x80` | `<GHBGDBBCEEEDAHE>` | `AimController*` | |
| `+0x88` | `<BFAGDADAFBFCFHE>` | `WeaponryController*` | |
| `+0x90` | `<CCEGFHHCBFDAGBG>` | `MecanimController*` | |
| `+0x98` | `<GBEBBBCDABBBGBG>` | `MovementController*` | |
| `+0xA0` | `<EBFBDFFEFHFHGCF>` | `ArmsAnimationController*` | |
| `+0xA8` | `<FEHEEGFGBEEHAHF>` | `PlayerHitController*` | **HIT-КОНТРОЛЛЕР** |
| `+0xB0` | `<DFDCHDBDBBABAHB>` | `PlayerMaterialController*` | |
| `+0xB8` | `<FFCHFAFCGABDGDE>` | `PlayerOcclusionController*` | |
| `+0xC0` | `<EEAEADBACBDGBGG>` | `NetworkController*` | |
| `+0xC8` | `<AHBHAGDHEBGAEHA>` | `ArmsLodGroup` | |
| `+0xD0` | `<DDFDFHCFGAEAAHE>` | `PlayerCharacterView` | |
| `+0xD8` | `<FEHHDEDCEFCDGBG>` | `bool` | |
| `+0xD9` | `<DDEBGDFFDCBDAHC>` | `bool` | |
| `+0xDC` | `<EEEEGAGEACBHEGE>` | `float` | |
| `+0xE0` | `<GFDDDHCFDEGDCDA>` | `PlayerSoundController*` | |
| `+0xE8` | `GEAHBBBHFECADHC` | `PlayerMainCamera` | |
| `+0xF0` | `GGDCGDBBFHHCABG` | `PlayerFPSCamera` | |
| `+0xF8` | `DECCBDEEHGADBBD` | `PlayerMarkerTrigger` | |
| `+0x100` | `HGABCFFEBCFBGDB` | `Transform` | |
| `+0x108` | `EEBDHHDHEGBHABC` | `Controller[]` | массив всех контроллеров |
| `+0x110` | `CCEFBBFHDGBAHDA` | `Dict<Type, Controller>` | |
| `+0x118` | `AFGCDHHCACEFABH` | `CharacterController` | |
| `+0x120` | `<HAEHADGEHFAEFGB>` | `SkinnedMeshLodGroup` | |
| `+0x128` | `<GACCBFDDBBEDDBB>` | `CharacterLodGroup` | |
| `+0x130` | `<HCHFDEEHAEAECDA>` | `bool` | |
| `+0x131` | `<GACABHEEDGBFHDB>` | `bool` | |
| `+0x134` | `<DHACBFAFGFEGFHH>` | `GECFBGHHEAEHDCD` | |
| `+0x138` | `BEEHBBFAHDFBBHE` | `Nullable<int>` | |
| `+0x140` | `EAAAEEAFCECBECE` | `Nullable<bool>` | |
| `+0x144` | `EBGGFCHECFEBHCB` | `Nullable<int>` | |
| `+0x150` | `<FECHGCBAEBGDACH>` | `PhotonView*` | |
| `+0x158` | `<BFGEGCBEABBHBHG>` | `int` | viewID |
| `+0x15C` | `<DGEBFCDHFFCEEBH>` | `int` | |
| `+0x160` | `<GHFBDECDCDFEGEA>` | `PhotonPlayer*` | **ЛОКАЛЬНЫЙ PhotonPlayer** |

---

## 6. HitController

**Строка:** `39725` · Базовый хит-контроллер (`abstract`)
**Наследуется от:** `Controller` (наследует `+0x28..+0x52`)

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x58` | `_config` | `PlayerHitboxConfig` | |
| `+0x60` | `DDEAGDDABHFBGAD` | `Dict<Bip, PlayerHitbox>` | |
| `+0x68` | `HGCGCHEDCFFCHHF` | `PlayerOcclusionController*` | |
| `+0x70` | `FEGFGAGFGGDDBBF` | `MonoBehaviourRef<PlayerController>` | |
| `+0x80` | `FHBFFGADFFHBCDF` | `bool` | |
| `+0x88` | `GCFBBBFBCABFEAC` | `Action` | |
| `+0x90` | `GDDFBDHECCBHECF` | `Action<HECABHGEHCEGBGC>` | |
| `+0x98` | `<EGFFHGGGCDBDDGA>` | `CapsuleCollider` | |

---

## 7. PlayerHitController

**Строка:** `40101` · Хит-контроллер в мультиплеере (кто нанёс / получил урон)
**Наследуется от:** `HitController → Controller`

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0xA0` | `HitAffectCurve` | `AnimationCurve` | эффект попадания |
| `+0xA8` | `FHHHHECFAHADBGF` | `float` | |
| `+0xAC` | `DBFBACHECEBDFEA` | `float` | |
| `+0xB0` | `ACBHCBAFGECAACA` | `float` | |
| `+0xB4` | `DCGDDAHBEHACAAG` | `bool` | |
| `+0xB8` | `BFEEFAAGBAAEDFB` | `Action<HECABHGEHCEGBGC>` | |
| `+0xC0` | `BEBBHBCHGAGAGBH` | `Action<PlayerController, HECABHGEHCEGBGC>` | |
| `+0xC8` | `CFCBFHHFAFGEHEC` | `Action` | |
| `+0xD0` | `DDGDBCABAGFFEHA` | `PhotonPlayer*` | **ИСТОЧНИК последнего урона!** |
| `+0xD8` | `HBCAGCFAEFEGADA` | `FHAHBEEDFCFHEHD[]` | |
| `+0xE0` | `EFEGAHEFEEGGCFB` | `CCEGCEAGBFGABBA` | |
| `+0xE8` | `EBHBCBFDFADCGBF` | `HECABHGEHCEGBGC` | данные последнего хита |
| `+0xF0` | `CBAHEHCDAHHAAGA` | `object[]` | |
| `+0xF8` | `CHHFACBEGCEACGA` | `Action<HECABHGEHCEGBGC, HBAHEABCDEHDHDD, PhotonPlayer, PhotonPlayer>` | ивент хита |
| `+0x100` | `LocalTime` | `float` | |
| `+0x104` | `FFFEDGBBFHEEFEF` | `bool` | |

---

## 8. DummyHitController

**Строка:** `39548` · Хит-контроллер для локальной симуляции (тренировка / локальные хиты)
**Наследуется от:** `HitController → Controller`

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0xA0` | `_bipMap` | `BipedMap` | |
| `+0xA8` | `_hitPoints` | `List<Vector2>` | позиции хитов на экране |
| `+0xB0` | `BDGCCECAHEGDDBH` | `DDAAGCEGFEHFHCE` | |
| `+0xB8` | `ECCFDCBBBGEBACC` | `Vector3[]` | |
| `+0xC0` | `EDFCBCGEAEEFEAH` | `Action` | |
| `+0xC8` | `BAHBCAEBAHGCBHD` | `float` | |
| `+0xCC` | `FEEBBBGACGADDDA` | `float` | |
| `+0xD0` | `HDHGCACBHGHGHGF` | `float` | |
| `+0xD4` | `HABAGDEFGEAGBBC` | `float` | |
| `+0xD8` | `FEHFEFACFGFEGEA` | `bool` | |
| `+0xDC` | `AFDAHECAFDGHBHD` | `int` | |
| `+0xE0` | `ECHEDDBCFEGHAED` | `Transform` | |
| `+0xE8` | `HEFDFDDFCDDHGDH` | `HitMarkerView` | красный X на экране |
| `+0xF0` | `GHABHDHGGBCDGAE` | `Action<HECABHGEHCEGBGC>` | колбэк хита |
| `+0xF8` | `OnKillAction` | `Action<EEDHFEHFEBAGGHA>` | когда убил |
| `+0x100` | `OnHitAction` | `Action<HECABHGEHCEGBGC, bool, bool>` | колбэк: данные хита, крит?, что-то |

---

## 9. PropHitController

**Строка:** `161628` · Хит-контроллер для объектов (гранаты, пропсы)
**Наследуется от:** `PlayerHitController → HitController → Controller`

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x108` | `DDAGGHFCBGGDDHH` | `BipedMap` | |
| `+0x110` | `EDEEEGDEFFHEABE` | `string` | |
| `+0x118` | `HAEHFDECCACDGGB` | `bool` | |
| `+0x119` | `<ADGCDADDADHFEBC>` | `bool` | |
| `+0x120` | `<FHFFEBFFEBBDAFB>` | `HGEDDAAGFBHDEDD` | |

---

## 10. WeaponryController

**Строка:** `33851` · Контроллер оружия (слоты, переключение)
**Наследуется от:** `Controller`

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x58` | `HDBEEDCEEHFCAEA` | `Dict<byte, WeaponController>` | оружие по слоту |
| `+0x60` | `EAEEAAAAFGEAGFD` | `List<WeaponController>` | |
| `+0x68` | `FHGAFACHEDAFHHB` | `List<byte>` | |
| `+0x70` | `FAFCGDAAEFGDGEB` | `List<CFHHCFCBDHAGFEG>` | |
| `+0x78` | `CGGHEGADBDBCBGF` | `PlayerController*` | владелец |
| `+0x80` | `EGHEEFACDDGHAFF` | `MecanimController*` | |
| `+0x88` | `CHFCFDDABEEDGDD` | `byte` | текущий слот |
| `+0x89` | `BDHAGGGAGHFGCDA` | `bool` | |
| `+0x90` | `<HGFFHFHABBGBGHH>` | `WeaponPickupController` | |
| `+0x98` | `<GGGGAEAHDBBGAEF>` | `KitController` | |
| `+0xA0` | `<CAAFCAFCCDEEHFD>` | `WeaponController*` | **текущее оружие!** |
| `+0xA8` | `<HGFHFGFFBFEDCCB>` | `bool` | IsReloading? |
| `+0xA9` | `<AAHDHAHCAFBDGGB>` | `bool` | |
| `+0xAC` | `<GAFBDAEACCBBFDC>` | `float` | |
| `+0xB0` | `<HCFDCFGHFFFGEFE>` | `float` | |
| `+0xB8` | `HFHCGEHGADFACBB` | `WeaponManager` | |

---

## 11. WeaponController

**Строка:** `68515` · Конкретное оружие (ствол, магазин, параметры стрельбы) (`abstract`)
**Наследуется от:** `MonoBehaviour`

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x20` | `BFBCFFFBFFCECAF` | `PlayerController*` | владелец |
| `+0x28` | `CEDDEEEBFDFDBHF` | `MecanimController*` | |
| `+0x30` | `AABHDFHCHGEBFBE` | `WeaponAnimationController` | |
| `+0x38` | `AHGBBFAGCABCCHA` | `WeaponAnimationParameters` | |
| `+0x40` | `EADBCDHDEECCFED` | `VisibilityState` | |
| `+0x44` | `ACEEFDGFDGADHEH` | `GECFBGHHEAEHDCD` | |
| `+0x48` | `GFHAGBCEADDEGGH` | `Action` | |
| `+0x50` | `EABAHDFAGGBAGDC` | `Action` | |
| `+0x58` | `HFHHFDDFGEDGADC` | `Action` | |
| `+0x60` | `GABDBECGEHFHEFG` | `Transform` | |
| `+0x68` | `CHHHEFHCFGHFDBB` | `Controller[]` | |
| `+0x70` | `DABABEHFADEBEDB` | `ABAFACGDGHHHAHH` | |
| `+0x78` | `FCDHDDFADHFEEBF` | `ABAFACGDGHHHAHH` | |
| `+0x80` | `<HAAHGHDHAGGEBGB>` | `float` | **FireRate**, скорострельность |
| `+0x84` | `<DFCHGEHGCDCHDBA>` | `float` | **ReloadDuration**, время перезарядки |
| `+0x88` | `<EHFBDCCCHFHEDGC>` | `WeaponLodGroup` | |
| `+0x90` | `<BHDDCEFEGFEBBDD>` | `HandleState` | |
| `+0x94` | `<FBBCHHHCACHFCAD>` | `byte` | **SlotIndex**, номер слота |
| `+0x98` | `<DCHECBGAEDAEAAE>` | `string` | название оружия |
| `+0xA0` | `<DHDDGFDCAACCBDG>` | `int` | **AmmoInMagazine**, патроны в магазине! |
| `+0xA4` | `<FEFEBADGACBFFBA>` | `int` | **AmmoReserve**, запас патронов! |
| `+0xA8` | `<BAHFDCEHBDHBCFB>` | `WeaponParameters` | параметры оружия |
| `+0xB0` | `<ECGAHBEADFCFFEE>` | `AEBDDBCGGFEAHHG` | |
| `+0xB8` | `<BBDHBCHGHHDGDBB>` | `WeaponMap` | |
| `+0xC0` | `<GEFGEEHEHHFHHFF>` | `byte` | |
| `+0xC1` | `<HFGAGFDABBEEDBB>` | `bool` | **IsFiring?** стреляет ли сейчас? |
| `+0xC8` | `<ECHGDGBHCGDCBDH>` | `WeaponStatTrackController` | effects/stat трекер |
| `+0xD0` | `<GCFBFAEFCDGDDHE>` | `WeaponMaterialController` | |
| `+0xD8` | `<EFGDCDAHAFFEEGB>` | `WeaponPatternControllerComponent` | shots контроллер |
| `+0xE0` | `<GHACHBCBBBGCDGD>` | `ADBEGAFBCEHHBFB` | PassData |
| `+0xE8` | `BBFEAAEFCHFHGDF` | `GCBDEEFDHAGGBDE` | |
| `+0xF0` | `AGHGABHAEHDHCGG` | `GEAFAGDHCDHACGA` | |
| `+0xF8` | `EEHHFACEGCEGFGD` | `GDCHHHDGEDHGCGG` | |

> **Новое в v0.39.1:** поля `+0xC8`, `+0xD0`, `+0xD8` теперь имеют конкретные типы вместо обобщённого `T` (`WeaponStatTrackController`, `WeaponMaterialController`, `WeaponPatternControllerComponent`).

---

## 12. MovementController

**Строка:** `37531` · Контроллер передвижения
**Наследуется от:** `Controller`

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x58` | `FDCGGAGDBDBGAAB` | `PlayerController*` | владелец |
| `+0x60` | `FACDDDHCCBEFAAD` | `PlayerOcclusionController*` | |
| `+0x68` | `_neverIdle` | `bool` | |
| `+0x70` | `<CEHEGGFCECHFBCG>` | `Transform` | корень персонажа |
| `+0x78` | `<AACGGBCHHHAFFHD>` | `GFCECCCDBFCABFA` | |
| `+0x80` | `<GDDEADBECCFEAGF>` | `float` | скорость передвижения? |
| `+0x84` | `<AFHBHACHBFFEAGD>` | `float` | |
| `+0x88` | `<EGCFBCADBFCDGBA>` | `CharacterController` | |
| `+0x90` | `<ABBDBGGECCAAAAC>` | `Trigger` | |
| `+0x98` | `DEAEGEGEADHFEEE` | `BGABCHGAFHDEBCG[]` | |
| `+0xA0` | `EAECADFFGEBCCEG` | `GEAADDGADGGGGFG` | |
| `+0xA8` | `translationParameters` | `PlayerTranslationParameters` | |
| `+0xB0` | `translationData` | `FABHEBAHBGAAADG` | |
| `+0xB8` | `CFDGGGFGDEEEGAH` | `DEDHBHGCEGGBBDG` | |
| `+0xC0` | `characterTransform` | `Transform` | |
| `+0xC8` | `<HCEAFAACABCHDBD>` | `MecanimController*` | |
| `+0xD0` | `CGHDEBEEBAFADCC` | `float` | |
| `+0xD8` | `ECGAHBHCGAGBDDF` | `List<...>` | |
| `+0xE0` | `FEHDDBFGGFBHAAD` | `List<...>` | |
| `+0xE8` | `GHEHCDEDFGBFGDA` | `FEAFCHCCHEAFFAE<...>[]` | |

---

## 13. AimController

**Строка:** `40828` · Контроллер прицеливания (Aim / FOV)
**Наследуется от:** `Controller`

| Offset | Поле | Тип | Описание |
|--------|------|-----|----------|
| `+0x53` | `_overrideSpineRotation` | `bool` | |
| `+0x54` | `GBGEFEHHDHGADAE` | `ABHBFBAACDGEBHH` | |
| `+0x58` | `sensitivityX` | `float` | чувствительность X |
| `+0x5C` | `sensitivityY` | `float` | чувствительность Y |
| `+0x60` | `minimumX` | `float` | |
| `+0x64` | `maximumX` | `float` | |
| `+0x68` | `FPSP_go` | `Transform` | |
| `+0x70` | `spineDirector` | `Transform` | |
| `+0x78` | `FPSCamera` | `Transform` | FPS камера |
| `+0x80` | `camTransform` | `Transform` | трансформ камеры |
| `+0x88` | `aimingParameters` | `AimingParameters` | параметры прицеливания |
| `+0x90` | `aimingData` | `CGHDEGEFCDDFGHE` | |
| `+0x98` | `interpolatorsBunch` | `InterpolatorsBunch` | интерполяторы |
| `+0xA0` | `tuningParams` | `TuningParams` | параметры тюнинга |
| `+0xA8` | `_headDampingSpeed` | `float` | |
| `+0xB0` | `BECFEHADDBCECBC` | `PlayerController*` | |
| `+0xB8` | `EHGHFFEEHBHEGGA` | `MovementController*` | |
| `+0xC0` | `EGGBBFBAAGEEHBE` | `Transform` | |
| `+0xC8` | `GECEBDDDEDEHDCC` | `MecanimController*` | |
| `+0xD0` | `CGAGHGGFFCFGHGD` | `Transform` | |
| `+0xD8` | `FDEFEBCGGBDADAB` | `bool` | |
| `+0xE0` | `AECEDDHEABGDFHC` | `EFHFAEADHEFDHBB` | |
| `+0xE8` | `AFFCDGBBFACFCAF` | `StateSimple<GECFBGHHEAEHDCD>` | |
| `+0xF0` | `FCHFBACFCEFDFAF` | `Vector3` | |
| `+0x100` | `HAHAFHDEFDDDCBH` | `StateSimple<WeaponOffsetState>` | |
| `+0x108` | `BDFAEBFFFEBFCGA` | `StateSimple<MoveState>` | |
| `+0x110` | `DCGAEGFDCFDCAGC` | `TransformTR` | |
| `+0x118` | `EHCGCECBAFBFHBB` | `TransformTR` | |

> **Новое в v0.39.1:** ниже `+0x118` добавлен блок дополнительных полей (Pose-буферы, WeaponAnimationParameters, WeaponryController*, кватернионы и флаги тюнинга). В v0.39.0 класс заканчивался на `+0x118`. Расширенная часть (для справки):
>
> | Offset | Поле | Тип |
> |--------|------|-----|
> | `+0x120` | `DDEBABCFHAGBAAH` | `Pose` |
> | `+0x13C` | `HDDDDCCHABDHFFH` | `Pose` |
> | `+0x158` | `FCBGDHHACDBADDC` | `Pose` |
> | `+0x174` | `GDHDEHGGCDAFGFF` | `Pose` |
> | `+0x190` | `HHBHEDACEFEABDF` | `Pose` |
> | `+0x1B0` | `CEDEDHFHDBCDCCG` | `WeaponAnimationParameters` |
> | `+0x1B8` | `CCCBGGDFGDFHBCH` | `ACGCAAFAFHACFDB` |
> | `+0x1C0` | `ABEDBECEFGBDAEB` | `Action` |
> | `+0x1C8` | `FCEDHAAEADGGBHB` | `Action` |
> | `+0x1D0` | `AABBHBGCCBAGACA` | `Action` |
> | `+0x1D8` | `AACGABAFCEGADGB` | `Action` |
> | `+0x1E0` | `<HBCFBFCHBECEDFG>` | `bool` |
> | `+0x1E4` | `<HDGGGHBCHEHFAAG>` | `float` |
> | `+0x1E8` | `<HFCHCGAECHCBFCD>` | `float` |
> | `+0x1F0` | `BBEDHEFDHFDECCC` | `BBFBBEHGHDEBCCG` |
> | `+0x1F8` | `GEGECABGCBHDCGD` | `float` |
> | `+0x1FC` | `BGBCBFHDBFAFDFA` | `float` |
> | `+0x200` | `CEGBEFEHCFCCFED` | `FCFHGECECBDBDEA[]` |
> | `+0x208` | `GEAAGEEHDAGEGAE` | `WeaponryController*` |
> | `+0x210` | `ABEDCFFGBBGBHEG` | `Quaternion` |
> | `+0x220` | `ToolPivotTuningEnabled` | `bool` |
> | `+0x221` | `SpineRotationEnabled` | `bool` |
> | `+0x224` | `FHACGDBGCDADGCG` | `Vector3` |
> | `+0x230` | `CBCHCBEDFDAAEGG` | `Vector3` |
> | `+0x23C` | `EDDHFEDHBAFCFDD` | `Vector3` |
> | `+0x248` | `AFBBDAADDDBEEGH` | `Pose` |

---

## 14. PlayerMainCamera

**Строка:** `32710` · Основная камера игрока

> См. полный класс в `dump.cs` по указанной строке.

---

## 15. PlayerSoundController

**Строка:** `35292` · Звуки игрока (шаги, попадания, и т.д.)
**Наследуется от:** `Controller`

> См. полный класс в `dump.cs` по указанной строке.

---

## 16. NetworkController

**Строка:** `31755` · Сетевой контроллер игрока
**Наследуется от:** `Controller`

> См. полный класс в `dump.cs` по указанной строке.

---

## Ключевые оффсеты (для чита — самые важные)

| Выражение | Назначение |
|-----------|-----------|
| `PhotonPlayer+0x18` | `actorID` (уникальный ID игрока) |
| `PlayerController+0x7C` | `Health` (здоровье) |
| `PlayerController+0xA8` | `PlayerHitController*` (хит-контроллер) |
| `PlayerController+0x160` | `PhotonPlayer*` (локальный PhotonPlayer) |
| `WeaponryController+0xA0` | `WeaponController*` (текущее оружие) |
| `WeaponController+0xA0` | `AmmoInMagazine` (патроны в магазине) |
| `WeaponController+0xA4` | `AmmoReserve` (запас патронов) |
| `WeaponController+0xC1` | `IsFiring?` (стреляет ли?) |
| `PlayerHitController+0xD0` | `PhotonPlayer*` (ИСТОЧНИК урона) |
| `PlayerHitController+0xF8` | `Action` hit event |
| `Controller+0x40` | `PhotonPlayer*` (владелец контроллера) |

---

## HOWTO — Проверка, что урон нанёс именно ты (hitsound)

```c
// Получить свой actor ID
local_actor_id = Read<int>(LocalPlayer + 0x160 → PhotonPlayer + 0x18)

// Когда у врага упало HP:
hit_ctrl   = Read<ptr>(EnemyPlayer + 0xA8)     // PlayerHitController
src_photon = Read<ptr>(hit_ctrl + 0xD0)        // source PhotonPlayer
src_id     = Read<int>(src_photon + 0x18)      // source actorID

if (src_id == local_actor_id) {
    // Это Я нанёс урон → играем hitsound!
}
```

### `Controller+0x40` — PhotonPlayer (OWNER)

Если `Owner == LocalPlayer` → это наш контроллер.

---

## Сводка изменений v0.39.0 → v0.39.1

- **Смещения полей:** без изменений — все оффсеты в классах `PhotonPlayer`, `ObjectPlayer`, `CharacterPlayer`, `Controller`, `PlayerController`, `HitController`, `PlayerHitController`, `DummyHitController`, `PropHitController`, `WeaponryController`, `WeaponController`, `MovementController`, `AimController` идентичны предыдущей версии.
- **Номера строк дампа:** изменились (классы переместились в `dump.cs`), актуальные значения приведены в таблице выше.
- **Обфусцированные имена:** пересгенерированы — обновлены в таблицах.
- **`WeaponController`:** поля `+0xC8 / +0xD0 / +0xD8` получили конкретные типы (`WeaponStatTrackController`, `WeaponMaterialController`, `WeaponPatternControllerComponent`) вместо обобщённого `T`.
- **`AimController`:** класс расширен ниже `+0x118` — добавлены Pose-буферы, `WeaponryController*`, флаги тюнинга и др. (см. расширенную таблицу в секции 13).
