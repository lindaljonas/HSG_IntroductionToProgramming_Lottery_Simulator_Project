# HSG_IntroductionToProgramming_Lottery_Simulator_Project
#Part 1: Lottery Simulator

import random

print('Welcome! This is a lottery simulator.')
print('Guess 7 numbers and 3 lucky numbers.')
print('Choose numbers between 1 and 34, and lucky numbers between 1 and 6.')
print('To win a prize you must guess 4 or more numbers in the correct position')
print('The prizes to win are: CHF 75 for 4 correct guesses')
print('                       CHF 150 for 5 correct guesses')
print('                       CHF 1.000 for 6 correct guesses')
print('                       CHF 1.000.000 for 7 correct guesses')


#Machine Plays
number_main=list(range(1,35)) #List of main numbers from 1 to 34 
chosenNumber=[]
numbers_lucky=list(range(1,7)) #List of lucky numbers from 1 to 6
luckyNumber=[]
n=0    #Floor number of choices from the lists

while n<7: #Using while loop to restrict the selection of numbers from main list to exactly 7
  x=random.choice(number_main) #picks a random choice of a number from the main list
  chosenNumber.append(x) #adds the randomly picked number from main list to chosen number list
  number_main.remove(x) #removes the picked numbers from the main list
  n+=1

n=0
while n<3: #Using while loop to restrict the random selection of numbers from lucky_number list to 3
  x=random.choice(numbers_lucky)
  luckyNumber.append(x)
  numbers_lucky.remove(x)
  n+=1

#print('Correct numbers: ', chosenNumber)
#print('Correct lucky numbers: ', luckyNumber)

#You play
n=0
myGuess=[] #list of users guesses
while n<7:
  choice=input('Guess a number: ')
  while type(choice) != int: 
    try: 
      choice = int(choice)
    except: 
       choice = input("Error! thats not a whole number, please try again: ") #limiting the guess to integers
  myGuess.append(choice) #adds choice to list og guesses made until user has made 7 guesses
  n+=1

n=0
myGuess_luckyNumber=[]
while n<3:
  luckychoice=input('Guess a lucky number: ')
  while type(luckychoice) != int:
    try: 
      luckychoice = int(luckychoice)
    except: 
       luckychoice = input("Error! thats not a whole number, please try again: ") #limiting the guess to integers
  myGuess_luckyNumber.append(luckychoice)
  n+=1

CorrectNumbers = 0
for x in range (0,7):
  if myGuess[x]==chosenNumber[x]: #Checking how many of the randomly picked numbers is similar to the input numbers
    CorrectNumbers += 1

CorrectLuckyNumbers = 0
for x in range (0,3):
  if myGuess_luckyNumber[x]==luckyNumber[x]: #Checking how many of the randomly picked lucky numbers corresponds to the input numbers
    CorrectLuckyNumbers += 1

print('Winning numbers: ', chosenNumber)
print('Winning lucky numbers: ', luckyNumber)

print('Correct numbers: ', CorrectNumbers)
print('Correct lucky number: ', CorrectLuckyNumbers)

if CorrectNumbers==7: #if the users 7 main guesses corresponds with the randomly drawn numbers from the main list
  print('You have won CHF 1.000.000!')
elif CorrectNumbers==6 and CorrectLuckyNumbers==1:
  print('You have won CHF 10.000!')
elif CorrectNumbers==6 and CorrectLuckyNumbers!=1:
  print('You have won CHF 1.000!')
elif CorrectNumbers==5:
  print('You have won CHF 150!')
elif CorrectNumbers==4:
  print('You have won CHF 75!')
else:
  print('You did not win anything!')

#Part 2: Chance of winning the big prize defined by number of tickets bought

def factorial(n):
    final_product = 1
    for i in range(n, 0, -1):
        final_product *= i
    return final_product

def combinations(n,k):
    numerator = factorial(n)
    denominator = factorial(k) * factorial(n-k)
    return numerator / denominator

def one_ticket_probability(numbers):
    total_outcomes = combinations(34, 7) 
    successful_outcome = 1 / total_outcomes 
    probability_winning = (successful_outcome / total_outcomes) *100
    print("You're chances of winning the big prize with one ticket are {:.16f}%!".format(probability_winning))

test_ticket = [1,4,32,10,5,18,8] #random numbers
one_ticket_probability(test_ticket)

def multi_ticket_probability(n_tickets_played):
  total_outcomes = combinations(34,7)
  successful_outcome = n_tickets_played / total_outcomes
  probability_n_tickets = (successful_outcome / total_outcomes)*100
  combinations_simplified = round(total_outcomes / n_tickets_played)
  print("""Your chances to win the big prize with {:,} different tickets are 1 in {:,} chances to win.""".format(n_tickets_played, combinations_simplified))

ticket_quantity = int(input('How many tickets would you like to buy? '))

#print(ticket_quantity)
multi_ticket_probability(ticket_quantity)
