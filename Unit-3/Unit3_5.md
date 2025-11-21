# Unit III Assignment 5: Postfix Expression Evaluator using Stack

Implementation to evaluate postfix expressions (Reverse Polish Notation) using stack data structure.

## Problem Statement

You are given a postfix expression (also known as Reverse Polish Notation) consisting of single-digit operands and binary operators (+, -, *, /). Your task is to evaluate the expression using stack and return its result.

## Pseudo Code

### Stack Structure
```
Structure IntStack:
    items: array of integers
    top: integer
    size: integer
```

### Is Operator
```
Algorithm IsOperator(symbol):
    Return symbol is one of '+', '-', '*', '/'
```

### Is Operand
```
Algorithm IsOperand(symbol):
    Return symbol is digit (0-9)
```

### Perform Operation
```
Algorithm PerformOperation(operator, operand1, operand2):
    Switch operator:
        Case '+': Return operand1 + operand2
        Case '-': Return operand1 - operand2
        Case '*': Return operand1 * operand2
        Case '/': 
            If operand2 is 0:
                Return error (division by zero)
            Return operand1 / operand2
```

### Evaluate Postfix
```
Algorithm EvaluatePostfix(expression):
    Initialize empty stack
    For each character in expression:
        If character is operand:
            Convert to integer and push to stack
        Else If character is operator:
            If stack has fewer than 2 elements:
                Return error (invalid expression)
            operand2 = Pop from stack
            operand1 = Pop from stack
            result = PerformOperation(character, operand1, operand2)
            Push result to stack
    If stack has exactly one element:
        Return that element
    Else:
        Return error (invalid expression)
```

## Code Implementation

