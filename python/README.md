Объяснение кода оплаты
Импортируемые библиотеки
import requests
Функция get_pay_link
Эта функция создает ссылку для оплаты и возвращает её вместе с ID инвойса.
Параметры:
•
amount: сумма для оплаты в USDT.
Возвращает:
•
Ссылка для оплаты.
•
ID инвойса.
Описание:
1.
Сначала формируем HTTP-заголовки, включая токен API для аутентификации.
2.
Определяем тело запроса с суммой и валютой (USDT).
3.
Отправляем POST-запрос к API.
4.
Если запрос успешный (response.ok), парсим JSON-ответ и возвращаем ссылку для оплаты и ID инвойса.
5.
Если запрос не успешный, возвращаем None, None.
def get_pay_link(amount):
headers = {"Crypto-Pay-API-Token": config.API_TOKEN} data = {"asset": "USDT", "amount": amount}
response = requests.post('https://pay.crypt.bot/api/createInvoice', headers= headers, json=data)
if response.ok:
response_data = response.json()
return response_data['result']['pay_url'], response_data['result']['invo ice_id']
return None, None
Функция check_payment_status
Эта функция проверяет статус оплаты по ID инвойса.
Параметры:
•
invoice_id: ID инвойса.
Возвращает:
•
JSON-ответ от API с данными об инвойсах или None в случае ошибки.
Описание:
1. Формируем HTTP-заголовки, включая токен API и тип содержимого.
2. Отправляем POST-запрос к API для получения информации о всех инвойсах.
3. Если запрос успешный (response.ok), возвращаем JSON-ответ.
4. Если запрос не успешный, выводим ошибку и возвращаем None.
def check_payment_status(invoice_id):
headers = {
"Crypto-Pay-API-Token": config.API_TOKEN,
"Content-Type": "application/json"
}
response = requests.post('https://pay.crypt.bot/api/getInvoices', headers=he
aders, json={})
}")
if response.ok:
return response.json()
else:
print(f"Ошибка при запросе к API: {response.status_code}, {response.text
return None
Заключение
В этом архиве также есть код бота, который при оплате будет отправлять документ. Вы
можете посмотреть, как он работает и вырезать часть кода, отвечающую за оплату и
проверку оплаты.