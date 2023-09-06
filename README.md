# Batcher-Banyon-Network

### Introduction about Batcher Banyon

Batcher-Banyan networks are a type of multistage interconnection network that is commonly found in multiprocessor interconnections and ATM switches. Switches built for these applications must be completely scalable. It is a combination of the batcher sorter and the banyan network. The Batcher sorter sorts the input packets according to their addresses. This sorting operation ensures that the subsequent banyan network will not be blocked, and it provides a quick way to check for contention. The Banyan network distributes packets to their final destinations with no contention.
In the Banyan network, there is a single path from each input port to each output port. 

### Demonstration of the batcher banyan logic using Python program:

Batcher banyan networks work as below logic:

* Request the user to enter the input value between 0 and 15.
* Based on the input value, the number of random numbers is generated.
* The random numbers generated are sorted in ascending order (batcher sort).
* Converting the random numbers to their binary equivalent and deciding the path of the whole network.
* The banyan network will select the upper path of the lane if the binary digit is “0” and the lower path of the lane if the binary digit is “1”
* In the 8*8 banyan network, switch 1 and switch 2 will decide the path based on the binary number, and switch 3 will display the final packet of data (out).
* In the 16*16 banyan network, switch 1, switch 2, and switch 3 will decide the path based on the binary number, and switch 4 will display the final packet of data (out).

### Source Code:

```python
import random

#Function switch1 to determine path from A to B
def switch1(input , destination):
    sw1 = {
        "A1": ["B1","B5"],
        "A2": ["B2","B6"],
        "A3": ["B3","B7"],
        "A4": ["B4","B8"],
        "A5": ["B1","B5"],
        "A6": ["B2","B6"],
        "A7": ["B3","B7"],
        "A8": ["B4","B8"],
        }
    Path_2 = sw1[input][int(destination[0])]
    return Path_2

#Function switch2 to determine path from B to C
def switch2(input , destination): 
    sw2 = {
        "B1": ["C1","C3"],
        "B2": ["C2","C4"],
        "B3": ["C1","C3"],
        "B4": ["C2","C4"],
        "B5": ["C5","C7"],
        "B6": ["C6","C8"],
        "B7": ["C5","C7"],
        "B8": ["C6","C8"],
        }
    Path_3 = sw2[input][int(destination[1])]
    return Path_3

#Function switch3 to determine path from C to D
def switch3(input , destination):
    sw3 = {
        "C1": ["D1","D2"],
        "C2": ["D1","D2"],
        "C3": ["D4","D4"],
        "C4": ["D3","D4"],
        "C5": ["D5","D6"],
        "C6": ["D5","D6"],
        "C7": ["D7","D8"],
        "C8": ["D7","D8"],
       }
    Path_4 = sw3[input][int(destination[2])]
    return Path_4

#Function switch4 to determine path from D to Out
def switch4(input , destination):
    sw4 = {
        "D1": ["out 0","out 1"],
        "D2": ["out 2","out 3"],
        "D3": ["out 4","out 5"],
        "D4": ["out 6","out 7"],
        "D5": ["out 8","out 9"],
        "D6": ["out 10","out 11"],
        "D7": ["out 12","out 13"],
        "D8": ["out 14","out 15"],
        }
    Path_5 = sw4[input][int(destination[3])]
    return Path_5

# Define main function for batcher banyon
def main():
    input_value = []
    get_user_input = int(input("Enter the input value between 0 to 15: \n"))
    print("-----------------------------------------------------------------------")         
    for r in range(get_user_input):
        random_number = random.randint(0,15)
        while random_number in input_value:
            random_number = random.randint(0,15)
        input_value.append(random_number)
      
    print("The Random Numbers are : ")
    print(input_value)
    print("-----------------------------------------------------------------------") 

    input_value.sort()
    input_dict ={} 
    print("Sorting the randomly generated number in ascending order:")
    for r in range(get_user_input):
        input_dict[r]= input_value[r]
        print("", input_dict[r])
    
    print("-----------------------------------------------------------------------") 
    entry_point = {
                    '0':'A1', 
                    '1':'A2', 
                    '2':'A3', 
                    '3':'A4', 
                    '4':'A5', 
                    '5':'A6', 
                    '6':'A7', 
                    '7':'A8',
                    '8':'A1', 
                    '9':'A2', 
                    '10':'A3', 
                    '11':'A4', 
                    '12':'A5', 
                    '13':'A6', 
                    '14':'A7', 
                    '15':'A8',
                  }
# Generate path from input port to output port
    print("<===== Path from input port to output port ====>\n")
    for r in range(get_user_input):
        Y = bin(input_dict[r])[2:].zfill(4)
        print("The Binary format of " +str(input_dict[r])+ " is", Y)
        Path_1 = entry_point[str(r)]
        Path_2 = switch1(Path_1, Y)
        Path_3 = switch2(Path_2, Y)
        Path_4 = switch3(Path_3, Y)
        Path_5 = switch4(Path_4, Y)
        print("Path from input port " +str(r)+ " to the output port " +str(input_dict[r])+ " is:")
        print(Path_1+ "------->" +Path_2+ "----->" +Path_3+ "------->" +Path_4+ "------->" +Path_5)
        print("\n")
    print("***** End of Program ****")

#Calling the main function
if __name__ == "__main__":
    main()
```

