# Final-Project
import random

class Dice:
    def __init__(self, sides=6):
        self.sides = sides

    def roll(self):
        return random.randint(1, self.sides)

class Player:
    def __init__(self, name):
        self.name = name
        self.score = 0

    def roll_dice(self, num_dice, sides):
        total = sum(Dice(sides).roll() for _ in range(num_dice))
        return total

class Game:
    def __init__(self, player_name, num_dice, sides, rounds):
        self.player = Player(player_name)
        self.computer = Player("Computer")
        self.num_dice = num_dice
        self.sides = sides
        self.rounds = rounds

    def play_round(self):
        player_total = self.player.roll_dice(self.num_dice, self.sides)
        computer_total = self.computer.roll_dice(self.num_dice, self.sides)

        print(f"{self.player.name} rolled a total of: {player_total}")
        print(f"Computer rolled a total of: {computer_total}")

        if player_total > computer_total:
            self.player.score += 1
            print(f"{self.player.name} wins this round!\n")
        elif computer_total > player_total:
            self.computer.score += 1
            print("Computer wins this round!\n")
        else:
            print("This round is a tie!\n")

    def play_game(self):
        for round_num in range(1, self.rounds + 1):
            print(f"Round {round_num}:")
            self.play_round()

        print("Final Scores:")
        print(f"{self.player.name}: {self.player.score}")
        print(f"Computer: {self.computer.score}")

        if self.player.score > self.computer.score:
            print(f"{self.player.name} wins the game!")
        elif self.computer.score > self.player.score:
            print("Computer wins the game!")
        else:
            print("The game is a tie!")

def main():
    player_name = input("Enter your name: ")
    num_dice = int(input("Enter the number of dice: "))
    sides = int(input("Enter the number of sides on each die: "))
    rounds = int(input("Enter the number of rounds: "))

    game = Game(player_name, num_dice, sides, rounds)
    game.play_game()

if __name__ == "__main__":
    main()
