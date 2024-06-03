import telebot
import config
from telebot import types

bot = telebot.TeleBot(config.TOKEN)

previous_menu = {}

user_contacts = {}

# ПРИВЕТСТВИЕ
@bot.message_handler(commands=['start'])
def welcome(message):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item1 = types.InlineKeyboardButton("Меню", callback_data="menu")
    item2 = types.InlineKeyboardButton("Наши Соцсети", callback_data="sosmed")
    item3 = types.InlineKeyboardButton("О Нас", callback_data="about")
    markup.add(item1, item2, item3)

    photo_path1 = "hello.jpg"
    bot.send_photo(message.chat.id, open(photo_path1, 'rb'), caption="🌟 Добро пожаловать, {0.first_name}, в кафе 'Pronto Bistro'! 🌟 \n\nЗдесь, в уютном атмосферном заведении, каждый гость находит что-то особенное для себя. Мы гордимся предлагаемым разнообразием блюд, внимательным обслуживанием и уютной атмосферой.\n\n🍽️ У нас вы найдете все, чтобы насладиться вкусом каждого момента: от изысканных пицц и ароматного кофе до нежных десертов, соблазняющих своим вкусом и ароматом.\n\n🛵 Желаете заказать на вынос или сделать заказ с доставкой? Наш телеграм-бот станет вашим верным помощником в этом! Исследуйте наше меню, выбирайте изысканные блюда и оформляйте заказ в несколько кликов!\n\n🌿 Наслаждайтесь вкусом момента в кафе 'Pronto Bistro'!".format(message.from_user, bot.get_me()),
                   parse_mode='html', reply_markup=markup)

#НАШИ СОЦСЕТИ
@bot.callback_query_handler(func=lambda call: call.data == "sosmed")
def show_med(call):
        markup = types.InlineKeyboardMarkup(row_width=2)
        item40 = types.InlineKeyboardButton("Назад", callback_data="back")
        markup.add(item40)

        previous_menu[call.message.chat.id] = "menu"
        photo_path4 = "inst.png"
        bot.send_photo(call.message.chat.id, open(photo_path4, 'rb'), caption ="Рады сообщить, что мы теперь активны в социальных сетях.😉\n\nСледите за нами, чтобы быть в курсе последних новостей и обновлений.\n\nСоциальные сети:\nВК: https://vk.com/id735769540 \nInst: https://www.instagram.com/bistroprontospb/", reply_markup=markup)

#О НАС
@bot.callback_query_handler(func=lambda call: call.data == "about")
def show_about(call):
        markup = types.InlineKeyboardMarkup(row_width=2)
        item41 = types.InlineKeyboardButton("Назад", callback_data="back")
        markup.add(item41)

        previous_menu[call.message.chat.id] = "menu"
        photo_path = 'pronto.webp'
        bot.send_photo(call.message.chat.id, open(photo_path, 'rb'), caption=" Приветствуем вас в нашем уютном кафе!😊 \nПредоставляем подробную информацию о нашем заведении:\n\n• Название: Pronto Bistro.\n\n• Местонахождение: Питер, Лиговский проспект 271.\n\n• Часы работы: 9:00 - 21:00.\n\n•Контактный телефон: +79642394514.\n\n•Телеграм владельца: @sokolenok60", reply_markup=markup)

# МЕНЮ
@bot.callback_query_handler(func=lambda call: call.data == "menu")
def show_menu(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item5 = types.InlineKeyboardButton("Пицца", callback_data="pizza")
    item6 = types.InlineKeyboardButton("Дессерты", callback_data="dessert")
    item0 = types.InlineKeyboardButton("Кофе", callback_data = "coffee")
    item7 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item5, item6, item0, item7)

    previous_menu[call.message.chat.id] = "menu"
    photo_path2 = "menu.png"
    bot.send_photo(call.message.chat.id, open(photo_path2, 'rb'),
                   caption='''🍴 Готовы насладиться вкусом наших блюд? 🍴

У нас в кафе "Pronto Bistro" широкий выбор изысканных блюд, которые наверняка удовлетворят ваши вкусовые предпочтения! Выберите что-то из нашего меню и насладитесь вкусом вкуснейших пицц, нежных десертов и ароматного кофе.

🍕 Пицца - Попробуйте наши разнообразные варианты пиццы, от классической Маргариты до изысканной Пепперони.

🍰 Десерты - Развлеките себя нежными десертами, начиная от мороженого и заканчивая аппетитными круассанами и тортиками.

☕ Кофе - Приятное дополнение к вашему обеду или ужину - наш ароматный кофе в различных вариантах.

Выберите что-то на свой вкус и оформите заказ прямо сейчас! Наш телеграм-бот готов вам помочь. Просто нажмите на кнопку и выберите то, что вам по вкусу.

Приятного аппетита!''',
                   reply_markup=markup)

