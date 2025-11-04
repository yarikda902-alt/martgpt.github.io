<!doctype html>
<html lang="ru">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Шифр Мартгпт</title>
  <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
    </style>
 </head>
 <body>
  <h1>Шифр Мартгпт</h1>
  <textarea id="inputText" rows="4" cols="50" placeholder="Введите текст..."></textarea>
  <br>
  <button onclick="encrypt()">Зашифровать</button>
  <h2>Результат:</h2>
  <p id="outputText"></p>
  <script>
        function encrypt() {
            const input = document.getElementById('inputText').value;
            let result = '';

            const englishAlphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
            const russianAlphabet = "абвгдежзийклмнопрстуфхцчшщъыьэюяАБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ";

            // Функция для шифрования
            function encodeChar(char) {
                let firstLetter = char === '' ? '' : char[0];  // Сохраняем первую букву

                // Шифрование оставшихся букв
                let rest = char.slice(1).split('').map(c => {
                    let isEnglish = englishAlphabet.includes(c);
                    let isRussian = russianAlphabet.includes(c);

                    // Шифр Цезаря сдвиг на 1
                    if (isEnglish) {
                        return String.fromCharCode(c.charCodeAt(0) + 1);
                    } else if (isRussian) {
                        return String.fromCharCode(c.charCodeAt(0) + 1);
                    }
                    return c;  // Если символ не в алфавите, оставляем как есть
                }).join('');

                // Применяем шифр Атбаша
                let atbash = '';
                for (let i = 0; i < rest.length; i++) {
                    let code;
                    if (englishAlphabet.includes(rest[i])) {
                        code = englishAlphabet.length - englishAlphabet.indexOf(rest[i]) - 1;
                        atbash += englishAlphabet[code];
                    } else if (russianAlphabet.includes(rest[i])) {
                        code = russianAlphabet.length - russianAlphabet.indexOf(rest[i]) - 1;
                        atbash += russianAlphabet[code];
                    } else {
                        atbash += rest[i]; // Если символ не в алфавите, оставляем как есть
                    }
                }

                return firstLetter + atbash;  // Соединяем первую букву с зашифрованным текстом
            }

            // Обрабатываем ввод
            const words = input.split(' ');
            words.forEach(word => {
                result += encodeChar(word) + ' ';
            });

            // Убираем последний пробел
            document.getElementById('outputText').textContent = result.trim();
        }
    </script>
 </body>
</html>
