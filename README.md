# 🧰 No-Code Architects Toolkit API (Форк)

Устали тратить тысячи долларов на подписки, чтобы поддерживать все свои автоматизации?  
А что, если есть **бесплатная альтернатива**?

**No-Code Architects Toolkit API** — это **100% бесплатный** инструмент на Python (Flask), предназначенный для работы с медиа и автоматизации.

---

## 🚀 Что умеет этот API?

- 🎧 Конвертация аудиофайлов  
- 📝 Расшифровка аудио/видео  
- 🌍 Перевод между языками  
- 🎬 Добавление субтитров к видео  
- 🧠 Комплексная медиаобработка  
- ☁️ Работа с файлами на Google Drive, Amazon S3, Google Cloud Storage и Dropbox

API легко разворачивается с помощью **Docker**, поддерживается на **Google Cloud**, **Digital Ocean** и других платформах.

🧩 Способен заменить дорогие сервисы: ChatGPT Whisper, Cloud Convert, Createomate, JSON2Video, PDF.co, Placid, OCodeKit и др.

---

## ❓Нужна помощь?

Присоединяйтесь к моему [**телеграм-каналу**](https://t.me/+VY7IEk4sR7AxOWY0) — задавайте любые вопросы, получайте поддержку и делитесь опытом.

---

## 📡 API Эндпоинты

Каждый эндпоинт сопровождается валидацией данных и полной документацией.

<details>
<summary><strong>🎧 Аудио</strong></summary>

- `/v1/audio/concatenate` — Объединяет несколько аудиофайлов в один  
</details>

<details>
<summary><strong>👨‍💻 Код</strong></summary>

- `/v1/code/execute/python` — Выполняет Python-код удалённо и возвращает результат  
</details>

<details>
<summary><strong>🎞 FFmpeg</strong></summary>

- `/v1/ffmpeg/compose` — Гибкий интерфейс для сложной медиаобработки через FFmpeg  
</details>

<details>
<summary><strong>🖼 Изображения</strong></summary>

- `/v1/image/convert/video` — Превращает изображение в видео  
</details>

<details>
<summary><strong>🎥 Медиа</strong></summary>

- `/v1/media/convert` — Конвертирует формат медиа  
- `/v1/media/convert/mp3` — Конвертирует в MP3  
- `/v1/BETA/media/download` — Загружает медиа через yt-dlp  
- `/v1/media/feedback` — Интерфейс для обратной связи  
- `/v1/media/transcribe` — Расшифровка/перевод по ссылке  
- `/v1/media/silence` — Поиск тишины в аудио/видео  
- `/v1/media/metadata` — Извлечение метаданных  
</details>

<details>
<summary><strong>☁️ S3</strong></summary>

- `/v1/s3/upload` — Загрузка файла в S3 по URL  
</details>

<details>
<summary><strong>🧪 Toolkit</strong></summary>

- `/v1/toolkit/authenticate` — Аутентификация по API-ключу  
- `/v1/toolkit/test` — Проверка доступности API  
- `/v1/toolkit/job/status` — Статус конкретного задания  
- `/v1/toolkit/jobs/status` — Статусы всех заданий  
</details>

<details>
<summary><strong>📹 Видео</strong></summary>

- `/v1/video/caption` — Добавление субтитров  
- `/v1/video/concatenate` — Объединение видео  
- `/v1/video/thumbnail` — Получение превью  
- `/v1/video/cut` — Вырезка фрагмента  
- `/v1/video/split` — Разделение по времени  
- `/v1/video/trim` — Обрезка по диапазону  
</details>

---

## 🐳 Сборка и запуск через Docker

### 🔨 Сборка образа

```bash
docker build -t no-code-architects-toolkit .
```

---

## ⚙️ Переменные окружения

### Обязательная

| Переменная | Назначение |
|-----------|-------------|
| `API_KEY` | Аутентификация API |

---

### S3-совместимое хранилище (если используется)

| Переменная | Описание |
|-----------|----------|
| `S3_ENDPOINT_URL` | URL эндпоинта |
| `S3_ACCESS_KEY` | Ключ доступа |
| `S3_SECRET_KEY` | Секретный ключ |
| `S3_BUCKET_NAME` | Название бакета |
| `S3_REGION` | Регион (можно `"None"`) |

---

### Google Cloud Storage (если используется)

| Переменная | Описание |
|-----------|----------|
| `GCP_SA_CREDENTIALS` | JSON ключ от GCP Service Account |
| `GCP_BUCKET_NAME` | Название бакета |

---

### Производительность

| Переменная | Назначение | Рекомендации |
|------------|------------|---------------|
| `MAX_QUEUE_LENGTH` | Очередь задач | Например, 10 |
| `GUNICORN_WORKERS` | Кол-во процессов | 2–4× CPU |
| `GUNICORN_TIMEOUT` | Таймаут обработки | Лучше 300–600 сек |

---

### Хранилище

| Переменная | Значение по умолчанию |
|------------|-------------------------|
| `LOCAL_STORAGE_PATH` | `/tmp` |

⚠️ **Важно:** переменные S3/GCP обязательны, если используете соответствующее хранилище.

---

### ▶️ Пример запуска Docker-контейнера

```bash
docker run -d -p 8080:8080 \
  -e API_KEY=your_api_key \

  # Пример: S3
  #-e S3_ENDPOINT_URL=https://nyc3.digitaloceanspaces.com \
  #-e S3_ACCESS_KEY=your_access_key \
  #-e S3_SECRET_KEY=your_secret_key \
  #-e S3_BUCKET_NAME=your_bucket_name \
  #-e S3_REGION=nyc3 \

  # Или GCP
  #-e GCP_SA_CREDENTIALS='{"your":"service_account_json"}' \
  #-e GCP_BUCKET_NAME=your_gcs_bucket_name \

  -e LOCAL_STORAGE_PATH=/tmp \
  -e MAX_QUEUE_LENGTH=10 \
  -e GUNICORN_WORKERS=4 \
  -e GUNICORN_TIMEOUT=300 \
  no-code-architects-toolkit
```