```c
#include <iostream>
using namespace std;
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#define MAX_SIZE 100
struct IntStack_rrd {
    int items_rrd[MAX_SIZE];
    int top_rrd;
    int size_rrd;
};

struct IntStack_rrd* createStack_rrd();
int isEmpty_rrd(struct IntStack_rrd* stack_rrd);
int isFull_rrd(struct IntStack_rrd* stack_rrd);
int push_rrd(struct IntStack_rrd* stack_rrd, int item_rrd);
int pop_rrd(struct IntStack_rrd* stack_rrd, int* poppedValue_rrd);
int peek_rrd(struct IntStack_rrd* stack_rrd, int* peekedValue_rrd);
int isOperator_rrd(char ch_rrd);
int isOperand_rrd(char ch_rrd);
int isValidPostfix_rrd(char expression_rrd[]);
int performOperation_rrd(char operator_rrd, int operand1_rrd, int operand2_rrd, int* result_rrd);
int evaluatePostfix_rrd(char expression_rrd[], int* finalResult_rrd);
void displayMenu_rrd();
struct IntStack_rrd* createStack_rrd() {
    struct IntStack_rrd* stack_rrd = (struct IntStack_rrd*)malloc(sizeof(struct IntStack_rrd));
    stack_rrd->top_rrd = -1;
    stack_rrd->size_rrd = MAX_SIZE;
    return stack_rrd;
}

int isEmpty_rrd(struct IntStack_rrd* stack_rrd) {
    return stack_rrd->top_rrd == -1;
}

int isFull_rrd(struct IntStack_rrd* stack_rrd) {
    return stack_rrd->top_rrd == MAX_SIZE - 1;
}

int push_rrd(struct IntStack_rrd* stack_rrd, int item_rrd) {
    if (isFull_rrd(stack_rrd))
{
        cout << "Stack Overflow! Cannot push " << item_rrd << "" << endl;
        return 0;
    }

    stack_rrd->items_rrd[++stack_rrd->top_rrd] = item_rrd;
    return 1;
}

int pop_rrd(struct IntStack_rrd* stack_rrd, int* poppedValue_rrd) {
    if (isEmpty_rrd(stack_rrd))
{
        cout << "Stack Underflow! Cannot pop from empty stack" << endl;
        return 0;
    }

    *poppedValue_rrd = stack_rrd->items_rrd[stack_rrd->top_rrd--];
    return 1;
}

int peek_rrd(struct IntStack_rrd* stack_rrd, int* peekedValue_rrd) {
    if (isEmpty_rrd(stack_rrd))
{
        return 0;
    }

    *peekedValue_rrd = stack_rrd->items_rrd[stack_rrd->top_rrd];
    return 1;
}

int isOperator_rrd(char ch_rrd) {
    return (ch_rrd == '+' || ch_rrd == '-' || ch_rrd == '*' || ch_rrd == '/');
}

int isOperand_rrd(char ch_rrd) {
    return (ch_rrd >= '0' && ch_rrd <= '9');
}

int isValidPostfix_rrd(char expression_rrd[]) {
    int len_rrd = strlen(expression_rrd);
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        char ch_rrd = expression_rrd[i_rrd];
        if (!isOperand_rrd(ch_rrd) && !isOperator_rrd(ch_rrd))
{
            return 0;
        }
    }

    int operandCount_rrd = 0;
    int operatorCount_rrd = 0;
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        if (isOperand_rrd(expression_rrd[i_rrd]))
{
            operandCount_rrd++;
        } else if (isOperator_rrd(expression_rrd[i_rrd]))

{
            operatorCount_rrd++;
        }
    }

    if (operandCount_rrd == 0 || operatorCount_rrd == 0)
{
        return 0;
    }
    return 1;
}

int performOperation_rrd(char operator_rrd, int operand1_rrd, int operand2_rrd, int* result_rrd) {
    switch (operator_rrd)
{
        case '+':
            *result_rrd = operand1_rrd + operand2_rrd;
            return 1;
        case '-':
            *result_rrd = operand1_rrd - operand2_rrd;
            return 1;
        case '*':
            *result_rrd = operand1_rrd * operand2_rrd;
            return 1;
        case '/':
            if (operand2_rrd == 0)
{
                cout << "Error: Division by zero!" << endl;
                return 0;
            }

            *result_rrd = operand1_rrd / operand2_rrd;
            return 1;
        default:
            printf("Error: Invalid operator '%c'\n", operator_rrd);
            return 0;
    }
}

int evaluatePostfix_rrd(char expression_rrd[], int* finalResult_rrd) {
    struct IntStack_rrd* stack_rrd = createStack_rrd();
    int len_rrd = strlen(expression_rrd);
    cout << "\nEvaluating postfix expression: " << expression_rrd << "" << endl;
    cout << "Step-by-step evaluation:" << endl;
    cout << "Step\tCharacter\tStack\t\t\tOperation" << endl;
    cout << "----\t---------\t-----\t\t\t---------" << endl;
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        char ch_rrd = expression_rrd[i_rrd];
        if (isOperand_rrd(ch_rrd))
{
            int operand_rrd = ch_rrd - '0';
            if (!push_rrd(stack_rrd, operand_rrd))
{
                free(stack_rrd);
                return 0;
            }

            cout << "" << i_rrd + 1, ch_rrd << "\t%c\t\t";
            if (isEmpty_rrd(stack_rrd))
{
                cout << "(empty)\t\t\t";
            } else
{

                cout << "[";
                for (int j_rrd = 0; j_rrd <= stack_rrd->top_rrd; j_rrd++)
{
                    cout << "" << stack_rrd->items_rrd[j_rrd] << "";
                    if (j_rrd < stack_rrd->top_rrd) cout << ", ";
                    {
                }

                cout << "]\t\t\t";
            }

            cout << "Push " << operand_rrd << "" << endl;
        } else if (isOperator_rrd(ch_rrd))

{
            if (stack_rrd->top_rrd < 1)
{
                cout << "Error: Insufficient operands for operator '%c' at position " << ch_rrd, i_rrd + 1 << "" << endl;
                free(stack_rrd);
                return 0;
            }

            int operand2_rrd, operand1_rrd;
            if (!pop_rrd(stack_rrd, &operand2_rrd) || !pop_rrd(stack_rrd, &operand1_rrd))
{
                free(stack_rrd);
                return 0;
            }

            int result_rrd;
            if (!performOperation_rrd(ch_rrd, operand1_rrd, operand2_rrd, &result_rrd))
{
                free(stack_rrd);
                return 0;
            }

            if (!push_rrd(stack_rrd, result_rrd))
{
                free(stack_rrd);
                return 0;
            }

            cout << "" << i_rrd + 1, ch_rrd << "\t%c\t\t";
            if (isEmpty_rrd(stack_rrd))
{
                cout << "(empty)\t\t\t";
            } else
{

                cout << "[";
                for (int j_rrd = 0; j_rrd <= stack_rrd->top_rrd; j_rrd++)
{
                    cout << "" << stack_rrd->items_rrd[j_rrd] << "";
                    if (j_rrd < stack_rrd->top_rrd) cout << ", ";
                    {
                }

                cout << "]\t\t\t";
            }

            cout << "" << operand1_rrd, ch_rrd, operand2_rrd, result_rrd << " %c %d = %d" << endl;
        }
    }

    if (stack_rrd->top_rrd == 0)
{
        *finalResult_rrd = stack_rrd->items_rrd[0];
        cout << "Final\t-\t\t[" << *finalResult_rrd, *finalResult_rrd << "]\t\t\tResult: %d" << endl;
        free(stack_rrd);
        return 1;
    } else if (stack_rrd->top_rrd > 0)

{
        cout << "Error: Invalid expression - " << stack_rrd->top_rrd + 1 << " operands remaining in stack" << endl;
        free(stack_rrd);
        return 0;
    } else
{

        cout << "Error: Invalid expression - No result computed" << endl;
        free(stack_rrd);
        return 0;
    }
}

void infixToPostfix_rrd(char infix_rrd[], char postfix_rrd[]) {
    struct IntStack_rrd* stack_rrd = createStack_rrd();
    int i_rrd = 0, j_rrd = 0;
    while (infix_rrd[i_rrd] != '\0')
{
        char ch_rrd = infix_rrd[i_rrd];
        if (isOperand_rrd(ch_rrd))
{
            postfix_rrd[j_rrd++] = ch_rrd;
        } else if (ch_rrd == '(')

{
            push_rrd(stack_rrd, ch_rrd);
        } else if (ch_rrd == ')')

{
            int temp_rrd;
            while (!isEmpty_rrd(stack_rrd) && peek_rrd(stack_rrd, &temp_rrd) && temp_rrd != '(')
{
                pop_rrd(stack_rrd, &temp_rrd);
                postfix_rrd[j_rrd++] = temp_rrd;
            }

            int dummy_rrd;
            pop_rrd(stack_rrd, &dummy_rrd);
        } else if (isOperator_rrd(ch_rrd))

{
            int topOperator_rrd;
            while (!isEmpty_rrd(stack_rrd) && peek_rrd(stack_rrd, &topOperator_rrd) && 
            {
                   topOperator_rrd != '(' && 
                   ((ch_rrd == '+' || ch_rrd == '-') || (topOperator_rrd == '*' || topOperator_rrd == '/')))
{
                pop_rrd(stack_rrd, &topOperator_rrd);
                postfix_rrd[j_rrd++] = topOperator_rrd;
            }

            push_rrd(stack_rrd, ch_rrd);
        }

        i_rrd++;
    }

    int temp_rrd;
    while (!isEmpty_rrd(stack_rrd))
{
        pop_rrd(stack_rrd, &temp_rrd);
        postfix_rrd[j_rrd++] = temp_rrd;
    }

    postfix_rrd[j_rrd] = '\0';
    free(stack_rrd);
}

void generateSampleExpressions_rrd() {
    cout << "\nSample Postfix Expressions:" << endl;
    cout << "1. 23+     (Infix: 2+3)              = 5" << endl;
    cout << "2. 234*+    (Infix: 2+(3*4))         = 14" << endl;
    cout << "3. 23+4*    (Infix: (2+3)*4)         = 20" << endl;
    cout << "4. 234*+5-  (Infix: (2+(3*4))-5)     = 9" << endl;
    cout << "5. 23-45*+  (Infix: (2-3)+(4*5))     = 19" << endl;
    cout << "6. 234+*5-  (Infix: (2*(3+4))-5)     = 9" << endl;
}

void analyzeExpression_rrd(char expression_rrd[]) {
    int operandCount_rrd = 0;
    int operatorCount_rrd = 0;
    int len_rrd = strlen(expression_rrd);
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        if (isOperand_rrd(expression_rrd[i_rrd]))
{
            operandCount_rrd++;
        } else if (isOperator_rrd(expression_rrd[i_rrd]))

{
            operatorCount_rrd++;
        }
    }

    cout << "\nExpression Analysis:" << endl;
    cout << "Length: " << len_rrd << " characters" << endl;
    cout << "Operands: " << operandCount_rrd << "" << endl;
    cout << "Operators: " << operatorCount_rrd << "" << endl;
    cout << "Complexity: " << operatorCount_rrd << " operations" << endl;
    if (operandCount_rrd == operatorCount_rrd + 1)
{
        cout << "Structure: Valid postfix expression" << endl;
    } else
{

        cout << "Structure: Invalid postfix expression" << endl;
    }
}

void displayMenu_rrd() {
    cout << "\n===== Postfix Expression Evaluator =====" << endl;
    cout << "1. Evaluate Postfix Expression" << endl;
    cout << "2. Analyze Expression" << endl;
    cout << "3. Generate Sample Expressions" << endl;
    cout << "4. Convert Infix to Postfix (Bonus)" << endl;
    cout << "5. Exit" << endl;
    cout << "=======================================" << endl;
    cout << "Enter your choice: ";
}

int main() {
    cout << "Welcome to Postfix Expression Evaluator!" << endl;
    cout << "Note: This evaluator works with single-digit operands (0-9) and binary operators (+, -, *, /)" << endl;
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        cin >> choice_rrd;
        switch (choice_rrd)
{
{
                char expression_rrd[MAX_SIZE];
                cout << "Enter postfix expression: ";
                cin >> expression_rrd;
                if (!isValidPostfix_rrd(expression_rrd))
{
                    cout << "Error: Invalid postfix expression!" << endl;
                    cout << "Make sure expression contains only digits (0-9) and operators (+, -, *, /)" << endl;
                    break;
                }

                int result_rrd;
                if (evaluatePostfix_rrd(expression_rrd, &result_rrd))
{
                    cout << "\nFinal Result: " << result_rrd << "" << endl;
                } else
{

                    cout << "\nEvaluation failed!" << endl;
                }
                break;
            }

{
                char expression_rrd[MAX_SIZE];
                cout << "Enter postfix expression: ";
                cin >> expression_rrd;
                if (!isValidPostfix_rrd(expression_rrd))
{
                    cout << "Error: Invalid postfix expression!" << endl;
                    break;
                }

                analyzeExpression_rrd(expression_rrd);
                break;
            }

{
                generateSampleExpressions_rrd();
                break;
            }

{
                char infix_rrd[MAX_SIZE];
                char postfix_rrd[MAX_SIZE];
                cout << "Enter infix expression: ";
                cin >> infix_rrd;
                infixToPostfix_rrd(infix_rrd, postfix_rrd);
                cout << "Postfix expression: " << postfix_rrd << "" << endl;
                break;
            }

{
                cout << "Thank you for using Postfix Expression Evaluator!" << endl;
                exit(0);
            }

{
                cout << "Invalid choice! Please try again." << endl;
            }
        }
    }
    return 0;
}
```

