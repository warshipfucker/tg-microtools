import telebot
from telebot import types

# Создаем экземпляр бота, указывая ваш токен
bot = telebot.TeleBot("YOUR_TELEGRAM_BOT_TOKEN")

# Предварительно сформированный список referral codes
referral_codes = ['U05T21C5', '6H88BWUE', 'A1B2C3D4', 'X9Y8Z7W6']

# Ссылка на бота
base_url = "https://t.me/LumCity_bot?start="

# Словарь для хранения ссылок для каждого пользователя (вы можете использовать базу данных для более сложных приложений)
user_links = {}

# Обработчик команды /start
@bot.message_handler(commands=['start'])
def send_welcome(message):
    # Получаем уникальный referral code для пользователя из списка
    referral_code = referral_codes[len(user_links) % len(referral_codes)]
    # Создаем уникальную ссылку для пользователя и сохраняем ее в словаре
    user_links[message.chat.id] = base_url + referral_code
    # Отправляем приветственное сообщение с ссылкой
    bot.send_message(message.chat.id, f"Добро пожаловать в LumCity_bot! Нажмите на ссылку ниже для входа:\n{user_links[message.chat.id]}")

# Обработчик callback_query
@bot.callback_query_handler(func=lambda call: True)
def handle_callback_query(call):
    # Получаем ID пользователя, который сделал запрос
    user_id = call.message.chat.id
    # Обновляем ссылку в сообщении
    referral_code = referral_codes[len(user_links) % len(referral_codes)]
    updated_link = base_url + referral_code
    # Обновляем сообщение в канале с новой ссылкой
    bot.edit_message_text(chat_id=call.message.chat.id, message_id=call.message.message_id, text=f"Добро пожаловать в LumCity_bot! Нажмите на ссылку ниже для входа:\n{updated_link}")

# Запускаем бота
bot.polling()
