class Terrain:
    def _init_(self, rows, cols):
        self.rows = rows
        self.cols = cols
        self.robots = {} 

    def add_robot(self, robot_id):
        if robot_id in self.robots:
            print(f"Robot {robot_id} already exists!")
            return
        self.robots[robot_id] = (0, 0)
        print(f"Robot {robot_id} added at (0,0)")

    def move_robot(self, robot_id, direction):
        if robot_id not in self.robots:
            print(f"Robot {robot_id} does not exist!")
            return

        row, col = self.robots[robot_id]
        new_row, new_col = row, col

        if direction == "UP" and row > 0:
            new_row -= 1
        elif direction == "DOWN" and row < self.rows - 1:
            new_row += 1
        elif direction == "LEFT" and col > 0:
            new_col -= 1
        elif direction == "RIGHT" and col < self.cols - 1:
            new_col += 1
        else:
            print(f"Invalid move for Robot {robot_id}")
            return

        # Check if the new position is occupied
        if (new_row, new_col) in self.robots.values():
            print(f"Robot {robot_id} stopped before ({new_row}, {new_col}) due to another robot.")
            return

        self.robots[robot_id] = (new_row, new_col)
        print(f"Robot {robot_id} moved to ({new_row}, {new_col})")

    def display_robots(self):
        print("Current robot positions:")
        for robot_id, position in self.robots.items():
            print(f"Robot {robot_id}: {position}")
