# SimpleCam

Минималистичная Android-камера для записи видео с профессиональным управлением звуком.

## Возможности

- Запись видео 1280×720 @ 30fps, 6 Mbps H.264
- Выбор аудио-источника (встроенный/USB/Bluetooth)
- Регулировка усиления ±20 dB + Soft Clip
- Ручной/автофокус с барабанным управлением и Focus Assist
- Zoom-рычаг с пружинным возвратом
- **VU-метр dBFS с Peak Hold**
- **Осциллограф с Rising-Edge триггером (2048 сэмплов)**
- **Спектр-анализатор FFT 2048 точек, окно Ханна**

## Сборка через GitHub Actions

### 1. Залить репозиторий на GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_NAME/SimpleCam.git
git push -u origin main
```

### 2. Запустить сборку

- Перейдите в **Actions → Build APK**
- Нажмите **Run workflow**
- Через ~3-5 минут в артефактах появятся:
  - `SimpleCam-debug-N` — debug APK (сразу устанавливается)
  - `SimpleCam-release-N` — release APK (unsigned)

### 3. Подписанный Release APK (опционально)

Создайте keystore:
```bash
keytool -genkeypair -v \
  -keystore release.jks \
  -keyalg RSA -keysize 2048 \
  -validity 10000 \
  -alias simplecam
```

Добавьте секреты в **Settings → Secrets and variables → Actions**:

| Секрет | Значение |
|---|---|
| `KEYSTORE_BASE64` | `base64 -w0 release.jks` |
| `KEY_ALIAS` | `simplecam` |
| `STORE_PASSWORD` | пароль от keystore |
| `KEY_PASSWORD` | пароль от ключа |

## Локальная сборка

Требования: **Android Studio** или **JDK 17 + Android SDK**.

```bash
# Генерация wrapper (один раз)
gradle wrapper --gradle-version 8.7

# Debug APK
./gradlew assembleDebug

# APK будет в:
# app/build/outputs/apk/debug/app-debug.apk
```

## Системные требования устройства

- Android 6.0+ (API 23)
- Camera2 API
- Микрофон
