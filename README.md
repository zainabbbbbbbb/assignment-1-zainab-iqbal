# assignment-1-zainab-iqbal
flight_raw_data = {}

def display_seat_layout(seat_layout):
    print('V W X Y Z ')
    for coloum, row in enumerate(seat_layout, start=1):
        print(f'Row {coloum}: {" ".join(row)}')

def book_a_seat(airline):
    display_seat_layout(flight_raw_data[airline]['seat_layout'])
    row = int(input('eneter your desire row number(1-5): '))
    if 1 <= row <= 5:
        column1 = input('Enter your seat between (A-F): ').upper()
        if column1 in 'V W X Y Z' and flight_raw_data[airline]['seat_layout'][row - 1][ord(column1) - ord('A')] == '*':
            flight_raw_data[airline]['seat_layout'][row - 1][ord(column1) - ord('A')] = 'X'
            passenger_name = input('Enter your name: ')
            with open('flightdetail.txt', 'a') as f:
                f.write(f'{passenger_name} {airline} Row {row} Seat {column1}\n')
            print('YOUR SEAT IS  ',passenger_name,'BOOKED SUCCESSFULLY')
        else:
            print('Sorry the seat is already booked ')
    else:
        print('please try agaian or select number between 1 to 5.')

def cancel_booking(airline):
    display_seat_layout(flight_raw_data[airline]['seat_layout'])
    row = int(input('Enter Row number from (1-5): '))
    if 1 <= row <= 5:
        column2 = input('Enter Seat Column (A-F): ').upper()
        if column2 in 'V W X Y Z' and flight_raw_data[airline]['seat_layout'][row - 1][ord(column2) - ord('W')] == 'X':
            flight_raw_data[airline]['seat_layout'][row - 1][ord(column2) - ord('W')] = '*'
            print(f'Booking for IS  {row} Seat {column2} canceled.')
        else:
            print('Seat is available .')
    else:
        print('your row number is not correct')

def save_flight_data(filename, data):
    with open(filename, 'w') as f:
        for airline, details in data.items():
            f.write(f'Airline: {airline}\n')
            f.write(f'Departure Time: {details["Departure"]}\n')
            f.write(f'Arrival Time: {details["Arrival"]}\n')
            
            f.write('--------------------------------------------------\n')

def show_flight_details():
    for airline, details in flight_raw_data.items():
        print(f'Airline: {airline}')
        print(f'Departure Time: {details["Departure"]}')
        print(f'Arrival Time: {details["Arrival"]}')

def add_flight():
    airline_name = input('Enter  the Airline name you want to have a flight with ')
    departure_time = input('Enter Departure Time: ')
    arrival_time = input('Enter Arrival Time: ')
    flight_raw_data[airline_name] = {'Departure': departure_time, 'Arrival': arrival_time, 'seat_layout': [['*' for _ in range(6)] for _ in range(5)]}
    print('Your Flight is successfully incremented')

def remove_flight():
    airline_name2= input('To remove the flight please enter the airline name:')
    if airline_name2 in flight_raw_data:
        del flight_raw_data[airline_name2]
        print(f'Flight {airline_name2} removed')
    else:
        print('Airline wasnot found please enter correct details')

def modify_flight():
    airline_name3 = input('Enter Airline Name to Modify: ')
    if airline_name3 in flight_raw_data:
        departure_time2 = input('Enter New Departure Time: ')
        arrival_time2= input('Enter New Arrival Time: ')
        flight_raw_data[airline_name3]['Departure'] = departure_time2
        flight_raw_data[airline_name3]['Arrival'] = arrival_time2
        print(f'Flight {airline_name3} modified successfully.')
    else:
        print('Airline not found.')

def admin_interface():
    while True:
        print(" WELCOME TO USER FOR DESIRE FLIGHTS(: )")
        print("   1.  Add the flight")
        print("   2.  Remove a flight")
        print("   3.  Modify a flight")
        print("   4.  Display flights")
        print("   5.  Exit and Save")
        choice = input('Enter a number between 1 to 5: ')
        if choice == '1':
            add_flight()
        elif choice == '2':
            remove_flight()
        elif choice == '3':
            modify_flight()
        elif choice == '4':
            show_flight_details()
        elif choice == '5':
            save_flight_data('flightdetail.txt', flight_raw_data)
            print(' data saved for flight')
            break
        else:
            print('Incorrect choice Please select again.')
            admin_interface()
def user_menu():
    while True:
        print("   1.  Book a ticket")
        print("   2.  Cancel a booking")
        print("   3.  Show flight details")
        print("   4.  Go back")
        print()
        Yourchoice=input("select any option user")
        
        if Yourchoice == '1':
            print("welcome to ticket booking menu")
            airline = input('Enter Airline Name that you want to book: ')
            if airline in flight_raw_data:
                book_a_seat(airline)
            else:
                print('Airline not found')
        elif Yourchoice == '2':
            print("welcome to booking canceling")
            airline = input('Enter Airline Name from which you want to cancel the booking: ')
            print()
            if airline in flight_raw_data:
                cancel_booking(airline)
            else:
                print('Airline not found.')
        elif Yourchoice == '3':
            show_flight_details()
        elif Yourchoice == '4':
            break
        else:
            print('Incorrect option  Please select again.')
            user_menu()

def user_login1():
    print("welcome to user console")
    print()
    user=input("enter user name")
    print()
    password1=input("enter password")
    if user==("user") and password1==("user123"):
        user_menu()
    else:
        print("error!wrong username or password, tryagain")
        useradminlogin()


def admin_login():
    print("welcome to admin console")
    user=input("enter the admin name:")
    password2=input("enter the password:")
    if user==("zainab") and password2==("zainab29876"):
        admin_interface()
    else:
        print("wrong password please try again")
        




def useradminlogin():
    while True:
       
        print("press 1 for user login")
        print("press 2 for admin login"  )
        print("press 3 To  Exit this system ")
        
        choice = input(' select an option : ')
        if choice == '1':
            user_login1()
        elif choice == '2':
            admin_login()
        elif choice == '3':
            print('good day from z airplain management system ')
            break
        else:
            print('Incorrect option Please select again')
            useradminlogin()
            
useradminlogin()
