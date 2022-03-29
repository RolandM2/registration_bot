import telebot
from telebot import types

bot = telebot.TeleBot('Token')

user_data = []   # list of customer data


def step_name(message):
    child_name = message.text
    user_data.append(child_name)
    msg = bot.send_message(message.chat.id, text='Ok! How old is he?')
    bot.register_next_step_handler(msg, step_age)


def step_age(message):
    child_age = message.text
    user_data.append(child_age)
    bot.send_message(message.chat.id, text='Do you have a PC/Laptop for class?')
    markup = types.ReplyKeyboardMarkup(one_time_keyboard=True, resize_keyboard=True)
    itembtn1 = types.KeyboardButton('Yes')
    itembtn2 = types.KeyboardButton('No')
    markup.add(itembtn1, itembtn2)
    msg = bot.send_message(message.chat.id, text='Choose answer', reply_markup=markup)
    bot.register_next_step_handler(msg, step_comp)


def step_comp(message):
    comp = message.text
    if comp == 'Yes':   #checking for a computer
        user_data.append(comp)
        msg = bot.send_message(message.chat.id, text='Great! Last question. '
                                                     + 'Write your phone number:')
        bot.register_next_step_handler(msg, step_phone)
    else:
        bot.send_message(message.chat.id, text='Bed :( /n Classes are held online and a computer is required.')


def step_phone(message):
    phone = message.text
    user_data.append(phone)
    bot.send_message(message.chat.id, text='Fine! We will contact you and agree on the time of the lesson')
    bot.send_message(message.chat.id, text='See you!')


# if command /help, /start
@bot.message_handler(commands=['start', 'help'])
def start(message):
    bot.send_message(message.chat.id, text='Hi' 
                                           + message.from_user.first_name
                                           + ' You can sign up for your first free lesson here')
    msg = bot.send_message(message.chat.id, text='First, write your child name:')
    bot.register_next_step_handler(msg, step_name)


if __name__ == '__main__':
    bot.infinity_polling(timeout=10, long_polling_timeout=5)
