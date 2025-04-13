# Python-OOP-assignment-Wk-5
File Structure:
oop_assignment/
├── classes.py
└── main.py

1. Design Your Own Class! (classes.py):
# classes.py

class Smartphone:
    def __init__(self, brand, model, storage, battery):
        self.brand = brand
        self.model = model
        self.storage = storage
        self.battery = battery
        self.is_on = False

    def power_on(self):
        if not self.is_on:
            self.is_on = True
            print(f"{self.brand} {self.model}: Powering on...")
        else:
            print(f"{self.brand} {self.model} is already on.")

    def power_off(self):
        if self.is_on:
            self.is_on = False
            print(f"{self.brand} {self.model}: Powering off...")
        else:
            print(f"{self.brand} {self.model} is already off.")

    def install_app(self, app_name):
        print(f"{self.brand} {self.model}: Installing {app_name}...")
        # Simulate installation
        print(f"{app_name} installed successfully on {self.brand} {self.model}.")

    def get_info(self):
        return f"Brand: {self.brand}, Model: {self.model}, Storage: {self.storage}GB, Battery: {self.battery}mAh, Status: {'On' if self.is_on else 'Off'}"

class CameraSmartphone(Smartphone):
    def __init__(self, brand, model, storage, battery, megapixels):
        super().__init__(brand, model, storage, battery)
        self.megapixels = megapixels

    def take_photo(self):
        if self.is_on:
            print(f"{self.brand} {self.model}: Capturing a {self.megapixels}MP photo...")
            return "photo.jpg"  # Simulate saving a photo
        else:
            print("Please power on the phone to take a photo.")
            return None

    # Override get_info to include camera details (Polymorphism)
    def get_info(self):
        base_info = super().get_info()
        return f"{base_info}, Camera: {self.megapixels}MP"

# Example of Encapsulation (making battery level somewhat protected)
class AdvancedSmartphone(Smartphone):
    def __init__(self, brand, model, storage, battery):
        super().__init__(brand, model, storage, battery)
        self._battery_level = battery  # Using a single underscore to indicate protected

    def charge(self, duration_hours):
        if self.is_on:
            print("Please power off the phone before charging for optimal charging.")
        else:
            charge_amount = duration_hours * 500  # Example charge rate
            self._battery_level = min(self.battery, self._battery_level + charge_amount)
            print(f"{self.brand} {self.model}: Charging for {duration_hours} hours. Battery level is now {self._battery_level}mAh.")

    def use_app(self, app_name, duration_minutes):
        if self.is_on:
            usage = duration_minutes * 10  # Example battery drain
            if self._battery_level >= usage:
                self._battery_level -= usage
                print(f"{self.brand} {self.model}: Using {app_name} for {duration_minutes} minutes. Battery remaining: {self._battery_level}mAh.")
            else:
                print(f"{self.brand} {self.model}: Not enough battery to use {app_name} for {duration_minutes} minutes.")
        else:
            print("Please power on the phone first.")

    # Override get_info to show current battery level
    def get_info(self):
        base_info = super().get_info()
        return f"{base_info}, Current Battery: {self._battery_level}mAh"


2. Polymorphism Challenge! (main.py):
# main.py
from classes import Smartphone, CameraSmartphone, AdvancedSmartphone

def animal_sound(animal):
    animal.make_sound()

class Animal:
    def make_sound(self):
        print("Generic animal sound")

class Dog(Animal):
    def make_sound(self):
        print("Woof!")

class Cat(Animal):
    def make_sound(self):
        print("Meow!")

class Cow(Animal):
    def make_sound(self):
        print("Moo!")

def vehicle_move(vehicle):
    vehicle.move()

class Vehicle:
    def move(self):
        print("Generic vehicle movement")

class Car(Vehicle):
    def move(self):
        print("Driving 🚗")

class Plane(Vehicle):
    def move(self):
        print("Flying ✈️")

class Boat(Vehicle):
    def move(self):
        print("Sailing ⛵")

if __name__ == "__main__":
    # Activity 1: Design Your Own Class!
    print("--- Activity 1: Designing Classes ---")
    my_phone = Smartphone("Google", "Pixel 8", 128, 4500)
    camera_phone = CameraSmartphone("Samsung", "Galaxy S24 Ultra", 256, 5000, 200)
    advanced_phone = AdvancedSmartphone("Apple", "iPhone 16", 512, 4000)

    my_phone.power_on()
    my_phone.install_app("WhatsApp")
    print(my_phone.get_info())
    my_phone.power_off()
    print("-" * 20)

    camera_phone.power_on()
    photo_file = camera_phone.take_photo()
    if photo_file:
        print(f"Photo saved as {photo_file}")
    print(camera_phone.get_info())
    camera_phone.power_off()
    print("-" * 20)

    advanced_phone.charge(2)
    advanced_phone.power_on()
    advanced_phone.use_app("Instagram", 30)
    print(advanced_phone.get_info())
    advanced_phone.power_off()
    print("-" * 20)

    # Activity 2: Polymorphism Challenge!
    print("\n--- Activity 2: Polymorphism Challenge ---")
    animals = [Dog(), Cat(), Cow()]
    for animal in animals:
        animal_sound(animal)
    print("-" * 20)

    vehicles = [Car(), Plane(), Boat()]
    for vehicle in vehicles:
        vehicle_move(vehicle)