# ВЫБОР ПИЦЦЫ
@bot.callback_query_handler(func=lambda call: call.data == "pizza")
def show_pizza_menu(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item12 = types.InlineKeyboardButton("Пеперони", callback_data="peperoni")
    item13 = types.InlineKeyboardButton("Маргарита", callback_data="margarita")
    item14 = types.InlineKeyboardButton("Четыре Сыра", callback_data="forechees")
    item15 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item12, item13, item14, item15)

    previous_menu[call.message.chat.id] = "menu"
    photo_path4 = "pizza.png"
    bot.send_photo(call.message.chat.id, open(photo_path4, 'rb'), caption='''🍕 Пиццы

Пепперони

Острая и аппетитная пицца с пепперони, сочным томатным соусом и обильным слоем сыра. Идеальный выбор для ценителей острого вкуса и аромата.
Цена: 400 руб.

Маргарита

Классическая пицца с тонким хрустящим тестом, покрытая ароматным томатным соусом, свежими кусочками моцареллы и томатами. Простота и вкус в каждом кусочке!
Цена: 400 руб.

Четыре Сыра

Пицца, в которой слились воедино четыре сыра: моцарелла, пармезан, гауда и дор-блю. Нежный сливочный вкус, сгущенный ароматом итальянских сыров.
Цена: 400 руб.
Выберите свою любимую пиццу и наслаждайтесь неповторимым вкусом вместе с кафе "Pronto Bistro"!''', reply_markup=markup)

# ВЫБОР ДЕСЕРТА
@bot.callback_query_handler(func=lambda call: call.data == "dessert")
def show_dessert_menu(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item8 = types.InlineKeyboardButton("Мороженое", callback_data="icecream")
    item9 = types.InlineKeyboardButton("Круассан", callback_data="croissant")
    item10 = types.InlineKeyboardButton("Тортик", callback_data="cake")
    item11 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item8, item9, item10, item11)

    previous_menu[call.message.chat.id] = "menu"
    photo_path3 = "dessert.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path3, 'rb'), caption='''🍰 Десерты

Мороженое

Насладитесь разнообразием вкусов в нашем мороженом! От классического ванильного до экзотических фруктовых и шоколадных вариантов. Освежающее удовольствие в каждой ложке!
Цена: 250 руб.

Круассан

Хрустящие круассаны с различными начинками, в том числе с нежным шоколадом. Идеальный выбор для завтрака или перекуса в любое время дня!
Цена: 150 руб.

Тортик

Маленькие тортики, созданные для истинных гурманов! Наслаждайтесь богатым вкусом и неповторимым ароматом наших десертов.
Цена: 100 руб.''', reply_markup=markup)

# ВЫБОР КОФЕ
@bot.callback_query_handler(func=lambda call: call.data == "coffee")
def show_coffee_menu(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item01 = types.InlineKeyboardButton("Черное Кофе", callback_data="black")
    item02 = types.InlineKeyboardButton("Капучино", callback_data="capuchino")
    item03 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item01, item02, item03)

    previous_menu[call.message.chat.id] = "menu"
    photo_path01 = "coffee.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path01, 'rb'), caption='''☕ Кофе

Черное Кофе

Насладитесь насыщенным ароматом и богатым вкусом чашечки нашего черного кофе. Идеальное начало дня или приятное дополнение к вашему обеду!
Цена: 100 руб.

Капучино

Нежное сочетание эспрессо и молока, украшенное аппетитной молочной пенкой. Отличный выбор для любителей кофейных напитков с мягким вкусом и ароматом.
Цена: 150 руб.
Выберите свой любимый кофейный напиток и наслаждайтесь атмосферой кафе "Pronto Bistro"!

