import math
import random

class RoboticPollinator:
    def __init__(self, x=0, y=0, direction=0):
        self.position = (x, y)
        self.direction = direction  # Direction in degrees, 0 means facing east
        self.is_moving = False
    
    def start(self):
        self.is_moving = True
        print("Robotic pollinator started moving.")
    
    def stop(self):
        self.is_moving = False
        print("Robotic pollinator stopped moving.")
    
    def move(self, distance):
        if self.is_moving:
            rad = math.radians(self.direction)
            dx = distance * math.cos(rad)
            dy = distance * math.sin(rad)
            x, y = self.position
            self.position = (x + dx, y + dy)
            print(f"Moved {distance} units in direction {self.direction} degrees. New position: {self.position}.")
        else:
            print("The robotic pollinator is not moving. Start it first.")
    
    def change_direction(self, new_direction):
        if 0 <= new_direction < 360:
            self.direction = new_direction
            print(f"Changed direction to {self.direction} degrees.")
        else:
            print("Invalid direction. Please enter a value between 0 and 359 degrees.")
    
    def pollinate(self):
        print(f"Pollinating at position {self.position}")
    
    def get_position(self):
        return self.position
    
    def search_for_flower(self, search_area):
        if self.is_moving:
            flower_x = random.uniform(search_area[0], search_area[2])
            flower_y = random.uniform(search_area[1], search_area[3])
            self.flower_position = (flower_x, flower_y)
            print(f"Flower detected at position {self.flower_position}")
            self.move_towards_flower()
        else:
            print("The robotic pollinator is not moving. Start it first.")
    
    def move_towards_flower(self):
        if self.is_moving and hasattr(self, 'flower_position'):
            fx, fy = self.flower_position
            x, y = self.position
            dx = fx - x
            dy = fy - y
            distance = math.sqrt(dx**2 + dy**2)
            if distance > 0:
                self.direction = math.degrees(math.atan2(dy, dx))
                self.move(distance)
                print(f"Moved towards the flower at {self.flower_position}")
            else:
                print("Already at the flower position.")
        else:
            print("Either the robot is not moving or the flower position is not set.")

