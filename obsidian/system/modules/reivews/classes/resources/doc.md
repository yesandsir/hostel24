документация по дополнительным ресурсам. таблицы, доки, картинки и другое для модуля system/modules/reviews

дерево
gooTables (google tables) - таблицы гугла
excTables (microsoft excel tables) - таблицы икселя


содержание{
gooTable/get_reviews 

sheets (разделитель это линия вот эта вот)
______________________________
requests_to_commendants - создан для работы при работе с запросами посылаемым комендантам с целью получить ответ информирующих о жильцах конкретного хостела.
использует протокол system/protocols/reviews/get_peoples/get_comendant и механизм использования system/protocols/mechanisms/subordinate_request_response

лист состоит из столбцов :

адрес - адрес хостела
комендант - комендант хостела по адресу
номер телефона коменданта - рабочий номер телефона коменданта
способ коммуникации - приложение (тг, фб, сотовая связь) для обмена запрос ответами с конкретным комендантом 
дата запроса - дата отправки запроса
ФИО жильца - фио жильца
период проживания - период проживания жильца
номер телефона жильца - номер телефона жильца
примечание - информация о жильце которую комендант посчитает нужным сказать

и служебных столбцов :
служебка - обозначает служебный столбец
дата запроса с предыдущего месяца - дата запроса с предыдущего месяца
E4 - формула расчета цвета фона для столбца "дата запроса"

столбцы имеют свойства и форматирование :

адрес - форматирование неизменно в процессе всего периода использования. содержимое ячейки автоматически переносится в следующие листы через формулу.
комендант - форматирование неизменно в процессе всего периода использования.
номер телефона коменданта - форматирование неизменно в процессе всего периода использования.
способ коммуникации - форматирование неизменно.
дата запроса - форматирование таково. красный фон, запрос просрочен, не отправлен вовремя. желтый фон, запрос отправлен, ожидается ответ. зеленый фон, ответ получен. цвет ячейки автоматически изменяется высчитывая дату последнего запроса и вводимый вручную требуемый период. так считывает, есть ли какая либо информация в ячейках с жильцами, если нету то желтый, если есть то зеленый.
ФИО жильца - форматирование неизменно. автоматических переносится в следующий лист raw_revievs.
период проживания - форматирование неизменно. переносится в следующий лист raw_reviews.
номер телефона жильца - форматирование неизменно. переносится в следующий лист raw_reviews.
примечание - форматирование неизменно. пока что никак не используется

формулы :
формулы находятся справа от обрабатываемой информации

дата запроса - светофор
""
_________________________________
raw_reviews - создан для сбора сырых отзывов храня в себе значения таких столбцов

ФИО жильца - фио жильца
период проживания - период проживания
номер телефона жильца - номер телефона жильца
примечание - примечание коменданта об этом жильце
отзыв - мнение жильца о месте жительства

эти столбцы не имеют никакого форматирования и имеют такие свойства
ФИО жильца - переносится автоматически с листа requests_to_comendants
период проживания - переносится автоматически с листа requests_to_comendants
номер телефона жильца - переносится автоматически с листа requests_to_comendants
примечание - переносится автоматически с листа requests_to_comendants

этот столбец не имеет свойств но требует ручного изменения форматирования фона ячейки.
красный - плохой отзыв
зеленый - хороший отзыв
желтый - и хороший и плохой
серый - в отзыве нету полезной информации/жилец не пошел на контакт
белый - звонка не производилось

если жилец не взял трубку - ставится дата последнего звонка. в последующем по формуле и вручную выставленном периоде повторного звонка, формула при превышении периода ожидания до повторного звонка меняет цвет ячейки на черный и пишет в служебной ячейке соотношение ответивших на звонок и не ответивших, которые и являются черными ячейками.

фио, номер, адрес, период заполняется не абы как, а правильно. большие буквы. дд.мм.гггг. +380... . Вул. Житомирьска 21, кв. 50 .

_______________________________
preproccessed_raw_review - эта таблица является промежуточным звеном между использованием модуля отзывов с другими модулями, например в модуль с задачей переработки старых хостелов под другой контингент людей.

имеются такие столбцы :

служебные :
светофор нужды в обработке - показатель использующий даты выполнения работы в предыдущем месяце и дате выполнения работ в текущем месяце с использованием вручную установленного периода частоты обработки
заполненность - определяет заполненность по каждой категории. есть ли впринципе по этому информация какая либо
нестача информации для исследований - считает новые строки в каждой ячейке по категории, что бы собрать задачу дизайнерам и строителям для новых/старых обьектов
нестача информации впринципе - считает количество символов в ячейке с отзывом в формате обычного текста, из которого можно еще что то вытащить если постараться.

обычные
адрес - адрес хостела
дата выполнения работы в предыдущем месяце - дата выполнения работы в предыдущем месяце по работе с этим адресом на этом листе
дата выполнения работ - дата выполнения работ по этому адресу в последний раз этого месяца
текстом - привычный ранее отзыв описанный текстом, своими словами так сказать, но обобщенно от всех дильцов
ответ - вписывается ответ соответствующей категории из столбца "по категориям"
общая рецензия - вывод по каждому аспекту проживания (местоположение, обслуживание, комфорт, общая обстановка)

_____________________________
reviews_dashboard - статистика по трем выше описанным листам


}


формулы сделаны через нажатие на ячейку - формат - условное форматирование
потом опишу процесс с картинками
чисто уже блять док по разработке пишу еще книгу напишу и буду богатым папой