''', reply_markup=markup)

# ПЕПЕРОНИ
@bot.callback_query_handler(func=lambda call: call.data == "peperoni")
def show_peperoni(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item19 = types.InlineKeyboardButton("Оформить заказ", callback_data="order1")
    item16 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item19, item16)

    previous_menu[call.message.chat.id] = "pizza"
    photo_path10 = "peproni.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path10, 'rb'), caption='''🍕 "Пицца "Пепперони"

Описание: Аппетитная и острая пицца, приготовленная с использованием острой пепперони, ароматного томатного соуса и обильного слоя сыра. Каждый кусочек этой пиццы наполнен ярким вкусом и ароматом, который оставит в вас незабываемое впечатление.

Цена: 400 руб.

Выберите пиццу "Пепперони" и насладитесь острым и сочным вкусом.''', reply_markup=markup)

# МАРГАРИТА
@bot.callback_query_handler(func=lambda call: call.data == "margarita")
def show_margarita(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item20 = types.InlineKeyboardButton("Оформить заказ", callback_data="order2")
    item17 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item20, item17)

    previous_menu[call.message.chat.id] = "pizza"
    photo_path11 = "margarita.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path11, 'rb'), caption='''🍕 Пицца "Маргарита"

Описание: Классическая и всеми любимая пицца с тонким хрустящим тестом, покрытая ароматным томатным соусом и свежими кусочками моцареллы. Дополнительно украшена свежими помидорами. Простота и вкус в каждом кусочке!

Цена: 400 руб.

Выберите пиццу "Маргарита" и насладитесь классическим итальянским вкусом''', reply_markup=markup)

# ЧЕТЫРЕ СЫРА
@bot.callback_query_handler(func=lambda call: call.data == "forechees")
def show_forechees(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item21 = types.InlineKeyboardButton("Оформить заказ", callback_data="order3")
    item18 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item21, item18)

    previous_menu[call.message.chat.id] = "pizza"
    photo_path12 = "4chees.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path12, 'rb'), caption='''🍕 Пицца "Четыре Сыра"

Описание: Изысканная пицца, приготовленная из смеси четырех разных сыров: моцарелла, пармезан, гауда и дор-блю. Нежное сочетание сливочного и сырного вкусов, которое подарит вам неповторимый гастрономический опыт.

Цена: 400 руб.

Выберите пиццу "Четыре Сыра" и насладитесь богатством сырного вкуса''', reply_markup=markup)

# МОРОЖЕНОЕ
@bot.callback_query_handler(func=lambda call: call.data == "icecream")
def show_icecream(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item50 = types.InlineKeyboardButton("Оформить заказ", callback_data="order4")
    item52 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item50, item52)

    previous_menu[call.message.chat.id] = "dessert"
    photo_path14 = "icecream.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path14, 'rb'), caption='''🍨 Мороженое

Описание: Насладитесь освежающими и ароматными вкусами нашего мороженого. У нас в ассортименте представлены различные варианты: от классического ванильного до экзотических фруктовых и шоколадных. Идеальное лакомство для охлаждения в жаркий день или просто для того, чтобы порадовать себя.

Цена: 250 руб.

Выберите ваш любимый вкус мороженого и насладитесь его неповторимым вкусом''', reply_markup=markup)

# КРУАССАН
@bot.callback_query_handler(func=lambda call: call.data == "croissant")
def show_croissant(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item53 = types.InlineKeyboardButton("Оформить заказ", callback_data="order5")
    item54 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item53, item54)

    previous_menu[call.message.chat.id] = "dessert"
    photo_path15 = "cruassan.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path15, 'rb'), caption='''🥐 Круассан

Описание: Наслаждайтесь хрустящими круассанами с различными начинками, в том числе с нежным шоколадом. Это отличный выбор для завтрака или перекуса в любое время дня. Каждый кусочек круассана — это нежное сочетание теста, сливочного масла и ароматной начинки, которое подарит вам момент удовольствия.

Цена: 150 руб.

Выберите круассан с вашей любимой начинкой и насладитесь его вкусом''', reply_markup=markup)

# ТОРТИК
@bot.callback_query_handler(func=lambda call: call.data == "cake")
def show_cake(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item55 = types.InlineKeyboardButton("Оформить заказ", callback_data="order6")
    item56 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item55, item56)

    previous_menu[call.message.chat.id] = "cake"
    photo_path16 = "cake.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path16, 'rb'), caption='''🎂 Тортик

