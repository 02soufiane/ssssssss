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

