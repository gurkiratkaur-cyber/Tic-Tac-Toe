# Tic-Tac-Toe
Tic-Tac-Toe Game
def print_board(board):
    print("---------")
    for row in board:
        print("| " + " | ".join(row) + " |")
    print("---------")

def check_win(board, player):
    # Check rows, columns, and diagonals
    for i in range(3):
        if all([cell == player for cell in board[i]]):
            return True
        if all([board[j][i] == player for j in range(3)]):
            return True
    if all([board[i][i] == player for i in range(3)]):
        return True
    if all([board[i][2-i] == player for i in range(3)]):
        return True
    return False

def is_full(board):
    return all([cell != " " for row in board for cell in row])

def tic_tac_toe():
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"
    while True:
        print_board(board)
        print(f"Player {current_player}'s turn.")
        try:
            row = int(input("Enter row (0-2): "))
            col = int(input("Enter col (0-2): "))
            if not (0 <= row < 3 and 0 <= col < 3):
                print("Invalid input. Try again.")
                continue
            if board[row][col] != " ":
                print("Cell already taken. Try again.")
                continue
        except ValueError:
            print("Invalid input. Please enter numbers.")
            continue

        board[row][col] = current_player
        if check_win(board, current_player):
            print_board(board)
            print(f"Player {current_player} wins!")
            break
        if is_full(board):
            print_board(board)
            print("It's a tie!")
            break
        current_player = "O" if current_player == "X" else "X"

if __name__ == "__main__":
    tic_tac_toe()