Описание: Насладитесь божественным вкусом наших маленьких тортиков, созданных для истинных гурманов. Каждый тортик приготовлен с любовью и вниманием к деталям, чтобы подарить вам незабываемый вкусовой опыт. Выберите свой любимый вариант и порадуйте себя вкуснейшим десертом!

Цена: 100 руб.

Выберите тортик по вашему вкусу и наслаждайтесь его неповторимым вкусом''', reply_markup=markup)

# ЧЕРНОЕ КОФЕ
@bot.callback_query_handler(func=lambda call: call.data == "black")
def show_black(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item001 = types.InlineKeyboardButton("Оформить заказ", callback_data="order01")
    item002 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item001, item002)

    previous_menu[call.message.chat.id] = "coffee"
    photo_path001 = "black.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path001, 'rb'), caption='''☕ Черное Кофе

Описание: Насладитесь насыщенным ароматом и богатым вкусом чашечки нашего черного кофе. Этот классический напиток подарит вам бодрость и энергию на целый день. Свежесть и аромат свежемолотого кофе — вот что делает наше черное кофе идеальным выбором для всех любителей кофеинового бодрствования!

Цена: 100 руб.

Выберите черное кофе и насладитесь его насыщенным вкусом и ароматом''', reply_markup=markup)

# КАПУЧИНО
@bot.callback_query_handler(func=lambda call: call.data == "capuchino")
def show_capuchino(call):
    markup = types.InlineKeyboardMarkup(row_width=2)
    item003 = types.InlineKeyboardButton("Оформить заказ", callback_data="order02")
    item004 = types.InlineKeyboardButton("Назад", callback_data="back")
    markup.add(item003, item004)

    previous_menu[call.message.chat.id] = "coffee"
    photo_path002 = "capuchino.jpg"
    bot.send_photo(call.message.chat.id, open(photo_path002, 'rb'), caption='''☕ Капучино

Описание: Нежное сочетание эспрессо, молока и аппетитной молочной пенки делает наше капучино идеальным выбором для любителей кофейных напитков с мягким вкусом и ароматом. Насладитесь утренним ритуалом или перекусите в течение дня, наслаждаясь богатым вкусом капучино из кафе "Pronto Bistro".

Цена: 150 руб.

Выберите капучино и насладитесь его нежным вкусом и ароматом''', reply_markup=markup)

#Получения контактной информации
@bot.message_handler(content_types=['contact'])
def contact_received(message):
    try:
        contact_info = f"Имя: {message.from_user.first_name}\n"
        contact_info += f"Контактный номер: {message.contact.phone_number}\n"
        contact_info += f"Юзернейм: @{message.from_user.username}\n"

        bot.send_message('600981959', contact_info)
        bot.reply_to(message, "Ваш номер успешно получен! Теперь, если не затруднит, отправьте ваше местоположение, чтобы мы могли быстрее доставить ваш заказ.")
    except Exception as e:
        bot.reply_to(message, "Что-то пошло не так. Пожалуйста, попробуйте снова.")

#Получения геолокации
@bot.message_handler(content_types=['location'])
def location_received(message):
    try:
        location_info = f"Геолокация: {message.location.latitude},{message.location.longitude}\n"
        location_info += f"Юзернейм: @{message.from_user.username}\n"

        bot.send_message('600981959', location_info)
        bot.reply_to(message, '''Мы благодарим вас за предоставленную геолокацию! 🌍

Ваш заказ будет доставлен в течение одного до двух часов после совершения оплаты. 🚚

Наш сотрудник выйдет на связь с вами, чтобы подтвердить заказ и обсудить детали оплаты. 📞

Мы ценим ваше терпение и выбор нашего кафе! Спасибо! ☕''')
    except Exception as e:
        bot.reply_to(message, "Что-то пошло не так. Пожалуйста, попробуйте снова.")

#Кнопки для получиения Геолокации и номера телефона
@bot.callback_query_handler(func=lambda call: call.data in ["order1", "order2", "order3", "order4", "order5", "order6", "order01", "order02"])
def process_order(call):
    try:
        # Определение товара, который был заказан
        item_name = ""
        if call.data == "order1":
            item_name = '''Пицца Пеперони
