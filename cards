import json
import random

def load_definitions():
    try:
        with open("definitions.json") as file:
            return json.load(file)
    except FileNotFoundError:
        return {}

def save_definitions(definitions):
    with open("definitions.json", "w") as file:
        json.dump(definitions, file)

def check_answer(user_answer, correct_answer):
    return user_answer.lower() == correct_answer.lower()

def get_random_definition(definitions):
    term = random.choice(list(definitions.keys()))
    return term, definitions[term]

def handler(event, context):
    definitions = load_definitions()
    term, definition = get_random_definition(definitions)
    
    text = f"Определение: {definition}\n\nВведите соответствующий термин:"
    buttons = []

    if "request" in event and "original_utterance" in event["request"] and len(event["request"]["original_utterance"]) > 0:
        user_input = event["request"]["original_utterance"]

        if check_answer(user_input, term):
            text = "Правильно! Молодец! Хочешь увидеть следующее определение?"
            buttons = [
                {
                    "title": "Да",
                    "hide": True
                },
                {
                    "title": "Нет",
                    "hide": True
                }
            ]
        else:
            text = f"Неправильно. Верный термин: {term}. Хочешь увидеть следующее определение?"
            buttons = [
                {
                    "title": "Да",
                    "hide": True
                },
                {
                    "title": "Нет",
                    "hide": True
                }
            ]

    return {
        "version": event["version"],
        "session": event["session"],
        "response": {
            "text": text,
            "buttons": buttons,
            "end_session": False
        }
    }
