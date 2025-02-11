import os
import time
from colorama import Fore, Style, init

init(autoreset=True)

def display_maze(maze, player_pos, explored):
    os.system('cls' if os.name == 'nt' else 'clear')
    for i, row in enumerate(maze):
        for j, col in enumerate(row):
            if (i, j) == player_pos:
                print(Fore.YELLOW + "🐢", end=" ")
            elif (i, j) in explored:
                if explored[(i, j)]:
                    print(Fore.GREEN + "🟢", end=" ")  # ทางที่ไปได้
                else:
                    print(Fore.RED + "🔴", end=" ")  # ทางตัน
            else:
                print(col, end=" ")
        print("")
    print("")

def explore_path(maze, start, end):
    stack = [start]
    visited = set()
    explored = {}

    while stack:
        current = stack.pop()
        if current == end:
            display_maze(maze, current, explored)
            return True
        
        if current in visited:
            continue
        visited.add(current)
        x, y = current

        paths = []
        for dx, dy in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
            next_pos = (x + dx, y + dy)
            if 0 <= next_pos[0] < len(maze) and 0 <= next_pos[1] < len(maze[0]) and maze[next_pos[0]][next_pos[1]] in (" ", "E"):
                paths.append(next_pos)
        