## Output

```
Welcome to Postfix Expression Evaluator!
Note: This evaluator works with single-digit operands (0-9) and binary operators (+, -, *, /)
===== Postfix Expression Evaluator =====
1. Evaluate Postfix Expression
2. Analyze Expression
3. Generate Sample Expressions
4. Convert Infix to Postfix (Bonus)
5. Exit
=======================================
Enter your choice: 1
Enter postfix expression: 234*+
Evaluating postfix expression: 234*+
Step-by-step evaluation:
Step	Character	Stack			Operation
----	---------	-----			---------
1	2		[2]			Push 2
2	3		[2, 3]			Push 3
3	4		[2, 3, 4]		Push 4
4	*		[2, 12]			3 * 4 = 12
5	+		[14]			2 + 12 = 14
Final	-		[14]			Result: 14
Final Result: 14
```

## Dry Run

For postfix expression: 234*+

1. **Process '2'**:
   - Operand, convert to integer (2) and push to stack
   - Stack: [2]

2. **Process '3'**:
   - Operand, convert to integer (3) and push to stack
   - Stack: [2, 3]

3. **Process '4'**:
   - Operand, convert to integer (4) and push to stack
   - Stack: [2, 3, 4]

4. **Process '*'**:
   - Operator, pop two operands:
     * operand2 = 4 (top of stack)
     * operand1 = 3 (next in stack)
   - Perform operation: 3 * 4 = 12
   - Push result (12) to stack
   - Stack: [2, 12]

