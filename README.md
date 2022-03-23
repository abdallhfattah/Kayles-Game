# Kayles-Game Coded with python

import random

player_turn = 0


def list_generator():
    # Generate 20 random numbers between 0 and 99 with no duplication
    # list has dash on first and dash at the end to avoid some errors
    random_list = ['-']
    while len(random_list) < 21:
        list_num = random.randint(0, 99)
        if list_num not in random_list:
            random_list.append(list_num)
    random_list.append('-')
    return random_list


# function that enables players to choose number from the random list
def play_function(random_list):
    list_generator()
    # separator
    print('*' * 100)
    # description of how the game works
    print(
        "!! Rules of the game !!\neach player can choose token from the list"
        "\nyou can choose two tokens but second token has to be next to the first token chosen by only 1 move either to the left or right"
        "\nafter choosing token it gets replaced with dash and second player wont be able to choose it to the end of the game\n"
        "!! Last player hit token Wins !! ")
    # this list is made to be compared with the random list so we can define a winner if they are equal to each other
    listo = ['-'] * 22
    # code that runs the whole game and calls other functions
    while listo != random_list:
        print('*' * 100)
        print(random_list[1:-1])
        player(random_list, listo)


def player(random_list,listo):
    global player_turn
    if player_turn == 0:
        player_num = 1
    else:
        player_num = 2
    # makes players alternate turns
    player_turn += 1
    player_turn = player_turn % 2

    num_player = int(input(f"Player {player_num}: Enter number from the list shown to eliminate it: "))

    while num_player not in random_list:
        num_player = int(input(f"Player {player_num}: Please hit number that is in the list: "))
    index_checker = random_list.index(num_player)
    # turning the number chosen to dash
    random_list[index_checker] = '-'
    print(random_list[1:-1])
    # asking for second play form Player
    entering_second_number = input(f"Player {player_num}: If you want to play your second token press Y: ")

    if entering_second_number.lower().strip() == 'y':
        sec_num_player = int(input(f"Player {player_num}: Enter second number from the list shown to eliminate it: "))
        # checking if the number is adjacent to the first number chosen or not
        if random_list[(index_checker + 1)] != '-' or random_list[(index_checker - 1)] != '-':
            # checking if the number is adjacent to the first number chosen or not
            if sec_num_player not in [random_list[index_checker + 1], random_list[index_checker + 1]]:
                # keeps asking if player has wrong input
                while sec_num_player not in [random_list[index_checker + 1], random_list[index_checker - 1]]:

                    sec_num_player = int(input(f"Player {player_num}: please choose adjacent number: "))
            # if player chooses right input from the first time
            if random_list[index_checker + 1] == sec_num_player or random_list[index_checker + 1] == sec_num_player:
                index_checker2 = random_list.index(sec_num_player)
                random_list[index_checker2] = '-'
                print(random_list[1:-1])

            else:
                index_checker2 = random_list.index(sec_num_player)
                random_list[index_checker2] = '-'
                print(random_list[1:-1])

        else:
            print(f"Player {player_num}: you cant play another token")
    # declares a winner
    if listo == random_list:
        print(f"Player {player_num} congratulations you have won")
        exit()


def main():
    play_function(list_generator())


main()
