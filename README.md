# starting values and modules
from random import randint
good_function_input = False
good_digit_length = False
digits_are_numbers = False
digits_are_usable = False
answering_questions = False
answer_usable = False
is_done = False
questions_answered = 0
score = 0

# defining function to generate random digits based on input
def random_number_generator(number_of_digits):
    if number_of_digits == 1:
        return (randint(1,9))
    elif number_of_digits == 2:
        return (randint(10,99))
    else:
        return (randint(100,999))

# greeting
print("Welcome to Math Mania!")

# requesting function from user
function_input = input("To start, please choose your function.\
\nPlease type +, -, *, or / \nType 'done' if you wish to exit.\n")

# checking if they chose one of the functions
while good_function_input == False:
    if function_input.lower() == "done":
        is_done = True
        break
    elif function_input == "+" or function_input == "-" or function_input == "*" or function_input == "/":
        good_function_input = True
        
        if function_input == "+":
            chosen_function = function_input
            print("\nYou have chosen addition!\n")
        elif function_input == "-":
            chosen_function = function_input
            print("\nYou have chosen subtraction!\n")
        elif function_input == "*":
            chosen_function = function_input
            print("\nYou have chosen multiplication!\n")
        elif function_input == "/":
            chosen_function = function_input
            print("\nYou have chosen division!\n")
        break
    else:
         function_input = input("You must type +, -, *, /, or 'done'\n")
         continue

# requesting digits from user
if is_done == False and (chosen_function == "+" or chosen_function == "-" or chosen_function == "*"):
    digits_input = input("Please type the digits you'd like to use in format a,b\
    \nwith a being # of digits in first number and b being the # of digits in the second.\
    \nEach # must be between the numbers 1 and 3. \nType 'done' if you wish to exit.\n")
    
    # checking if their answer has the correct length
    while digits_are_usable == False or digits_are_numbers == False or good_digit_length == False:
        if digits_input.lower() == "done":
            is_done = True
            break
        
        if digits_input != "" and len(digits_input) == 3:
            good_digit_length = True
        else:
            good_digit_length = False
            digits_input = input("Your answer should be 3 characters long ex: 2,3. Please try again. \n")
            continue
    
        # checking if their their answer has numbers
        if digits_input[0].isnumeric() == True and digits_input[2].isnumeric() == True:
            digits_are_numbers = True
        else: 
            digits_are_numbers = False
            digits_input = input("You need to type digits not letters ex: 2,3. Please try again. \n")
            continue

        # checking if their numbers are in range
        if 3 >= int(digits_input[0]) >= 1 and 3 >= int(digits_input[2]) >= 1:
            digits_are_usable = True
            chosen_digits = digits_input
            break
        else: 
            digits_are_usable = False
            digits_input = input("Your digits need to be between 1 and 3. Please try again. \n")
            continue

# setting chosen digits
if is_done == False:
    first_number_digits = int(chosen_digits[0])
    second_number_digits = int(chosen_digits[2])

    # must be true to loop questions
    answering_questions = True

    print("\nNow it's time to start answering questions!\
    \nType 'done' when you want to finish and get your score\n")

while is_done == False and answering_questions == True:
    # must be false in order to check conditions at the bottom
    answer_usable = False
    
    # generating numbers, setting answer, and requesting input for +
    if chosen_function == "+":
        first_number = random_number_generator(first_number_digits)
        second_number = random_number_generator(second_number_digits)
        real_answer = first_number + second_number
        user_answer = input(f"What is {first_number} + {second_number}?\n")
    
    # generating numbers, setting answer, and requesting input for -
    if chosen_function == "-":
        first_number = random_number_generator(first_number_digits)
        second_number = random_number_generator(second_number_digits)
        real_answer = first_number - second_number
        user_answer = input(f"What is {first_number} - {second_number}?\n") 
        
    # generating numbers, setting answer, and requesting input for *
    if chosen_function == "*":
        first_number = random_number_generator(first_number_digits)
        second_number = random_number_generator(second_number_digits)
        real_answer = first_number * second_number
        user_answer = input(f"What is {first_number} * {second_number}?\n")
    
    # generating numbers (in a different way to prevent remainder), setting answer, and requesting input for /   
    if chosen_function == "/":
        real_answer = randint(50,299)
        second_number = randint(1,20)
        first_number = real_answer * second_number
        user_answer = input(f"What is {first_number} / {second_number}?\n")

    # checking if user wants to stop answering questions
    if user_answer.lower() == "done":
        answering_questions = False
        break
    
    # checking if answer is a number (ignoring '-' in case of negatives)
    while answer_usable == False:
        
        if user_answer.lower() == "done":
            answering_questions = False
            is_done = True
            break
        elif user_answer.strip("-").isdigit() == False:
            user_answer = input("You must enter a number for your answer\n")
        else:
            answer_usable = True
            break
    
    # checking if answer is correct and adding to question/score total    
    if is_done == False and real_answer == int(user_answer):
            print("Correct!\n")
            score += 1
            questions_answered += 1
    elif is_done == False:
            print("Incorrect :(\n")
            questions_answered += 1
    else:
        break

# closing statement with score
if questions_answered > 0:
    print(f"You got {score} out of {questions_answered} questions correct!\
    \nHave a nice day!")
else:
    print("Have a nice day!")

