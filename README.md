# Monty Interpreter

A language interpreter made in the C programming language to manage stacks and queues (LIFO and FIFO). The aim is to interpret Monty bytecodes files. [Monty](http://montyscoconut.github.io/) is a language that aims to close the gap between scripting and programming languages.

# Compilation

To compile this project, you can use the following command:

```
$ make
```

# Option Codes

## Push opcode

The opcode `push` pushes an element to the stack.

**Usage:** `push <int>`, where *int* is an integer.

## Pall opcode

The opcode `pall` prints all the values on the stack, starting from the top of the stack.

**Usage:** `pall`. If the stack is empty, `pall` don’t print anything.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/push_pall_0.m
push 1$
push 2$
push 3$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/push_pall_0.m
3
2
1
$ ahmad-dev@ubuntu:~/monty$
```

## Pint opcode

The opcode `pint` prints the value at the top of the stack, followed by a new line.

**Usage:** `pint`. If the stack is empty, `pint` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/pint.m
push 1$
pint$
push 2$
pint$
push 3$
pint$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/pint.m
1
2
3
$ ahmad-dev@ubuntu:~/monty$
```

## Pop opcode

The opcode `pop` removes the top element of the stack.

**Usage:** `pop`. If the stack is empty, `pop` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/pop.m
push 1$
push 2$
push 3$
pall$
pop$
pall$
pop$
pall$
pop$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/pop.m
3
2
1
2
1
1
$ ahmad-dev@ubuntu:~/monty$
```

## Swap opcode

The opcode `swap` swaps the top two elements of the stack.

**Usage:** `swap`. If the stack contains less than two elements, `swap` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/swap.m
push 1$
push 2$
push 3$
pall$
swap$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/swap.m
3
2
1
2
3
1
$ ahmad-dev@ubuntu:~/monty$
```

## Add opcode

The opcode `add` adds the top two elements of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `add`. If the stack contains less than two elements, `add` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/add.m
push 1$
push 2$
push 3$
pall$
add$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/swap.m
3
2
1
5
1
$ ahmad-dev@ubuntu:~/monty$
```

## Nop opcode

The opcode `nop` doesn’t do anything.

**Usage:** `nop`.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/nop.m
nop$
push 1$
nop$
push 2$
nop$
push 3$
nop$
pall$
nop$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/nop.m
3
2
1
3
2
1
$ ahmad-dev@ubuntu:~/monty$
```

## Sub opcode

The opcode `sub` subtracts the top element of the stack from the second top element of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `sub`. If the stack contains less than two elements, `sub` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/sub.m
push 1$
push 2$
push 10$
push 3$
sub$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/sub.m
7
2
1
$ ahmad-dev@ubuntu:~/monty$
```

## Div opcode

The opcode `div` divides the second top element of the stack by the top element of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `div`. If the stack contains less than two elements, `div` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/div.m
push 1$
push 2$
push 10$
push 5$
div$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/div.m 
2
2
1
$ ahmad-dev@ubuntu:~/monty$
```
## Mul opcode

The opcode `mul` multiplies the second top element of the stack with the top element of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `mul`. If the stack contains less than two elements, `mul` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/mul.m
push 1$
push 2$
push 20$
push 5$
mul$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/mul.m 
100
2
1
$ ahmad-dev@ubuntu:~/monty$
```

## Mod opcode

The opcode `mod` computes the rest of the division of the second top element of the stack by the top element of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `mod`. If the stack contains less than two elements, `mod` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/mod.m
push 1$
push 2$
push 20$
push 5$
mod$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/mul.m 
0
2
1
$ ahmad-dev@ubuntu:~/monty$
```

## Comments

Every good language comes with the capability of commenting. When the first non-space character of a line is `#`, treat this line as a comment (don’t do anything).

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/comments.m
#hello world$
#hahahaha$
#cisfun$
#montyisfun$
push 10$
push 2$
push 8$
push 5$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/comments.m 
5
8
2
10
$ ahmad-dev@ubuntu:~/monty$
```

## Pchar opcode

The opcode `pchar` prints the char at the top of the stack, followed by a new line. The integer stored at the top of the stack is treated as the ascii value of the character to be printed.

**Usage:** `pchar`

* If the value is not in the ascii table (`man ascii`), `pchar` print an error message.
* If the stack is empty, `pchar` print an error message.

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/pchar.m
push 72$
pchar$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/pchar.m 
H
$ ahmad-dev@ubuntu:~/monty$
```

## Pstr opcode

The opcode `pstr` prints the string starting at the top of the stack, followed by a new line. The integer stored in each element of the stack is treated as the ascii value of the character to be printed.

**Usage:** `pstr`. If the stack is empty, `pstr` print only a new line

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/pstr.m
push 1$
push 2$
push 3$
push 4$
push 0$
push 110$
push 0$
push 121$
push 116$
push 110$
push 111$
push 77$
pstr$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/pstr.m 
Monty
$ ahmad-dev@ubuntu:~/monty$
```

## Rotl opcode

The opcode `rotl` rotates the stack to the top. The top element of the stack becomes the last one, and the second top element of the stack becomes the first one.

**Usage:** `rotl`

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/rotl.m
push 1$
push 2$
push 3$
push 4$
push 5$
push 6$
push 7$
push 8$
push 9$
push 0$
pall$
rotl$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/rotl.m 
0
9
8
7
6
5
4
3
2
1
9
8
7
6
5
4
3
2
1
0
$ ahmad-dev@ubuntu:~/monty$
```

## Rotr opcode

The opcode `rotr` rotates the stack to the bottom. The last element of the stack becomes the top element of the stack.

**Usage:** `rotr`

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/rotr.m
push 1$
push 2$
push 3$
push 4$
push 5$
push 6$
push 7$
push 8$
push 9$
push 0$
pall$
rotr$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/rotr.m 
0
9
8
7
6
5
4
3
2
1
1
0
9
8
7
6
5
4
3
2
$ ahmad-dev@ubuntu:~/monty$
```

## Stack opcode

The opcode `stack` sets the format of the data to a stack (LIFO). This is the default behavior of the program.

**Usage:** `stack`

## Queue opcode

The opcode `queue` sets the format of the data to a queue (FIFO).

**Usage:** `queue`

### Switching mode

* The top of the stack becomes the front of the queue
* The front of the queue becomes the top of the stack

```
$ ahmad-dev@ubuntu:~/monty$ cat -e bytecodes/queue_stack.m
queue$
push 1$
push 2$
push 3$
pall$
stack$
push 4$
push 5$
push 6$
pall$
add$
pall$
queue$
push 11111$
add$
pall$
$ ahmad-dev@ubuntu:~/monty$ ./monty.run bytecodes/queue_stack.m
1
2
3
6
5
4
1
2
3
11
4
1
2
3
15
1
2
3
11111
$ ahmad-dev@ubuntu:~/monty$
```
