- 👋 Hi, I’m @23Elaineee
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
23Elaineee/23Elaineee is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
# Data section
.data
     prompt1: .asciiz"\nEnter number for M : "
     prompt2: .asciiz"\nEnter number for N : "
     message: .asciiz"\nY = "
     message1: .asciiz"\nError! Invalid input! \n"
     message2: .asciiz"\nError! Invalid input! \n"


# Text section
.text
.globl main


main:

     addi $t0, $zero, 100
     addi $t1, $zero, 250

     # Input M
     li $v0, 4
     la $a0, prompt1
     syscall

     li $v0, 5
     syscall
     move $t2, $v0
  
     # Input N 
     li $v0, 4
     la $a0, prompt2
     syscall

     li $v0, 5
     syscall
     move $t3, $v0

     jal operation1

operation1:
     addi $sp, $sp, -4
     sw $t4, 4($sp)
     move $t4, $zero
     li $v1, 1

loop:
     beq $t4, $t3, end
     mul $v1, $v1, $t1
     addi $t4, $t4, 1

     ble $t2, 0, end1
     bge $t2, 100, end1

     ble $t3, 1, end2
     bge $t3, 5, end2

     j loop

end:
     mul $t5, $t2, 3
     add $t6, $v1, $t5
     sub $t7, $t6, $t0

     # Display message
     li $v0, 4
     la $a0, message
     syscall

     # Print out or show the result
     li $v0, 1
     move $a0, $t7
     syscall
     
     j main

end1:
     li $v0, 4
     la $a0, message1
     syscall

     j main


end2:
     li $v0, 4
     la $a0, message2
     syscall

     j main


.end main
