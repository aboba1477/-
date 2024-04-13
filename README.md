# все нужные импорты
import telebot
import random
from telebot import types

# связь с ботом
bot = telebot.TeleBot("7184759483:AAHSa5sW7Mb9gm3g0TSU2a7YqEdrlm_4LeM")

# все нужные списки
ifd = [" довольно дешево! 👍", " неплохо! 👍", " а вы умеете выбирать товары по хорошей цене! 👍"]
ifD = [" дороговато! 😬", " хотелось бы подешевле! 🥲"]


@bot.message_handler(func=lambda message: True)
def handle_message(message):
    try:

        if message.text == '1488':
            bot.send_message(message.chat.id,
                             "ПОСХАЛОЧКАА ВКЛЮЧАЕМ ВЕНТИЛЯТОРЫ МЕДНЫЙ БЫЧОК УЖЕ ГРЕЕТСЯ 卐卐卐卐")  # посхалочка

        else:
            a = int(message.text)
            proc = a + a // 20
            otv = proc + proc // 20 + 45
            final_price = round(otv * 13.8 + 1000)  # подсчеты цены

            ifd2 = random.choice(ifd)  # выбирание случайного элемента из списков
            ifD2 = random.choice(ifD)

            if final_price < 30000:
                message_to_send = f"Итоговая цена составит {final_price} рублей 💵, {ifd2}"  # вывод если меньше 30к
            else:
                message_to_send = f"Итоговая цена составит {final_price} рублей 💵, {ifD2}"  # если больше

            # пока до конца не понимаю работу, добавление кнопок
            keyboard = types.InlineKeyboardMarkup()
            button1 = types.InlineKeyboardButton(text="Покупаю!", callback_data="button1")
            button2 = types.InlineKeyboardButton(text="Воздержусь", callback_data="button2")

            keyboard.row(button1, button2)
            bot.send_message(message.chat.id, message_to_send, reply_markup=keyboard)

    # если вводится не число
    except ValueError:
        bot.send_message(message.chat.id, "Привет! Введи цену в юанях, чтобы узнать сколько прийдется заплатить")


@bot.callback_query_handler(func=lambda call: True)
def handle_button_click(call):
    if call.data == "button1":
        bot.send_message(call.message.chat.id, "Отлично! Напиши продавцу @Pudge1234 🛍")
    elif call.data == "button2":
        bot.send_message(call.message.chat.id, "Хорошо, может в следующий раз! 😗")


# обязательный элемент для завершения работы бота
bot.polling()