Цена - 400Р'''
        elif call.data == "order2":
            item_name = '''Пицца Марагрита
Цена - 400Р'''
        elif call.data == "order3":
            item_name = '''Пицца Четыре Сыра
Цена - 400Р'''
        elif call.data == "order4":
            item_name = '''Мороженое  
Цена - 250Р'''
        elif call.data == "order5":
            item_name = '''Круассан 
Цена - 150Р'''
        elif call.data == "order6":
            item_name = '''Тортик  
Цена - 100Р'''
        elif call.data == "order01":
            item_name = '''Черное кофе
Цена - 100Р'''
        elif call.data == "order02":
            item_name = '''Капучино
Цена - 150Р'''
        
        # Отправка запроса на отправку контактной информации и геолокации
        markup = types.ReplyKeyboardMarkup(row_width=1, one_time_keyboard=True)
        contact_button = types.KeyboardButton("Отправить контакт", request_contact=True)
        location_button = types.KeyboardButton("Отправить геолокацию", request_location=True)

        markup.add(contact_button, location_button)

        msg = bot.send_message(call.message.chat.id, f'''📱 Для оформления заказа {item_name}, пожалуйста, отправьте ваш номер телефона:

Мы гарантируем конфиденциальность ваших данных и использование их исключительно для оформления заказа и связи с вами.

(Нажмите кнопку "Отправить контакт" на клавиатуре Telegram для автоматической отправки вашего номера телефона.)

📍 После отправки номера телефона, пожалуйста, поделитесь вашей геолокацией:

Это поможет нашим курьерам быстрее доставить ваш заказ по нужному адресу.

(Нажмите кнопку "Отправить геолокацию" на клавиатуре Telegram для автоматической отправки вашей текущей геолокации.)

Спасибо за ваше сотрудничество!''', reply_markup=markup)

        bot.register_next_step_handler(msg, lambda message: send_data(message, call.message, item_name))
    except Exception as e:
        bot.reply_to(call.message, "Что-то пошло не так. Пожалуйста, попробуйте снова.")

#Настройка кнопки Back (назад)
@bot.callback_query_handler(func=lambda call: call.data == "back")
def go_back(call):
    previous = previous_menu.get(call.message.chat.id)

    if previous == "menu":
        welcome(call.message)

    elif previous == "pizza":
        show_menu(call)

    elif previous == "sosmed":
        welcome(call.message)

    elif previous == "about":
        welcome(call.message)

    elif previous == "dessert":
        show_menu(call)
    
    elif previous == "coffee":
        show_menu(call)

# Функция отправки данных о заказе на мой аккаунт (XxaannaaxX)
def send_data(message, original_message, item_name):
    try:
        if message.contact:
            contact_info = f"Имя: {message.from_user.first_name}\n"
            contact_info += f"Контактный номер: {message.contact.phone_number}\n"
            contact_info += f"Юзернейм: @{message.from_user.username}\n"
            contact_info += f"Заказанный товар: {item_name}\n"

            bot.send_message('600981959', contact_info)
            bot.reply_to(original_message, "Ваш номер успешно получен! Теперь, если не затруднит, отправьте ваше местоположение, чтобы мы могли быстрее доставить ваш заказ.")

        elif message.location:
            location_info = f"Геолокация: Широта {message.location.latitude}, Долгота {message.location.longitude}\n"
            location_info += f"Юзернейм: @{message.from_user.username}\n"

            bot.send_message('600981959', location_info)
            bot.reply_to(original_message, '''Мы благодарим вас за предоставленную геолокацию! 🌍

Ваш заказ будет доставлен в течение одного до двух часов после совершения оплаты. 🚚

Наш сотрудник выйдет на связь с вами, чтобы подтвердить заказ и обсудить детали оплаты. 📞

Мы ценим ваше терпение и выбор нашего кафе! Спасибо! ☕''')

        else:
            bot.reply_to(original_message, "Не удалось определить тип данных. Пожалуйста, попробуйте еще раз.")
    except Exception as e:
        bot.reply_to(original_message, "Что-то пошло не так. Пожалуйста, попробуйте снова.")

bot.polling(none_stop=True, interval=0)
