import random


def dealing():
    global stock_pieces, player_pieces, computer_pieces, domino_snake, status
    while True:
        stock_pieces = []
        for i in range(0, 7):
            for ii in range(0, 7):
                if ii > i:
                    continue
                stock_pieces.append([i, ii])
        player_pieces = random.sample(stock_pieces, k=7)
        for i in player_pieces:
            stock_pieces.remove(i)
        computer_pieces = random.sample(stock_pieces, k=7)
        for i in computer_pieces:
            stock_pieces.remove(i)
        placeholder = 7
        for i in range(0, 6):
            placeholder -= 1
            if [placeholder, placeholder] in player_pieces:
                domino_snake = [[placeholder, placeholder]]
                player_pieces.remove([placeholder, placeholder])
                status = "computer"
                break
            elif [placeholder, placeholder] in computer_pieces:
                domino_snake = [[placeholder, placeholder]]
                computer_pieces.remove([placeholder, placeholder])
                status = "player"
                break
        return status


def make_move(user_move):
    global bad_input, to_print, pos, domino
    while True:
        if user_move == 0:
            if stock_pieces_size != 0:
                player_pieces.append(stock_pieces[0])
                stock_pieces.pop(0)
            return
        else:
            pos = abs(user_move) - 1
            domino = player_pieces[pos]
            string_dom = str(domino)
            first_val = string_dom[1]
            second_val = string_dom[-2]
            if user_move < 0:
                if second_val != to_print[1]:
                    if first_val != to_print[1]:
                        user_move = int(input("Illegal move. Please try again.\n"))
                        continue
                    else:
                        domino = [int(second_val), int(first_val)]
                if user_move < 0:
                    domino_snake.insert(0, domino)
                else:
                    domino_snake.append(domino)
                player_pieces.pop(pos)
                return
            else:
                if first_val != to_print[-2]:
                    if second_val != to_print[-2]:
                        user_move = int(input("Illegal move. Please try again.\n"))
                        continue
                    else:
                        domino = [int(second_val), int(first_val)]
                if user_move < 0:
                    domino_snake.insert(0, domino)

                else:
                    domino_snake.append(domino)
                player_pieces.pop(pos)
                return


def computer_move():
    global pos, domino
    counting_list = []
    val_dict = {}
    score_dict = {}
    for i in computer_pieces:
        for ii in i:
            counting_list.append(ii)
    for i in domino_snake:
        for ii in i:
            counting_list.append(ii)
    for i in range(0, 7):
        num_of_them = counting_list.count(i)
        val_dict[i] = num_of_them
    for i in computer_pieces:
        score_dict[str(i)] = val_dict[i[0]] + val_dict[i[1]]
    while True:
        if len(score_dict) == 0:
            if stock_pieces_size != 0:
                computer_pieces.append(stock_pieces[0])
                stock_pieces.pop(0)
            return
        fin_max = max(score_dict, key=score_dict.get)
        if fin_max[1] == to_print[1]:
            new_domino = [int(fin_max[-2]), int(fin_max[1])]
            domino_snake.insert(0, new_domino)
            computer_pieces.remove([int(fin_max[1]), int(fin_max[-2])])
            return
        elif fin_max[1] == to_print[-2]:
            new_domino = [int(fin_max[1]), int(fin_max[-2])]
            domino_snake.append(new_domino)
            computer_pieces.remove([int(fin_max[1]), int(fin_max[-2])])
            return
        elif fin_max[-2] == to_print[1]:
            new_domino = [int(fin_max[1]), int(fin_max[-2])]
            domino_snake.insert(0, new_domino)
            computer_pieces.remove([int(fin_max[1]), int(fin_max[-2])])
            return
        elif fin_max[-2] == to_print[-2]:
            new_domino = [int(fin_max[-2]), int(fin_max[1])]
            domino_snake.append(new_domino)
            computer_pieces.remove([int(fin_max[1]), int(fin_max[-2])])
            return
        del score_dict[fin_max]


def main():
    global stock_pieces_size, computer_pieces_size, bad_input, to_print
    current_status = dealing()
    while True:
        to_print = ""
        for i in domino_snake:
            to_print += str(i)
        stock_pieces_size = len(stock_pieces)
        computer_pieces_size = len(computer_pieces)
        bad_input = True
        print("=" * 70)
        print(f"Stock size: {stock_pieces_size}")
        print(f"Computer pieces: {computer_pieces_size}\n")
        if len(domino_snake) <= 6:
            print(to_print)
        else:
            print(f"{domino_snake[0]}{domino_snake[1]}{domino_snake[2]}...{domino_snake[-3]}{domino_snake[-2]}{domino_snake[-1]}")
        for i in player_pieces:
            num = player_pieces.index(i) + 1
            print(f"{num}:{i}")
        if computer_pieces_size == 0:
            print("Status: The game is over. The computer won!")
            break
        elif len(player_pieces) == 0:
            print("Status: The game is over. You won!")
            break
        elif to_print[1] == to_print[-2] and to_print.count(to_print[1]) == 8:
            print("Status: the game is over. It's a draw!")
            break
        if current_status == "computer":
            input("\nStatus: Computer is about to make a move. Press Enter to continue... \n")
            computer_move()
            current_status = "player"
        else:
            while bad_input:
                move = input("\nStatus: It's your turn to make a move. Enter your command. \n")
                try:
                    move = int(move)
                    pieces_count = len(player_pieces)
                    negative_pieces = pieces_count * -1
                    if move < negative_pieces or move > pieces_count:
                        print("Invalid input. Please try again.")
                        continue
                    make_move(move)
                    bad_input = False
                    current_status = "computer"
                except ValueError:
                    print("Invalid input. Please try again.")


if __name__ == "__main__":
    main()
