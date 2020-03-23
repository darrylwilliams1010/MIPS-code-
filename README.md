# MIPS-code-
MIPS code - This code is use to find out if a user input of a natural is the even or odd using recursion 
	.globl main
	.text 
main: 
	addi $sp, $sp, -8
	sw $s0, 0($sp)
	
	
	#prints message 
	 li $v0, 4
     	 la $a0, mes
     	 syscall 
     	 # read user input  
     	 li $v0, 5
     	 syscall
     	 move $s0, $v0
     	 
	move $a0, $s0
	jal isOdd 	# calls isodd function 
	
	beq $v0, $1, end
	jal isEven    		# calls isEven function 
	beq $v0, $0, end2
end: 

	li $v0,1
	move $a0, $s1
	syscall 
	li $v0,4
	la $a0, oddMes
	syscall 
end2: 

	li $v0,1
	move $a0, $v0
	syscall 
	li $v0,4
	la $a0, evenMes
	syscall 
	#restore register
	lw $ra, 4($sp)
	lw $a0, 0($sp)
	#free memory 
	addi $sp, $sp, 8	
     	  # system call to end program
     	   #end program 
     	  li $v0, 10
     	  syscall
isOdd: 
	addi $sp, $sp, -8
	sw $a0 ,0($sp)
	sw $ra, 4($sp)
	# check n==0
	beq $a0,0, return_0    #checks if user input equals 0
	# call isEven(n-1)
	add $a0,$a0,-1
	jal isEven  #jump to isEven
	
	#return return result
	move $s1,$v0  #(optional)
	
	#restore register
	lw $ra, 4($sp)
	lw $a0, 0($sp)
	#free memory 
	addi $sp, $sp, 8
	
	#jump back to return address
	jr $ra	
	
return_0:     
        li $v0,0
        #restore register
	lw $ra, 4($sp)
	lw $a0, 0($sp)
	#free memory 
	addi $sp, $sp, 8
	#jump back to return address
        jr $ra
isEven:
	#backup $ra and $a0
	# $a0 -> n
	addi $sp, $sp, -8
	sw $a0 ,0($sp)
	sw $ra, 4($sp)
	# check n==0
	beq $a0, $0, return_1 #if $a0==0, jump to retur_1
	# call isOdd(n-1)
	add $a0, $a0,-1
	jal isOdd  # jump to isOdd
	
	
	#return return result
	move $v0,$v0  #(optional)
	
	 
	#restore register
	lw $ra, 4($sp)
	lw $a0, 0($sp)
	#free memory 
	addi $sp, $sp, 8
	#jump back to return address
	jr $ra	
	
return_1:
	#return 1 
	li $v0,1
	#restore register
	lw $ra, 4($sp)
	lw $a0, 0($sp)
	#free memory 
	addi $sp, $sp, 8
	#jump back to return address
	jr $ra	
	 
  .data 
  mes: .asciiz "enter a natural number"
  oddMes: .asciiz "is odd number "
  evenMes: .asciiz  "is even number "
