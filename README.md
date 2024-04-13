# **Вступление**
___
### Тelegram-bot, на машином обучение с использованием scikit-learn





## Требования к установке
```python
   pip install python-telegram-bot, scikit-learn, numpy , telebot , nlk , pandas
   
```
___
## **Добавление библиотек**
```python
from telegram import Bot
import telegram
from telegram.ext import Updater, MessageHandler, Filters
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.svm import LinearSVC
import numpy as np
``` 
*Импортируем свой токен в проэкт: ```bot = Bot("Your_Token") ```* 

# Создаем бот
```python
bot = telegram.Bot(token=TOKEN)
updater = Updater(token=TOKEN, use_context=True)
dispatcher = updater.dispatcher
```

#### Пример данных для обучения модели
```python
X_train = np.array(["какой сегодня день?", "какого цвета небо?", "какой у вас любимый цвет?","Привет", "Ку", "Здравствуйте" , "Прив","Пока", "Увидимся позже", "до свидания","спасибо", "спасибо тебе", "Это очень полезно", "Спасибо за помощь", "Как дела?"])
y_train = np.array(["Сегодня вторник.", "Небо синее.", "Мой любимый цвет зелены","Здравствуйте", "Привет", "Здравствуй","Привет,Как дела?","Увидимся позже", "Хорошего дня", "Пока! Возвращайся снова","Рад помочь!", "В любое время!", "С удовольствием", "У меня все хорошо", "У меня все хорошо","Всегда рад помочь"])

```
#### Векторизация текста
```python
vectorizer = TfidfVectorizer()
X_train_vectorized = vectorizer.fit_transform(X_train)
```

#### Обучение модели
```python
model = LinearSVC()
model.fit(X_train_vectorized, y_train)
```

#### Обработчик сообщений
```python
def reply(update, context):
    input_text = update.message.text
    input_vectorized = vectorizer.transform([input_text])
    prediction = model.predict(input_vectorized)
    context.bot.send_message(chat_id=update.message.chat_id, text=prediction[0])
```

#### Добавляем обработчик сообщений
```python
dispatcher.add_handler(MessageHandler(Filters.text & ~Filters.command, reply))
```



# **Конфигурация**
Add [Bot_Father](https://t.me/botfather)
___

## Поддержка
[Telegram](https://web.telegram.org/a/#5153165332)
___

