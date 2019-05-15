# import json

# definiton of the variables
def get_the_data():        
    with open('hotels .json') as filename:
        hotels = json.load(filename)
    return hotels

def user_input_desiredStar():
    ds = raw_input("Insert your desired star from 1 to 5: ")
    while True:
        try:
            ds = int(ds) 
            if ds < 1 or ds > 5:
                ds = input("star of a hotel mighnt not be less than zero and more than 5")                
            else:
                return ds
        except ValueError as e:
            print("Try again")
            ds = raw_input("Insert your desired star from 1 to 5: ")
            continue
    
def user_input_money():
    money = raw_input("Insert the initial balance above 0: ")
    while True:
        try:
            money = int(money) 
            if money > 0:
                return money
            elif money < 0:
                money = input("not intereseted in your depts")
        except ValueError as e:
            print("Try again")
            ds = raw_input("Insert your desired star from 1 to 5: ")
            continue

def available_hotels(money,desiredStar,hotels):
        availableHotels = []
        for hotel in hotels:
            if int(money) >= int(hotel["single_room_price"]) and int(hotel["star_rating"]) == int(desiredStar):
                availableHotels.append(hotel)

        if len(availableHotels) == 0:
            print("Oops u don't have enoug money")
        else:
            for h in availableHotels:
                hotel_string = "Hotel: {}, Stars: {}, Price: {}".format(h["hotel_name"], h["star_rating"], h["single_room_price"])
                print(hotel_string)
        return availableHotels

def getHotelByPhoneNumber(hotels):
    phoneNumber = input("Input the phone number (###) #######")
    for h in hotels:
        if phoneNumber == h["phone"]:
            hotel_string = "Hotel: {}, Stars: {}, Price: {}".format(h["hotel_name"], h["star_rating"], h["single_room_price"])
            print(hotel_string)

def getTheBestChoise(money, hotels):
    star = 1
    bestHotel = None
    
    for h in hotels:
        if money >= int(h["single_room_price"]) and star < int(h["star_rating"]):
            star = int(h["star_rating"])
            bestHotel = h

    print(bestHotel)

def check():
    while True:
        checks = raw_input("Do you wanna try again? yes/no")
        print(checks)
        if checks == "no":
            return False
        elif checks == "yes":
            return True
        else:
            print('Please enter yes/no')
    

def main():
    print("THis app for finding hotels")
    hotels = get_the_data()
    flag = True
    while flag:
        action = input("Please input what you want (1 - for search based on PhoneNumber, 2 - For gettingthe best hotel based on money, 3 - for search based on stars")
        if action == 1:
            getHotelByPhoneNumber(hotels)
        elif action == 2:     
            money = user_input_money()
            getTheBestChoise(money, hotels)
        elif action == 3:
            money = user_input_money()
            desiredStars = user_input_desiredStar()
            available_hotel = available_hotels(money, desiredStars,hotels)
        else:
            print(" Wrong action")
        flag = check()


main()
