No-Code Architects Toolkit API fork

Устали тратить тысячи долларов на подписки для поддержки ваших автоматизаций? А что, если есть бесплатная альтернатива?

На 100% БЕСПЛАТНЫЙ No-Code Architects Toolkit API обрабатывает различные типы медиа. Он написан на Python с использованием Flask.

Что он умеет?
Этот API может:

Конвертировать аудиофайлы

Создавать расшифровки

Переводить контент между языками

Добавлять субтитры к видео

Выполнять сложную медиаобработку для создания контента

Управлять файлами на различных облачных сервисах, таких как Google Drive, Amazon S3, Google Cloud Storage и Dropbox

Его можно развернуть по-разному: через Docker, на Google Cloud, Digital Ocean и других системах, поддерживающих Docker.

Позволяет легко заменить платные сервисы вроде ChatGPT Whisper, Cloud Convert, Createomate, JSON2Video, PDF.co, Placid и OCodeKit.

Если у вас есть вопросы как этим пользоваться

Присоеденяйтесь в мой телеграм канал, и смело задавайте вопросы

https://t.me/+VY7IEk4sR7AxOWY0

API Эндпоинты
Каждый эндпоинт сопровождается валидацией данных и подробной документацией.

Аудио
/v1/audio/concatenate — Объединяет несколько аудиофайлов в один.

Код
/v1/code/execute/python — Выполняет Python-код удалённо и возвращает результат.

FFmpeg
/v1/ffmpeg/compose — Предоставляет гибкий интерфейс FFmpeg для сложной медиаобработки.

Изображения
/v1/image/convert/video — Преобразует изображение в видео с настройкой длительности и масштабирования.

Медиа
/v1/media/convert — Конвертирует медиафайлы с выбором кодека.

/v1/media/convert/mp3 — Конвертирует медиа в формат MP3.

/v1/BETA/media/download — Загружает медиа с онлайн-источников (использует yt-dlp).

/v1/media/feedback — Веб-интерфейс для обратной связи о медиа.

/v1/media/transcribe — Расшифровывает или переводит аудио/видео по ссылке.

/v1/media/silence — Находит участки тишины в медиафайле.

/v1/media/metadata — Извлекает метаданные: кодеки, разрешение, битрейт и т.д.

S3
/v1/s3/upload — Загружает файл в Amazon S3 с URL.

Toolkit
/v1/toolkit/authenticate — Аутентификация по API-ключу.

/v1/toolkit/test — Проверка работоспособности API.

/v1/toolkit/job/status — Получение статуса конкретного задания.

/v1/toolkit/jobs/status — Получение списка статусов всех заданий за определённый период.

Видео
/v1/video/caption — Добавляет субтитры к видео с настройкой стиля.

/v1/video/concatenate — Объединяет видеофайлы в один.

/v1/video/thumbnail — Получает кадр-превью из видео по таймстампу.

/v1/video/cut — Вырезает фрагмент из видео.

/v1/video/split — Делит видео на части по времени.

/v1/video/trim — Обрезает видео по заданному интервалу.

Сборка и запуск Docker
Сборка образа

docker build -t no-code-architects-toolkit .
Общие переменные окружения
API_KEY
Назначение: Аутентификация по API-ключу.

Обязателен: Да

Переменные для S3-совместимого хранилища
S3_ENDPOINT_URL — URL эндпоинта

S3_ACCESS_KEY — ключ доступа

S3_SECRET_KEY — секретный ключ

S3_BUCKET_NAME — название бакета

S3_REGION — регион (можно "None" для некоторых провайдеров)

Google Cloud Storage
GCP_SA_CREDENTIALS — JSON с данными аккаунта GCP

GCP_BUCKET_NAME — имя бакета GCP

Настройки производительности
MAX_QUEUE_LENGTH — Ограничение очереди задач (по умолчанию 0 — без лимита)

GUNICORN_WORKERS — Количество воркеров (рекомендуется 2–4× ядер CPU)

GUNICORN_TIMEOUT — Таймаут обработки (30 сек по умолчанию, лучше 300–600 для больших файлов)

Настройка хранения
LOCAL_STORAGE_PATH — Временная директория хранения файлов (по умолчанию: /tmp)

⚠️ Обязательно указывайте переменные в зависимости от выбранного облачного хранилища (GCP или S3). Без них API не запустится.

Запуск Docker-контейнера

docker run -d -p 8080:8080 \
  -e API_KEY=your_api_key \
  
  # Пример: S3-хранилище
  #-e S3_ENDPOINT_URL=https://nyc3.digitaloceanspaces.com \
  #-e S3_ACCESS_KEY=your_access_key \
  #-e S3_SECRET_KEY=your_secret_key \
  #-e S3_BUCKET_NAME=your_bucket_name \
  #-e S3_REGION=nyc3 \

  # Или Google Cloud
  #-e GCP_SA_CREDENTIALS='{"your":"service_account_json"}' \
  #-e GCP_BUCKET_NAME=your_gcs_bucket_name \

  -e LOCAL_STORAGE_PATH=/tmp \
  -e MAX_QUEUE_LENGTH=10 \
  -e GUNICORN_WORKERS=4 \
  -e GUNICORN_TIMEOUT=300 \
  no-code-architects-toolkit
  
