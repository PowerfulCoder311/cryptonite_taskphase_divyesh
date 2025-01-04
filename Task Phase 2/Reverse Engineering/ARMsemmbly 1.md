# ARMsemmbly 1
Challenge: For what argument does this program print `win` with variables 87, 3 and 3? File: chall_1.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb}  

Task: We have to find the specific input that makes the program 'you win'

### main function
  - converts the input into an integer
  - calls the func function with the input
  - prints "You win!" if func returns 0, otherwise prints "You Lose :("
Therefore we need to find the input for which func function returns 0

### Func Function
 - left shifts 87 by 3, essentially multiplying by 2^3. Calculating, we get 696
   (base 10)
 - divides the result by 3. 696/3= 232
 - finally, substracts the input from the given result. Therefore, for the function to return 0,
   input must also be 232
### Finding the Flag
232 to hex = 0xE8 where 0x indicates its in hexadecimal. 

 - no 0x -> E8
 - lowercase -> e8
 - 32 bits, we know 1 hex digit = 4bits therefore 8 hex digits

flag-> picoCTF{000000e8}

