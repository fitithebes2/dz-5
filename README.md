import random

# варіанти
options = {
    "r": "камінь",
    "p": "папір",
    "s": "ножиці",
    "l": "ящірка",
    "k": "спок"  # k = spocK
}

# хто кого перемагає
rules = {
    "камінь": ["ножиці", "ящірка"],
    "ножиці": ["папір", "ящірка"],
    "папір": ["камінь", "спок"],
    "ящірка": ["спок", "папір"],
    "спок": ["ножиці", "камінь"]
}

def game(choice, result):

    player_move = options.get(choice.lower())
    if not player_move:
        print("Невірний вибір!")
        return

    computer_move = random.choice(list(options.values()))

    print(f"Ти обрав: {player_move}")
    print(f"Комп'ютер обрав: {computer_move}")

    # Нічия
    if player_move == computer_move:
        print("------Нічия------")
    
    # Гравець перемагає
    elif computer_move in rules[player_move]:
        result["player"] += 1
        print("------Player Wins------")
    
    # Комп'ютер перемагає
    else:
        result["computer"] += 1
        print("------Computer Wins------")

    print("Score, Computer", result["computer"], "—", result["player"], "Player")
    print("-" * 40)


# старт гри
result = {"computer": 0, "player": 0}

print("Гра: Камінь–Ножиці–Папір–Ящірка–Спок")
print("Вибери:")
print(" R = камінь\n P = папір\n S = ножиці\n L = ящірка\n K = спок\n")

while True:
    choice = input("Select R / P / S / L / K: ")
    game(choice, result)

    again = input("Грати ще раз? (y/n): ").lower()
    if again != "y":
        print("Кінцевий рахунок:")
        print("Computer:", result["computer"])
        print("Player:", result["player"])
        print("Дякую за гру!")
        break