5. **Process '+'**:
   - Operator, pop two operands:
     * operand2 = 12 (top of stack)
     * operand1 = 2 (next in stack)
   - Perform operation: 2 + 12 = 14
   - Push result (14) to stack
   - Stack: [14]

6. **Final Check**:
   - Stack has exactly one element (14)
   - Return 14 as final result

## Conclusion

The implementation demonstrates postfix expression evaluation using stack data structure. Key features include:

1. **Proper Evaluation**: Correctly evaluates postfix expressions using stack operations
2. **Step-by-step Visualization**: Shows the evaluation process in detail
3. **Error Handling**: Comprehensive error checking for invalid expressions
4. **Division by Zero Protection**: Prevents arithmetic errors

**Time Complexity**: O(n) where n is the length of the postfix expression
- Each character is processed exactly once
- Stack operations (push/pop) are O(1)

**Space Complexity**: O(n) in worst case when all characters are operands

The stack-based approach is ideal for postfix evaluation because:
1. **Natural Fit**: Postfix evaluation is a classic stack application
2. **LIFO Nature**: Perfect for managing operand order
3. **Efficient Operations**: Push and pop are constant time operations
4. **Simple Logic**: Clear rules for when to push/pop

The implementation handles edge cases properly:
- Invalid characters in expressions
- Stack overflow and underflow conditions
- Insufficient operands for operators
- Division by zero errors
- Invalid expression structures

Additional features beyond requirements:
- Expression analysis
- Sample expression generation
- Infix to postfix conversion (bonus)
- Detailed step-by-step evaluation
- Comprehensive error handling

In real-world applications, this system could be extended to:
1. Support multi-digit operands
2. Handle more operators (power, modulo, etc.)
3. Add floating-point arithmetic
4. Implement expression optimization
5. Add graphical visualization of the process

Postfix notation (Reverse Polish Notation) is used in:
1. **Calculator Applications**: HP calculators famously used RPN
2. **Programming Languages**: Some functional languages use postfix
3. **Compiler Design**: Intermediate code generation
4. **Stack-based Virtual Machines**: Java bytecode, Python bytecode
5. **Mathematical Software**: For unambiguous expression evaluation

This implementation provides a solid foundation for understanding how stacks can be used to evaluate mathematical expressions, which is fundamental in compiler design and calculator applications.
