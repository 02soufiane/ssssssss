## Завдання 1
Посилання [JSON_DetailedDataSchema_Example.json](https://github.com/oleksandrblazhko/ai-211-el/blob/e0ad1f292628110120fe509b5d3b1bbd7b179b0f/2-SoftwareDesign/2.4-DetailedDataSchema/JSON_DetailedDataSchema_Example.json)<br>

Ось фрагмент коду працівника медпункту:

```
"Employee of the health center": {
      "description": "Employee of the health center details",
      "type": "object",
      "properties": {
        "Age": {
          "description": "Employee age",
          "type": "number",
          "minimum": 0
        },
        "Name": {
          "description": "Employee name",
          "type": "string",
          "minLength": 2,
          "maxLength": 50
        },
        "Specialization": {
          "description": "Specialization",
          "type": "string",
          "minLength": 6,
          "maxLength": 20
        }
      },
      "required": ["Age", "Name", "Specialization"]
    }
```

Тут у є поле "specialization", в цьому полі є обмеження на довжину вже, але перетворимо це все в регулярний вираз з забороної на спеціальні символи згідно завданню.
ось саме регулярний вираз:

`^(?!.*[#@%$]).{6,20}$`

А змінений код виглядає наступним чином:
```
"Employee of the health center": {
      "description": "Employee of the health center details",
      "type": "object",
      "properties": {
        "Age": {
          "description": "Employee age",
          "type": "number",
          "minimum": 0
        },
        "Name": {
          "description": "Employee name",
          "type": "string",
          "minLength": 2,
          "maxLength": 50
        },
        "Specialization": {
          "description": "Specialization",
          "type": "string",
          "pattern": "^(?!.*[#@%$]).{6,20}$"
        }
      },
      "required": ["Age", "Name", "Specialization"]
    }
```

## Завдання 2

[UMLProgramClasses](https://github.com/oleksandrblazhko/ai-211-el/tree/0843d70658b028db61ed29b1095a257eacb98af5/2-SoftwareDesign/2.5-UMLProgramClasses) - діаграма програмних класів з лабораторної роботи 6

Коментарі до UML - діаграми програмних класів

#### Consumer-QuestionAboutHealth :
Елементи класу Consumer активно взаємодіють із системою охорони здоров’я надсилаючи певні запити пов’язані зі здоров’ям інкапсульовані в класі QuestionAboutHealth. Ці запити спрямовані на вирішення проблем із особистим здоров’ям і мають мітку часу для точного ведення записів.

#### Consumer-ConsumerInformation :
Кожен індивід, представлений класом Consumer, підтримує окремий зв’язок зі своєю відповідною ConsumerInformation. Це сховище інформації містить такі важливі особисті дані, як ім’я, електронна адреса та вік. Крім того, він надає користувачам такі функції, як sendQuestion(), readInfo() і getAnswer(), що полегшує надсилання запитів, пов’язаних із здоров’ям, пошук збереженої інформації та отримання відповідей у системі.

#### HealthCenterEmployee-Consumer :
Клас HealthCenterEmployee бере на себе роль одержувача, отримуючи запити, пов’язані зі здоров’ям, від екземплярів класу Consumer. Ця взаємодія має ключове значення, оскільки вона дає змогу працівникам медичних центрів ефективно вирішувати та відповідати на запити споживачів, забезпечуючи швидку та точну допомогу.

#### HealthCenterEmployee-ConsumerInformation :
Клас HealthCenterEmployee активно взаємодіє з інформацією, що зберігається в ConsumerInformation, і використовує її. Ця взаємодія сприяє всебічному розумінню деталей споживачів, допомагаючи в обґрунтованих відповідях і індивідуальній допомозі в ефективному задоволенні потреб споживачів.

#### HealthCenterEmployee-HealthData Relationship :
Використовуючи дані, що зберігаються в сховищі HealthData, екземпляри класу HealthCenterEmployee проводять аналіз даних, пов’язаних зі здоров’ям, у системі. Цей аналіз даних відіграє вирішальну роль у наданні обґрунтованих відповідей, рекомендацій і персоналізованих порад щодо здоров’я для ефективного вирішення проблем здоров’я споживачів.

#### HealthCenterEmployee-ResponseToConsumer :
Екземпляри класу HealthCenterEmployee активно беруть участь у формуванні відповідей на запити споживачів, пов’язані зі здоров’ям, інкапсульовані в класі ResponseToConsumer. Ці відповіді розроблено на основі всебічного аналізу даних про здоров’я та інформації, зібраної від споживачів.

#### ResponseToConsumer-Consumer Relationship :
Клас ResponseToConsumer служить сховищем для відповідей, сформульованих екземплярами класу HealthCenterEmployee на запити, надіслані екземплярами класу Consumer. Цей зв’язок забезпечує безперебійне об’єднання відповідей із відповідними запитами, полегшуючи пошук і перегляд споживачами.
