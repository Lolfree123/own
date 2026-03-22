import sys
import time
import random

# colors
green = "\033[1;32m"
reset = "\033[0m"

# your logo
logo = r"""
██╗░░░██╗██████╗░░█████╗░░░░░░██╗░█████╗░███╗░░██╗
██║░░░██║██╔══██╗██╔══██╗░░░░░██║██╔══██╗████╗░██║
╚██╗░██╔╝██████╔╝██║░░██║░░░░░██║███████║██╔██╗██║
░╚████╔╝░██╔══██╗██║░░██║██╗░░██║██╔══██║██║╚████║
░░╚██╔╝░░██║░░██║╚█████╔╝╚█████╔╝██║░░██║██║░╚███║
░░░╚═╝░░░╚═╝░░╚═╝░╚════╝░░╚════╝░╚═╝░░╚═╝╚═╝░░╚══╝
"""

# split into matrix
lines = logo.strip("\n").split("\n")
matrix = [list(line) for line in lines]

# glitch characters
glitch_chars = list("█▓▒░@#$%&*+=-/<>ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

# revealed tracking
revealed = [[False]*len(row) for row in matrix]

# positions to reveal (ignore spaces)
positions = [
    (i, j)
    for i in range(len(matrix))
    for j in range(len(matrix[i]))
    if matrix[i][j] != " "
]

random.shuffle(positions)

# tuning
FLICKER_COUNT = 1     # less = faster reveal
GLITCH_DELAY = 0.02  # more = slower visible glitch
STEP = 4              # reveal multiple chars per step

# animation
for k in range(0, len(positions), STEP):
    batch = positions[k:k+STEP]

    # glitch frames
    for _ in range(FLICKER_COUNT):
        print("\033c", end="")

        for x in range(len(matrix)):
            row = ""
            for y in range(len(matrix[x])):
                if revealed[x][y]:
                    row += matrix[x][y]
                elif matrix[x][y] == " ":
                    row += " "
                else:
                    row += random.choice(glitch_chars)
            print(green + row + reset)

        time.sleep(GLITCH_DELAY)

    # reveal actual characters
    for (i, j) in batch:
        revealed[i][j] = True

# final stable output
print("\033c", end="")
for row in matrix:
    print(green + "".join(row) + reset)
