# Combine everything and create the main application logic.
from user import User
from workout import Workout
import file_handler
import report

def main():
    user = file_handler.load_user_data() or User(input("Enter your name: "))

    while True:
        print("\n1. Add Workout\n2. View Workouts\n3. Save Data\n4. Load Data\n5. Generate Report\n6. Exit")
        choice = input("Choose an option: ")
        if choice == '1':
            date = input("Enter date (YYYY-MM-DD): ")
            workout_type = input("Enter workout type: ")
            duration = int(input("Enter duration in minutes: "))
            calories_burned = int(input("Enter calories burned: "))
            workout = Workout(date, workout_type, duration, calories_burned)
            user.workouts.append(workout)
        elif choice == '2':
            for workout in user.workouts:
                print(workout)
        elif choice == '3':
            file_handler.save_user_data(user)
        elif choice == '4':
            user = file_handler.load_user_data()
        elif choice == '5':
            daily_report = report.generate_daily_report(user)
            report.display_report(daily_report)
        elif choice == '6':
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
