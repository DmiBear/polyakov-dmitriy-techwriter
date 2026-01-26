# Тестирование метода lookup API

**Получение API-ключа.**
1. Перейдите на сервис Яндекс.облака [yandex.oblako](https://yandex.ru/dev/dictionary/)
2. Нажмите на кнопку «Получить API-ключ».

**Формирование запроса curl**

```bash
curl -X GET "https://dictionary.yandex.net/api/v1/dicservice/lookup?key=ВАШ_API_КЛЮЧ&lang=en-ru&text=sky&ui=ru" -H "Accept: application/xml" -o response_sky.xml
```

## Параметры запроса

**key** - полученный API-ключ
**lang** - **en-ru** - направление перевода
**text - sky** - искомое слово
**ui - ru** - язык интерфейса 

## Результат
```xml
<DicResult nmt_code="200" code="200">
    <head/>
    <def pos="существительное" ts="skaɪ">
         <text>sky</text>
        <tr pos="существительное" gen="ср" fr="10">
             <text>небо</text>
             <syn pos="существительное" fr="5">
                 <text>небеса</text>
                 </syn>
                 <syn pos="существительное" gen="ср" fr="1">
                     <text>поднебесье</text>
                 </syn>
                 <mean>
                 <text>heaven</text>
                 </mean>
             <mean>
                 <text>heavens</text>
             </mean>
         </tr>
         <tr pos="существительное" gen="м" fr="1">
             <text>небосвод</text>
             <syn pos="существительное" gen="м" fr="1">
                 <text>небосклон</text>
             </syn>
             <syn pos="существительное" fr="1">
                 <text>небесный свод</text>
             </syn>
             <mean>
                 <text>firmament</text>
                 </mean>
             <mean>
                     -<text>horizon</text>
                 </mean>
             </tr>
             <tr pos="существительное" gen="м" fr="5">
                 <text>Скай</text>
             </tr>
         </def>
         <def pos="прилагательное" ts="skaɪ">
             <text>sky</text>
             <tr pos="прилагательное" fr="5">
                 <text>небесный</text>
                 <mean>
                     <text>heavenly</text>
                 </mean>
             </tr>
         </def>
 </DicResult>
```