### Manual Test conducted and its expected values:

![image](https://github.com/swethamurthy25/Batcher-Banyon-Network/assets/112581595/91695dca-4b39-49c6-8574-a8645c4d97eb)

![image](https://github.com/swethamurthy25/Batcher-Banyon-Network/assets/112581595/954e5563-d735-4df6-8795-6689e8c145af)


### Expected and Desired Output:

![image](https://github.com/swethamurthy25/Batcher-Banyon-Network/assets/112581595/1b834579-bb10-4fdc-9067-fd208e102bb6)

![image](https://github.com/swethamurthy25/Batcher-Banyon-Network/assets/112581595/6526ec9f-a17a-4d28-8ac4-9d7c13761a75)

![image](https://github.com/swethamurthy25/Batcher-Banyon-Network/assets/112581595/345f5e87-46a0-47e3-b7e2-6e1df0f4ad25)


### Batcher Sorter

The batcher sorter will get the input value from the user generate random numbers based on the input value and then sort the numbers in ascending order. 
Below is the source code for the batcher sorter and its working:

```python
import random
input_value = []
get_user_input = int(input("Enter the input value between 0 to 15: \n"))
#Generate random numbers   
for r in range(get_user_input):
    random_number = random.randint(0,15)
    while random_number in input_value:
        random_number = random.randint(0,15)
    input_value.append(random_number)
      
print("The Random Numbers are : ")
print(input_value)

# Batcher Sorter
input_value.sort()
input_dict ={} 
print("Sorting the randomly generated number in ascending order:")
for r in range(get_user_input):
    input_dict[r]= input_value[r]
    print("", input_dict[r])
```

### Discussion of Results and Outcome:

I have created an 8-by-eight (8-by-eight) Batcher Banyan Network. When we feed the sorter integer input values (0-7) it sorts the number of inputs and passes it to the "Banyan Network." The network then changes to the next network based on binary values (0 and 1). The same applies to a 16 by 16 (16X16) network, with the exception that it switches between two 8x8 networks. 

* In the program, the random function library has been included.
* Random numbers will be generated based on the user input using the random function library.
* In the main function, first we must get the number of input values from the user, and it is stored in the variable named “get_user_input”.
* The input value can range from 0 to 15, which implies it should not be 0 and should not exceed 15.
* The user input is then passed to the function random.randint(0,15), which generates random numbers between 0 and 15.
* The generated random numbers are then stored in the input value [] array list.
* Then we used the sort () function to sort the randomly generated numbers in ascending order, and the sorted values were stored in the input_dict[r] dictionary.
* Then we have created an “entry_point” dictionary which stores the input value associated with each port.

#### Binary conversion and path generation:

* The bin() function was used to convert the sorted random numbers to their respective binary format, and the binary value of each number was stored in the variable Y.
* The binary values and initial lanes will be passed to the functions that determine the network in which the data transfer will take place.
* Each path here will take the output of the previous path as an input and based on that the destination will be chosen for the next stage.
* In the 16X16 network, we have a total of 4 switches. Once the binary equivalent numbers are generated, the batcher banyan network starts its execution.

### Advantages of this code
* It accepts up to 16 numbers from the user in a dynamic manner.
* Accepts any input >= 0 and <= 15

__________________________________________________________________________________________________________________________________________________________






