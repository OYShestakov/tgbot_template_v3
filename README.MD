Этот темплейт необходим для разработки телеграм ботов с помощью библиотеки [`aiogram v3.0+`](https://github.com/aiogram/aiogram/tree/dev-3.x).

### Для того, чтобы начать:
1. Скопируйте `.env.dist` в `.env` и заполните необходимые переменные.
2. Сделайте хендлеры.
3. **Docker:**
   1. Можете запустить сразу из Docker, если его нет, то [установите](https://docs.docker.com/get-docker/).
   2. Запустить по команде `docker-compose up`
4. **Без Docker:**
   1. Создать [venv](https://docs.python.org/3/library/venv.html)
   2. Установить зависимости requirements.txt: `pip install -r requirements.txt --pre`
   3. Запустить проект `python3 bot.py`


### Как создавать хендлеры:
Создайте модуль `you_name.py` в папке `handlers`.

Создайте роутер `you_name.py`.
```python
from aiogram import Router
user_router = Router()
```
Можно делать роутеры в одном модуле.
Можно регистрировать модули декораторами:
```python
@user_router.message(commands=["start"])
async def user_start(message):
    await message.reply("Привет, мир!")
```

Заходим в файл `bot.py` и дописываем все роутеры в него:
```python
from tgbot.handlers.admin import admin_router
from tgbot.handlers.echo import echo_router
from tgbot.handlers.user import user_router

...

async def main():
   
   ...

    for router in [
        admin_router,
        user_router,
        ...,
        echo_router,

    ]:
        dp.include_router(router)
```
