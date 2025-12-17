# **Руководство разработчика по интеграции Tilda Publishing с Google Forms**

### **Настройка Tilda**

1. Перейдите на сайт Tilda.  
2. Нажмите «Настройка сайта».  
3. В боковом меню слева нажмите на пункт «Формы».
4. Выберите параметр «Google Sheets» для отправки данных с формы.  
5. Выдайте название таблице и папке.
6. Сохраните все указанные изменения.  
7. Подключите составленную форму к заявкам Tilda.

### **Настройка форм Tilda на Google диск**

1. Внутри google диска нажмите «Tilda Leads».  
2. Перейдите в указанный путь «Tilda\_Leads\_Test».  
3. Выберите «Расширения».  
4. Нажмите «Apps Script».  
5. Удалите все данные в открывшемся виртуальном окне.  
6. Впишите указанные данные в командую строку.

### **Основная функция для обработки новых заявок**
`function` `createSheetForNewLead`() {
  `try` {
    // Открываем основную таблицу
    `const` mainSpreadsheet = SpreadsheetApp.getActiveSpreadsheet();
    `const` mainSheet = mainSpreadsheet.getSheetByName(``"Лист1"``); _Укажите правильное имя листа_
    
    `const` data = mainSheet.getDataRange().getValues();
   
    // Проверяем, есть ли данные (кроме заголовков)
    `if` (data.length < 2) {
      Logger.log("Нет новых данных для обработки");
      return;
    }
   
### **Проходим по строкам в обратном порядке**
| :---- |
чтобы обработать последнюю строку
    `for` (let i = data.length - 1; i >= 1; i--) {
      `const` row = data[i];
      `const` processed = row[26]; // Флаг обработки в 37-м столбце (индекс 36)
     
      Logger.log(`Проверка строки ${i + 1}, processed: ${processed}`);
     
### **Проверяем, не обработана ли строка**
      if (processed !== "Processed") {
### **Получаем данные для имени файла**
        const clientName = row[0] ? row[0].toString().replace(/[\/\\?%*:|"<>]/g, "_") : "Клиент_" + i; **Имя клиента или номер строки**
       
### **Обработка временной метки**
        let timestamp;
        if (row[1] && typeof row[1] === "string" && row[1].trim() !== "") {
          const dateValue = new Date(row[1].replace(".", "-").replace(",", "-")); _Поддержка форматов вроде "21.07.2025"_
          timestamp = !isNaN(dateValue.getTime())
            ? dateValue.toISOString().replace(/[:.]/g, "-")
            : new Date().toISOString().replace(/[:.]/g, "-"); _Если дата некорректна, используем текущую_
        } else {
          timestamp = new Date().toISOString().replace(/[:.]/g, "-"); _Если нет даты, используем текущую_
        }
       
### **Создаём новую таблицу**
        const newSpreadsheet = SpreadsheetApp.create(`Заявка_${clientName}_${timestamp}`);
        const newSheet = newSpreadsheet.getSheets()[0];
       
### **Копируем заголовки (36 пунктов)**
        const headers = data[0].slice(0, 26); _Берем первые 36 столбцов_
        newSheet.getRange(1, 1, 1, 26).setValues([headers]);
       
### **Копируем данные текущей заявки (36 пунктов)**
        const clientData = row.slice(0, 26); _Берем первые 36 столбцов текущей строки_
        newSheet.getRange(2, 1, 1, 26).setValues([clientData]);
       
### **Перемещаем новую таблицу в нужную папку (опционально)**


7. Измените вручную в 57 строке аргумент `const` на `folderid`.  
8. Выберите id папки в google диске.  
9. Получите ссылку на обновленный google disk.  
10. Обновите данные в 57 строке загрузив полученную ссылку в командную строку.  
11. Перейдите во вкладку «триггеры».  
12. Нажмите на кнопку «добавить триггер».  
13. Укажите настройки показанные на скриншоте.  
14. Перейдите во вкладку «код».  
15. Нажмите «выполнить».  
16. Перейдите во вкладку «журнал выполнения».

### **Готово Вы подключили google формы к Tilda Publishing**