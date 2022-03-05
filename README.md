Ціль - інформаційна атака з використанням наявних злитих російських email адрес (~2.5млн.)

1. Встановіть Docker 
3. Скачайте базу імейлів https://mega.nz/file/nWw3jAqI#6mkrGhaV1GoyLqBpAi-QHAyUIHbcCSMjZce5Es5XKxU 
4. Надайте доступ у налаштуваннях докеру до папки/диску на якому розархівовано базу -> settings -> resources -> file sharing 
5. Створіть скриньку(и) у gmail
6. Включіть 2-факторну аутентифікацію -> Обліковий запис - Безпека - Вхід в обліковий запис Google - Двохетапна перевірка
7. Створіть пароль додатка -> Обліковий запис - Безпека - Вхід в обліковий запис Google - Паролі додатків
8. Скачайте https://github.com/bayraktar4ik/email-bomber/blob/main/docker-compose.yaml
9. змініть відповідно до своїх налаштувань (приклад для gmail, якщо створюєте скриньку у іншому сервісі - smtp налаштування теж мають бути змынені)

 environment:
      - mail.smtp.auth=true
      - mail.smtp.starttls.enable=true
      - mail.smtp.host=smtp.gmail.com
      - mail.smtp.port=587
      - mail.smtp.ssl.trust=smtp.gmail.com
      - email=rusinfo200@gmail.com <- новостворена пошта
      - password=tjprlhvkoqtcqlib <- пароль додатку
      - subject="Военное положение в России" <- заголовок листа
      - body=/dir/Collection_ANTIWAR/111111.html <- тіло листа (/dir/ залишити як є)
      - emails=/dir/mail_RU_part1.txt <- список імейлів 
      - bombSize=50 <- кількість адресатів за раз
      - chunk=4 <- номер чанку (кожен чанк - 500 імейлів (поточний ліміт gmail на відправку за добу). Розраховується як N/500. Тобто для 1го файлу ~ 4839 чанків)
    volumes:
      - b:\rus_email_spam\fuckers_emails_1\:/dir <- шлях до директорії з імейлами і html
      - /target/bayraktar-email-0.0.1-SNAPSHOT.jar:/ROOT.war

10. виконати з командного рядка (у тій же директорії де знаходиться файл docker-compose.yaml)
    docker-compose up -d

