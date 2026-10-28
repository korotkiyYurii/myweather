# Свіжі дані кожні 15 хвилин (обов’язково, якщо потрібна актуальність)

SaveEcoBot **блокує** запити з браузера (CORS).  
Публічні CORS-проксі **не працюють** з цим сайтом.  
Єдиний надійний шлях для GitHub Pages — **GitHub Actions** качає JSON у `data/`.

Вбудований `schedule` GitHub Free часто **не запускається годинами**.

## Налаштування cron-job.org (безкоштовно)

### 1. Токен GitHub
GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)  
Створіть token з правом **`repo`** (і `workflow`, якщо питає).

### 2. Нове завдання на https://cron-job.org

| Поле | Значення |
|------|----------|
| Title | myweather update |
| URL | `https://api.github.com/repos/korotkiyYurii/myweather/actions/workflows/update-weather.yml/dispatches` |
| Schedule | Every 15 minutes |
| Request method | **POST** |

**Request headers:**
```
Accept: application/vnd.github+json
Authorization: Bearer ВАШ_GITHUB_TOKEN
X-GitHub-Api-Version: 2022-11-28
Content-Type: application/json
```

**Request body:**
```json
{"ref":"main"}
```

### 3. Перевірка
- cron-job.org → History: має бути HTTP 204  
- GitHub → Actions: з’являється run *Update SaveEcoBot Data*  
- Через ~1 хв після run — Pages перезбирається, на сайті новий час вимірювання  

### 4. Зараз (разово)
GitHub → Actions → Update SaveEcoBot Data → **Run workflow**
