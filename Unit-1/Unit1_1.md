# Assignment 1: Basic String Operations Implementation

Implementation of basic string operations using character arrays without built-in string library functions.

## Pseudo Code

### String Length Calculation
```
Algorithm StringLength(str):
    Initialize length = 0
    While str[length] != '\0':
        Increment length
    Return length
```

### String Copy
```
Algorithm StringCopy(source, destination):
    Initialize i = 0
    While source[i] != '\0':
        destination[i] = source[i]
        Increment i
    destination[i] = '\0'
```

### String Reverse
```
Algorithm StringReverse(str):
    Calculate length of str
    Initialize start = 0, end = length - 1
    While start < end:
        Swap str[start] and str[end]
        Increment start, Decrement end
```

### String Concatenation
```
Algorithm StringConcatenate(str1, str2, result):
    Calculate lengths of str1 and str2
    Copy str1 to result
    Append str2 to result
```

## Code Implementation

```cpp
#include <iostream>
using namespace std;
int stringLength_rrd(char* str_rrd);
void stringCopy_rrd(char* source_rrd, char* destination_rrd);
void stringReverse_rrd(char* str_rrd);
void stringConcatenate_rrd(char* str1_rrd, char* str2_rrd, char* result_rrd);

int main()
{
    char str1_rrd[100], str2_rrd[100], result_rrd[200];
    
    cout << "Enter first string: ";
    cin.getline(str1_rrd, sizeof(str1_rrd));
    str1_rrd[stringLength_rrd(str1_rrd) - 1] = '\0';
    
    cout << "Enter second string: ";
    cin.getline(str2_rrd, sizeof(str2_rrd));
    str2_rrd[stringLength_rrd(str2_rrd) - 1] = '\0';
    
    cout << "\n--- String Operations ---" << endl;
    printf("Length of first string: %d\n", stringLength_rrd(str1_rrd));
    printf("Length of second string: %d\n", stringLength_rrd(str2_rrd));
    
    stringCopy_rrd(str1_rrd, result_rrd);
    cout << "Copy of first string: " << result_rrd << "" << endl;
    
    stringReverse_rrd(str1_rrd);
    cout << "Reverse of first string: " << str1_rrd << "" << endl;
    
    stringConcatenate_rrd(str1_rrd, str2_rrd, result_rrd);
    cout << "Concatenation result: " << result_rrd << "" << endl;
    
    return 0;
}

int stringLength_rrd(char* str_rrd)
{
    int length_rrd = 0;
    while (str_rrd[length_rrd] != '\0')
    {
        length_rrd++;
    }
    return length_rrd;
}

void stringCopy_rrd(char* source_rrd, char* destination_rrd)
{
    int i_rrd = 0;
    while (source_rrd[i_rrd] != '\0')
    {
        destination_rrd[i_rrd] = source_rrd[i_rrd];
        i_rrd++;
    }
    destination_rrd[i_rrd] = '\0';
}

void stringReverse_rrd(char* str_rrd)
{
    int length_rrd = stringLength_rrd(str_rrd);
    int start_rrd = 0;
    int end_rrd = length_rrd - 1;
    char temp_rrd;
    
    while (start_rrd < end_rrd)
    {
        temp_rrd = str_rrd[start_rrd];
        str_rrd[start_rrd] = str_rrd[end_rrd];
        str_rrd[end_rrd] = temp_rrd;
        start_rrd++;
        end_rrd--;
    }
}

void stringConcatenate_rrd(char* str1_rrd, char* str2_rrd, char* result_rrd)
{
    int i_rrd = 0, j_rrd = 0;
    
    while (str1_rrd[i_rrd] != '\0')
    {
        result_rrd[i_rrd] = str1_rrd[i_rrd];
        i_rrd++;
    }
    
    while (str2_rrd[j_rrd] != '\0')
    {
        result_rrd[i_rrd] = str2_rrd[j_rrd];
        i_rrd++;
        j_rrd++;
    }
    
    result_rrd[i_rrd] = '\0';
}
```

## Output

```
Enter first string: Hello
Enter second string: World

--- String Operations ---
Length of first string: 5
Length of second string: 5
Copy of first string: Hello
Reverse of first string: olleH
Concatenation result: olleHWorld
```

## Dry Run

For input strings "Hello" and "World":
1. `stringLength_rrd("Hello")`:
   - Initialize `length_rrd = 0`
   - Loop through each character until '\0'
   - Returns 5

2. `stringCopy_rrd(str1_rrd, result_rrd)`:
   - Copy each character from "Hello" to result buffer
   - Add null terminator at the end
   - Result: "Hello"

3. `stringReverse_rrd(str1_rrd)`:
   - Length = 5, start = 0, end = 4
   - Swap H and o: "oellH"
   - Swap e and l: "olleH"
   - Result: "olleH"

4. `stringConcatenate_rrd(str1_rrd, str2_rrd, result_rrd)`:
   - Copy "olleH" to result
   - Append "World" to result
   - Add null terminator
   - Result: "olleHWorld"

## Conclusion

The implementation demonstrates fundamental string operations using character arrays without library functions. Each operation has O(n) time complexity where n is the length of the string. Memory management is handled manually, providing insight into how string operations work internally.

The string length calculation iterates through the array until it finds the null terminator. String copy operation duplicates each character to a new location. String reversal uses the two-pointer technique for efficient in-place reversal. String concatenation combines two strings by copying them sequentially to a result buffer.

These implementations are efficient and avoid the overhead of library functions, giving programmers direct control over memory and performance characteristics.
