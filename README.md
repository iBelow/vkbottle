# 

<h1 align="center">VKBottle - high quality VK Tool</h1>
<p align="center"><a href="https://pypi.org/project/vkbottle/"><img alt="downloads" src="https://img.shields.io/static/v1?label=pypi%20package&message=0.13&color=brightgreen"></a> <a href="https://github.com/timoniq/vkbottle"><img src="https://img.shields.io/static/v1?label=version&message=opensource&color=yellow" alt="service-test status"></a> <a href="https://vk.me/join/AJQ1d7fBUBM_800lhEe_AwJj"><img src="https://img.shields.io/static/v1?message=VK%20Chat&label=&color=blue"></a>
    <blockquote>VKBottle - это многофункциональный модуль для работы с VK Api и создания ботов</blockquote>
</p>
<hr>

### Установка
1) С помощью установщика pip из PyPi:

   ```sh
   pip install vkbottle
   ```

2) С помощью установщика pip из GitHub: 
   
   ```sh
   pip install https://github.com/timoniq/vkbottle/archive/master.zip --upgrade
   ```
   
### Фишки

- Удобная и быстрая доставка сообщений через regex
- Быстрый API враппер
- Быстрый LongPoll фреймворк для ботов
- Маленький объем кода для достижения сложных конструкций
- Полностью асинхронно
- Множество встроенных помощников: Branches для цепей событий, VBML для разметки сообщений и так далее

***

### Longpoll

```python
from vkbottle import Bot, Message

bot = Bot('my-token', 123, debug=True)


@bot.on.message('My name is <name>', lower=True)
async def wrapper(ans: Message, name):
    await ans('Hello, {}'.format(name))


bot.run_polling()
```

### Callback

```python
from vkbottle import Bot, Message
from aiohttp.web import RouteTableDef, Application, Request, run_app


app = Application()
routes = RouteTableDef()
bot = Bot('my-token', 123, debug=True, secret="SecretKey")

@routes.get('/bot')
async def executor(request: Request):
    return await bot.emulate(event=dict(request.query), confirmation_token="ConfirmationToken")

@bot.on.message('test', lower=True)
async def wrapper():
    return "test"

app.add_routes(routes)
run_app(app)
```

Больше примеров в папке [/examples](./examples)

### Документация

Полная документация:  

* [Русская версия документации](docs/README.RU.md)  
в ней же можно найти документацию по валидаторам, веткам

* [Дополнительная документация - русская версия](docs/FrameworkAPI.md)  
там можно найти все остальную информацию, уровень прочтения требует профессионального понимания фреймворка

# Contributing

ПР поддерживаются! Мне приятно видеть ваш вклад в развитие библиотеки  
Задавайте вопросы в блоке Issues и в чате VK!

## Лицензия

Copyright © 2019 [timoniq](https://github.com/timoniq).  
Этот проект имеет [GPL-3.0](./LICENSE.txt) лицензию.
