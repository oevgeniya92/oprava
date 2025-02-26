# oprava

### `config.py`
```python
COINGECKO_API_KEY = 'YOUR_COINGECKO_API_KEY_HERE'
CRYPTOCURRENCIES = ['bitcoin', 'ethereum', 'litecoin']
```

### `utils.py`
```python
def format_currency_data(crypto_data):
    """
    Форматирует данные о криптовалютах для удобного отображения.
    :param crypto_data: список словарей с данными о криптовалютах
    :return: строка с отформатированными данными
    """
    output = ''
    for coin in crypto_data:
        if coin['symbol'].lower() in CRYPTOCURRENCIES:
            output += f"{coin['name']} ({coin['symbol']}) - Цена: ${coin['quote']['USD']['price']:.2f}\n"
    return output
```

### `tests.py`
```python
import unittest
from crypto_tracker import fetch_crypto_data, format_currency_data
from config import COINGECKO_API_KEY


class CryptoTrackerTests(unittest.TestCase):

    def test_fetch_crypto_data(self):
        data = fetch_crypto_data(COINGECKO_API_KEY)
        self.assertIsNotNone(data)
        self.assertTrue(isinstance(data, list))

    def test_format_currency_data(self):
        mock_data = [
            {"id": 1, "name": "Bitcoin", "symbol": "BTC", "quote": {"USD": {"price": 40000}}},
            {"id": 2, "name": "Ethereum", "symbol": "ETH", "quote": {"USD": {"price": 3000}}}
        ]
        result = format_currency_data(mock_data)
        expected_output = "Bitcoin (BTC) - Цена: $40000.00\nEthereum (ETH) - Цена: $3000.00\n"
        self.assertEqual(result, expected_output)


if __name__ == "__main__":
    unittest.main()
```

### `requirements.txt`
```
requests==2.26.0
```

### `.gitignore`
```
# Скрытые файлы операционной системы
.DS_Store
Thumbs.db

# Файлы виртуального окружения Python
venv/
*.pyc
__pycache__/
