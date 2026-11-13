# OrangeBeat

Android-приложение для прослушивания своей музыки

## Возможности

- **Плеер**: play/pause, перемотка, следующий/предыдущий, перемешивание, повтор.
- **Фоновое воспроизведение**: уведомление в шторке, управление с экрана блокировки.
- **Добавление своей музыки**: выбор аудиофайлов через системный проводник (SAF), без копирования файлов.
- **Сканирование устройства**: все аудио из MediaStore одним нажатием.
- **Поиск**: живой поиск по названию, исполнителю и альбому (с поддержкой кириллицы).
- **Плейлисты**: создание, удаление, добавление треков, просмотр содержимого.
- **Избранное** и удаление треков из библиотеки.

## Стек

| Технология | Версия | Роль |
| --- | --- | --- |
| Kotlin | 2.0.21 | Язык |
| Jetpack Compose (BOM) | 2024.10.01 | UI |
| Media3 / ExoPlayer | 1.5.0 | Воспроизведение и MediaSession |
| Room | 2.6.1 | Локальная база (треки, плейлисты) |
| Coil | 2.7.0 | Обложки |
| Navigation Compose | 2.8.4 | Экраны |

Минимальная версия Android: **7.0 (API 24)**, целевая: **15 (API 35)**.

## Запуск

### Android Studio

1. File → Open → папка проекта.
2. Дождаться Gradle Sync.
3. Run ▶ на устройстве или эмуляторе.

### Консоль

```
$env:JAVA_HOME = "C:\Program Files\Android\Android Studio\jbr"
$env:ANDROID_HOME = "C:\Android\Sdk"
.\gradlew.bat assembleDebug
```

APK: `app/build/outputs/apk/debug/app-debug.apk`

> **Важно про путь проекта.** Если текущая папка содержит кириллицу. То **юнит-тесты** в таком пути падают с `ClassNotFoundException` — это ограничение JVM, не кода. Если планируете гонять тесты, перенесите проект в путь без нелатинских символов, например `C:\dev\orangebeat`.

## Структура

```
app/src/main/java/com/orangebeat/music/
├── MainActivity.kt          точка входа, разрешения
├── OrangeBeatApp.kt         Application + ручной DI
├── ui/
│   ├── theme/               цвета, градиенты, форма, типографика
│   ├── components/          Buttons, SearchBar, TrackRow, MiniPlayer
│   ├── screens/             Home, Search, Library, Playlists, Player
│   └── viewmodel/           MusicViewModel
├── player/                  PlaybackService, PlaybackController, PlayerState
└── data/
    ├── local/               Room: TrackEntity, PlaylistEntity, DAO, MusicDatabase
    ├── scanner/             MediaStoreScanner, FileImporter
    ├── repository/          MusicRepository
    └── model/               Track, Playlist
```

## 
