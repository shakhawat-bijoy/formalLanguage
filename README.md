Formal Languages and Compiler Lab Portfolio
===========================================

**Name:** Shakhawat Hossain Bijoy **Student ID:** 231071041  
**Department:** CSE **Semester:** 5th  
**Course Instructor:** MD TAHFIMUZZAMAN

Table of Contents
-----------------

*   1\. Introduction
*   2\. String Operations and Analysis

*   2.1 String Length Calculation
*   2.2 White Space Operations
*   2.3 Character Analysis

*   3\. Regular Expressions and Pattern Matching

*   3.1 Pattern a\* (Zero or More 'a')
*   3.2 Pattern a\*b+ (Complex Pattern)
*   3.3 Exact String Matching
*   3.4 String Tokenization

*   4\. Lexical Analysis

*   4.1 Comment Removal
*   4.2 Article Counter
*   4.3 Valid Identifier Checker

*   5\. ASCII Operations and Name Processing

*   5.1 ASCII Character Manipulation
*   5.2 Initial Extraction

*   6\. Expression Evaluation (Recursive Descent Parser)

*   6.1 Parser Implementation
*   6.2 Expression Evaluation with Precedence

*   7\. Three Address Code (TAC) Generation

*   7.1 TAC Generation Algorithm
*   7.2 Intermediate Code Examples

*   8\. Recursive Descent Parser

*   8.1 Grammar-based Parsing
*   8.2 Syntax Validation

*   9\. Infix to Postfix Conversion

*   9.1 Shunting Yard Algorithm
*   9.2 Stack-based Conversion

*   10\. Deterministic Finite Automata (DFA)

*   10.1 DFA for Strings Starting with "10"
*   10.2 DFA for Strings Ending with "01"
*   10.3 DFA for Exactly One '0'
*   10.4 DFA for Strings Containing "01"
*   10.5 DFA for Even Number of '0's

*   11\. Key Concepts and Learning Outcomes
*   12\. Conclusion

1\. Introduction 3
------------------

This portfolio presents a comprehensive collection of 10 lab tasks focusing on fundamental concepts in formal languages and compiler design. The tasks progress systematically from basic string manipulation to advanced topics like parsing, Three Address Code (TAC) generation, and Deterministic Finite Automata (DFA) implementation.

*   Master string analysis and manipulation techniques in C
*   Understand pattern matching using regular expressions
*   Develop lexical analysis skills for identifier recognition
*   Learn expression parsing and evaluation methods
*   Implement intermediate code generation (TAC)
*   Design and simulate finite automata for pattern recognition

Each task builds upon previous knowledge, creating a solid foundation in compiler construction principles and providing hands-on experience with the theoretical concepts taught in formal language theory.

2\. String Operations and Analysis 4
------------------------------------

### 2.1 String Length Calculation 4

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char str[100];
        int length = 0;
        
        printf("Enter a string: ");
        fgets(str, sizeof(str), stdin);
        
        // Remove newline character if present
        if (str[strlen(str) - 1] == '\n') {
            str[strlen(str) - 1] = '\0';
        }
        
        // Count characters manually
        while (str[length] != '\0') {
            length++;
        }
        
        printf("Length of the string is: %d\n", length);
        return 0;
    }
                

Sample Output:  
Enter a string: Hello World  
Length of the string is: 11

### 2.2 White Space Operations 5

#### Count White Spaces

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char str[100];
        int i = 0, spaceCount = 0;
        
        printf("Enter a string: ");
        fgets(str, sizeof(str), stdin);
        
        if (str[strlen(str) - 1] == '\n') {
            str[strlen(str) - 1] = '\0';
        }
        
        while (str[i] != '\0') {
            if (str[i] == ' ') {
                spaceCount++;
            }
            i++;
        }
        
        printf("Number of white spaces: %d\n", spaceCount);
        return 0;
    }
                

Sample Output:  
Enter a string: This is a test string  
Number of white spaces: 4

#### Remove White Spaces

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char str[100], result[100];
        int i = 0, j = 0;
        
        printf("Enter a string: ");
        fgets(str, sizeof(str), stdin);
        
        if (str[strlen(str) - 1] == '\n') {
            str[strlen(str) - 1] = '\0';
        }
        
        while (str[i] != '\0') {
            if (str[i] != ' ') {
                result[j] = str[i];
                j++;
            }
            i++;
        }
        result[j] = '\0';
        
        printf("String without white spaces: %s\n", result);
        return 0;
    }
                

Sample Output:  
Enter a string: Hello World Programming  
String without white spaces: HelloWorldProgramming

### 2.3 Character Analysis 6

#### C Keyword Checker

    #include <stdio.h>
    #include <string.h>
    
    const char* keywords[] = {
        "auto", "break", "case", "char", "const", "continue",
        "default", "do", "double", "else", "enum", "extern",
        "float", "for", "goto", "if", "int", "long", "register",
        "return", "short", "signed", "sizeof", "static", "struct",
        "switch", "typedef", "union", "unsigned", "void", "volatile",
        "while"
    };
    
    #define NUM_KEYWORDS (sizeof(keywords) / sizeof(keywords[0]))
    
    int isKeyword(const char* str) {
        for (int i = 0; i < NUM_KEYWORDS; i++) {
            if (strcmp(str, keywords[i]) == 0) {
                return 1;
            }
        }
        return 0;
    }
    
    int main() {
        char str[50];
        printf("Enter a string: ");
        scanf("%s", str);
        
        if (isKeyword(str)) {
            printf("\"%s\" is a C keyword.\n", str);
        } else {
            printf("\"%s\" is NOT a C keyword.\n", str);
        }
        return 0;
    }
                

Enter a string: int  
"int" is a C keyword.  
Enter a string: variable  
"variable" is NOT a C keyword.

#### Count Vowels, Consonants, and Digits

    #include <stdio.h>
    #include <ctype.h>
    
    int main() {
        char str[200];
        int vowels = 0, consonants = 0, digits = 0;
        
        printf("Enter a string: ");
        fgets(str, sizeof(str), stdin);
        for (int i = 0; str[i] != '\0'; i++) {
            char ch = tolower(str[i]);
            if (ch >= 'a' && ch <= 'z') {
                if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
                    vowels++;
                else
                    consonants++;
            } else if (ch >= '0' && ch <= '9') {
                digits++;
            }
        }
        printf("Vowels: %d\nConsonants: %d\nDigits: %d\n", vowels, consonants, digits);
        return 0;
    }
                

Enter a string: Hello123World  
Vowels: 3  
Consonants: 7  
Digits: 3

3\. Regular Expressions and Pattern Matching 8
----------------------------------------------

### 3.1 Pattern a\* (Zero or More 'a') 8

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char str[100];
        int isValid = 1;
        
        printf("Enter a string: ");
        scanf("%s", str);
        
        for (int i = 0; str[i] != '\0'; i++) {
            if (str[i] != 'a') {
                isValid = 0;
                break;
            }
        }
        
        if (isValid) {
            printf("Accepted (Matches a*)\n");
        } else {
            printf("Rejected (Does not match a*)\n");
        }
        
        return 0;
    }
                

Enter a string: aaa  
Accepted (Matches a\*)  
Enter a string: aab  
Rejected (Does not match a\*)  
Enter a string:  
Accepted (Matches a\*)

### 3.2 Pattern a\*b+ (Complex Pattern) 9

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char str[100];
        int i = 0, len, isValid = 1;
        
        printf("Enter a string: ");
        scanf("%s", str);
        len = strlen(str);
        
        // Skip all 'a' characters
        while (str[i] == 'a') {
            i++;
        }
        
        // Count 'b' characters
        int bCount = 0;
        while (str[i] == 'b') {
            bCount++;
            i++;
        }
        
        // Check if we've consumed all characters and have at least one 'b'
        if (i != len || bCount == 0) {
            isValid = 0;
        }
        
        if (isValid) {
            printf("Accepted (Matches a*b+)\n");
        } else {
            printf("Rejected (Does not match a*b+)\n");
        }
        
        return 0;
    }
                

Enter a string: aaabb  
Accepted (Matches a\*b+)  
Enter a string: b  
Accepted (Matches a\*b+)  
Enter a string: aaa  
Rejected (Does not match a\*b+)

### 3.3 Exact String Matching 10

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char str[100];
        
        printf("Enter a string: ");
        scanf("%s", str);
        
        if (strcmp(str, "abb") == 0) {
            printf("Accepted (Exact match for 'abb')\n");
        } else {
            printf("Rejected (Does not match 'abb')\n");
        }
        
        return 0;
    }
                

Enter a string: abb  
Accepted (Exact match for 'abb')  
Enter a string: abc  
Rejected (Does not match 'abb')

### 3.4 String Tokenization 7

#### String Tokenization with strtok()

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char str[200];
        printf("Enter a string: ");
        fgets(str, sizeof(str), stdin);
        str[strcspn(str, "\n")] = '\0';
        char* token = strtok(str, " ,.-!?\t");
        printf("Tokens found:\n");
        while (token != NULL) {
            printf("%s\n", token);
            token = strtok(NULL, " ,.-!?\t");
        }
        return 0;
    }
                

Enter a string: Hello, world! How are you?  
Tokens found:  
Hello  
world  
How  
are  
you

#### Count Tokens

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char str[200];
        int tokenCount = 0;
        printf("Enter a string: ");
        fgets(str, sizeof(str), stdin);
        str[strcspn(str, "\n")] = '\0';
        char* token = strtok(str, " ,.-!?\t");
        while (token != NULL) {
            tokenCount++;
            token = strtok(NULL, " ,.-!?\t");
        }
        printf("Total tokens found: %d\n", tokenCount);
        return 0;
    }
                

Enter a string: The quick brown fox jumps over the lazy dog.  
Total tokens found: 9

4\. Lexical Analysis 11
-----------------------

### 4.1 Comment Removal 11

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char code[5000] = "";
        char line[500];
        
        printf("Enter your code (type '#' in a new line to finish):\n");
        while (1) {
            fgets(line, sizeof(line), stdin);
            if (line[0] == '#' && line[1] == '\n')
                break;
            strcat(code, line);
        }
        
        for (int i = 0; code[i] != '\0'; i++) {
            if (code[i] == '/' && code[i + 1] == '/') {
                // Skip single-line comment
                while (code[i] != '\n' && code[i] != '\0')
                    i++;
            } else if (code[i] == '/' && code[i + 1] == '*') {
                // Skip multi-line comment
                i += 2;
                while (!(code[i] == '*' && code[i + 1] == '/') && code[i] != '\0')
                    i++;
                i += 1;
            } else {
                putchar(code[i]);
            }
        }
        
        return 0;
    }
                

Sample Input/Output:  
int main() {  
// This is a comment  
int x = 5; /\* This is also a comment \*/  
return 0;  
}  
#  
Output:  
int main() {  
  
int x = 5;  
return 0;  
}

### 4.2 Article Counter 12

    #include <stdio.h>
    #include <string.h>
    #include <ctype.h>
    
    int main() {
        char str[1000], word[10];
        int a = 0, an = 0, the = 0;
        int i = 0, j = 0;
        
        printf("Enter a sentence: ");
        fgets(str, sizeof(str), stdin);
        
        while (str[i]) {
            if (isalpha(str[i])) {
                word[j++] = tolower(str[i]);
            } else {
                if (j > 0) {
                    word[j] = '\0';
                    if (strcmp(word, "a") == 0) a++;
                    else if (strcmp(word, "an") == 0) an++;
                    else if (strcmp(word, "the") == 0) the++;
                    j = 0;
                }
            }
            i++;
        }
        
        // Check last word
        if (j > 0) {
            word[j] = '\0';
            if (strcmp(word, "a") == 0) a++;
            else if (strcmp(word, "an") == 0) an++;
            else if (strcmp(word, "the") == 0) the++;
        }
        
        printf("a: %d\nan: %d\nthe: %d\n", a, an, the);
        return 0;
    }
                

Enter a sentence: The quick brown fox jumps over a lazy dog and an elephant.  
a: 1  
an: 1  
the: 1

### 4.3 Valid Identifier Checker 13

    #include <stdio.h>
    #include <ctype.h>
    #include <string.h>
    
    int main() {
        char str[100];
        int i, valid = 1;
        
        printf("Enter an identifier: ");
        scanf("%s", str);
        
        // First character must be letter or underscore
        if (!(isalpha(str[0]) || str[0] == '_')) {
            valid = 0;
        }
        
        // Remaining characters must be alphanumeric or underscore
        for (i = 1; str[i]; i++) {
            if (!(isalnum(str[i]) || str[i] == '_')) {
                valid = 0;
                break;
            }
        }
        
        if (valid)
            printf("Valid identifier\n");
        else
            printf("Invalid identifier\n");
            
        return 0;
    }
                

Enter an identifier: \_variable123  
Valid identifier  
Enter an identifier: 123variable  
Invalid identifier  
Enter an identifier: my\_var  
Valid identifier

5\. ASCII Operations and Name Processing 14
-------------------------------------------

### 5.1 ASCII Character Manipulation 14

#### Next ASCII Characters

    #include <stdio.h>
    
    int main() {
        char c1, c2, c3;
        
        printf("Enter 3 characters: ");
        scanf(" %c %c %c", &c1, &c2, &c3);
        
        printf("Next ASCII characters: %c %c %c\n", c1 + 1, c2 + 1, c3 + 1);
        return 0;
    }
                

Enter 3 characters: a b c  
Next ASCII characters: b c d

#### ASCII Value and Offset

    #include <stdio.h>
    
    int main() {
        char ch;
        
        printf("Enter a character: ");
        scanf(" %c", &ch);
        
        printf("ASCII of %c: %d\n", ch, ch);
        printf("ASCII 5 steps ahead: %d (%c)\n", ch + 5, ch + 5);
        return 0;
    }
                

Enter a character: A  
ASCII of A: 65  
ASCII 5 steps ahead: 70 (F)

### 5.2 Initial Extraction 15

#### Extract Initials

    #include <stdio.h>
    
    int main() {
        char first[50], last[50];
        
        printf("Enter first and last name: ");
        scanf("%s %s", first, last);
        
        printf("Initials: %c.%c.\n", first[0], last[0]);
        return 0;
    }
                

Enter first and last name: John Doe  
Initials: J.D.

#### Full Name Initials

    #include <stdio.h>
    #include <string.h>
    
    int main() {
        char name[100];
        int i;
        
        printf("Enter full name (up to 3 words): ");
        fgets(name, sizeof(name), stdin);
        
        for (i = 0; name[i] != '\0'; i++) {
            if (i == 0 && name[i] != ' ') {
                printf("%c.", name[i]);
            } else if (name[i] == ' ' && name[i + 1] != ' ' && 
                       name[i + 1] != '\0' && name[i + 1] != '\n') {
                printf("%c.", name[i + 1]);
            }
        }
        printf("\n");
        return 0;
    }
                

Enter full name (up to 3 words): Shakhawat Hossain Bijoy  
S.H.B.

6\. Expression Evaluation (Recursive Descent Parser) 16
-------------------------------------------------------

### 6.1 Parser Implementation 16

    #include <stdio.h>
    #include <stdlib.h>
    #include <ctype.h>
    #include <math.h>
    #include <string.h>
    
    char input[100];
    int pos = 0;
    
    int getNextToken() {
        while (input[pos] == ' ')
            pos++;
        return input[pos++];
    }
    
    void putBackToken() {
        pos--;
    }
    
    int parseExpr();
    int parseTerm();
    int parsePower();
    
    int parseFactor() {
        int token = getNextToken();
        
        if (isdigit(token)) {
            int value = token - '0';
            while (isdigit(input[pos])) {
                value = value * 10 + (input[pos++] - '0');
            }
            return value;
        } else if (token == '(') {
            int result = parseExpr();
            if (getNextToken() != ')') {
                printf("Error: Missing ')'\n");
                exit(1);
            }
            return result;
        } else {
            printf("Error: Expected number or '('\n");
            exit(1);
        }
    }
    
    int parsePower() {
        int base = parseFactor();
        int token = getNextToken();
        
        if (token == '^') {
            int exponent = parsePower();
            return pow(base, exponent);
        } else {
            putBackToken();
            return base;
        }
    }
    
    int parseTerm() {
        int result = parsePower();
        int token = getNextToken();
        
        while (token == '*' || token == '/') {
            if (token == '*') {
                result *= parsePower();
            } else {
                int divisor = parsePower();
                if (divisor == 0) {
                    printf("Error: Division by zero\n");
                    exit(1);
                }
                result /= divisor;
            }
            token = getNextToken();
        }
        
        putBackToken();
        return result;
    }
    
    int parseExpr() {
        int result = parseTerm();
        int token = getNextToken();
        
        while (token == '+' || token == '-') {
            if (token == '+') {
                result += parseTerm();
            } else {
                result -= parseTerm();
            }
            token = getNextToken();
        }
        
        putBackToken();
        return result;
    }
    
    int main() {
        printf("Enter an arithmetic expression: ");
        fgets(input, sizeof(input), stdin);
        
        size_t len = strlen(input);
        if (len > 0 && input[len - 1] == '\n') {
            input[len - 1] = '\0';
        }
        
        int result = parseExpr();
        printf("Result: %d\n", result);
        return 0;
    }
                

Enter an arithmetic expression: 3 + 4 \* 2  
Result: 11  
Enter an arithmetic expression: (5 + 3) \* 2  
Result: 16  
Enter an arithmetic expression: 2^3 + 1  
Result: 9

7\. Three Address Code (TAC) Generation 18
------------------------------------------

### 7.1 TAC Generation Algorithm 18

    #include <stdio.h>
    #include <string.h>
    #include <stdlib.h>
    #include <ctype.h>
    
    #define MAX 100
    int tempVarCount = 1;
    
    int isValidIdentifier(char *s) {
        if (!isalpha(s[0]))
            return 0;
        for (int i = 1; s[i]; i++) {
            if (!isalnum(s[i]))
                return 0;
        }
        return 1;
    }
    
    void getTemp(char *temp) {
        sprintf(temp, "t%d", tempVarCount++);
    }
    
    int main() {
        char input[MAX], lhs[20];
        char tokens[50][20];
        int tokenCount = 0;
        
        printf("Enter expression (e.g., a = b + c + d + e):\n> ");
        fgets(input, MAX, stdin);
        input[strcspn(input, "\n")] = '\0';
        
        char *token = strtok(input, " ");
        while (token != NULL) {
            strcpy(tokens[tokenCount++], token);
            token = strtok(NULL, " ");
        }
        
        if (tokenCount < 5 || strcmp(tokens[1], "=") != 0) {
            printf("Error: Invalid format. Use format like: a = b + c + d\n");
            return 1;
        }
        
        strcpy(lhs, tokens[0]);
        if (!isValidIdentifier(lhs)) {
            printf("Error: Invalid identifier on LHS.\n");
            return 1;
        }
        
        printf("\nThree Address Code:\n");
        
        char prevTemp[20], temp[20];
        char op1[20], op2[20], oper;
        
        strcpy(op1, tokens[2]);
        strcpy(op2, tokens[4]);
        oper = tokens[3][0];
        
        getTemp(temp);
        printf("%s = %s %c %s\n", temp, op1, oper, op2);
        strcpy(prevTemp, temp);
        
        for (int i = 5; i < tokenCount; i += 2) {
            if (i + 1 >= tokenCount) {
                printf("Error: Operator without operand.\n");
                return 1;
            }
            
            oper = tokens[i][0];
            strcpy(op2, tokens[i + 1]);
            
            getTemp(temp);
            printf("%s = %s %c %s\n", temp, prevTemp, oper, op2);
            strcpy(prevTemp, temp);
        }
        
        printf("%s = %s\n", lhs, prevTemp);
        return 0;
    }
                

Enter expression (e.g., a = b + c + d + e):  
\> a = b + c \* d + e  
  
Three Address Code:  
t1 = b + c  
t2 = t1 \* d  
t3 = t2 + e  
a = t3

### 7.2 Intermediate Code Examples 19

    Input: x = a + b + c
    Output:
    t1 = a + b
    t2 = t1 + c
    x = t2
    
    Input: result = p * q + r * s
    Output:
    t1 = p * q
    t2 = r * s
    t3 = t1 + t2
    result = t3
    

8\. Recursive Descent Parser 20
-------------------------------

### 8.1 Grammar-based Parsing 20

    #include <stdio.h>
    #include <ctype.h>
    #include <string.h>
    #include <stdlib.h>
    
    char input[100];
    int pos = 0;
    char currentChar;
    
    void error() {
        printf("Invalid Expression\n");
        exit(1);
    }
    
    void advance() {
        currentChar = input[pos++];
    }
    
    void match(char expected) {
        if (currentChar == expected)
            advance();
        else
            error();
    }
    
    void E();
    void Eprime();
    void T();
    void Tprime();
    void F();
    
    void E() {
        T();
        Eprime();
    }
    
    void Eprime() {
        if (currentChar == '+' || currentChar == '-') {
            char op = currentChar;
            advance();
            T();
            Eprime();
        }
    }
    
    void T() {
        F();
        Tprime();
    }
    
    void Tprime() {
        if (currentChar == '*' || currentChar == '/') {
            char op = currentChar;
            advance();
            F();
            Tprime();
        }
    }
    
    void F() {
        if (isalpha(currentChar)) {
            advance();
        } else if (currentChar == '(') {
            advance();
            E();
            if (currentChar == ')') {
                advance();
            } else {
                error();
            }
        } else {
            error();
        }
    }
    
    int main() {
        printf("Enter an expression: ");
        fgets(input, sizeof(input), stdin);
        input[strcspn(input, "\n")] = '\0';
        
        pos = 0;
        advance();
        E();
        
        if (currentChar == '\0')
            printf("Expression is Valid\n");
        else
            printf("Invalid Expression\n");
            
        return 0;
    }
                

Enter an expression: a+b\*c  
Expression is Valid  
Enter an expression: (a+b)\*c  
Expression is Valid  
Enter an expression: a++b  
Invalid Expression

### 8.2 Syntax Validation 21

    E  → T E'
    E' → + T E' | - T E' | ε
    T  → F T'
    T' → * F T' | / F T' | ε
    F  → id | ( E )
    

This grammar ensures proper operator precedence and associativity.

9\. Infix to Postfix Conversion 22
----------------------------------

### 9.1 Shunting Yard Algorithm 22

    #include <stdio.h>
    #include <stdlib.h>
    #include <ctype.h>
    
    #define MAX 100
    
    char stack[MAX];
    int top = -1;
    
    void push(char c) {
        stack[++top] = c;
    }
    
    char pop() {
        if (top == -1)
            return -1;
        return stack[top--];
    }
    
    char peek() {
        if (top == -1)
            return -1;
        return stack[top];
    }
    
    int precedence(char op) {
        if (op == '+' || op == '-')
            return 1;
        if (op == '*' || op == '/')
            return 2;
        return 0;
    }
    
    void infixToPostfix(char *exp) {
        char *e = exp;
        char ch;
        
        printf("Postfix: ");
        
        while (*e != '\0') {
            if (isalnum(*e)) {
                printf("%c ", *e);
            } else if (*e == '(') {
                push(*e);
            } else if (*e == ')') {
                while ((ch = pop()) != '(')
                    printf("%c ", ch);
            } else {
                while (precedence(peek()) >= precedence(*e))
                    printf("%c ", pop());
                push(*e);
            }
            e++;
        }
        
        while (top != -1)
            printf("%c ", pop());
        
        printf("\n");
    }
    
    int main() {
        char expression[MAX];
        
        printf("Enter infix expression (e.g., a+b*c): ");
        scanf("%s", expression);
        
        infixToPostfix(expression);
        return 0;
    }
                

Enter infix expression (e.g., a+b\*c): a+b\*c  
Postfix: a b c \* +  
Enter infix expression (e.g., a+b\*c): (a+b)\*c  
Postfix: a b + c \*  
Enter infix expression (e.g., a+b\*c): a+b\*c-d/e  
Postfix: a b c \* + d e / -

### 9.2 Stack-based Conversion 23

The algorithm works by:  
1\. **Operands**: Output directly to postfix expression  
2\. **Left Parenthesis**: Push onto stack  
3\. **Right Parenthesis**: Pop and output until left parenthesis is found  
4\. **Operators**: Pop operators with higher or equal precedence, then push current operator  
5\. **End of Expression**: Pop all remaining operators from stack  
  
**Precedence Rules:**

*   \*, / have precedence 2
*   +, - have precedence 1
*   (, ) are handled specially

10\. Deterministic Finite Automata (DFA) 24
-------------------------------------------

### 10.1 DFA for Strings Starting with "10" 24

    #include <stdio.h>
    #include <string.h>
    
    int dfa_startsWith10(char *str) {
        int state = 0;
        
        for (int i = 0; str[i] != '\0'; i++) {
            char ch = str[i];
            
            switch (state) {
                case 0:
                    if (ch == '1')
                        state = 1;
                    else
                        state = 3; // reject state
                    break;
                case 1:
                    if (ch == '0')
                        state = 2; // accept state
                    else
                        state = 3; // reject state
                    break;
                case 2:
                    if (ch == '0' || ch == '1')
                        state = 2; // stay in accept state
                    else
                        state = 3; // reject state
                    break;
                case 3:
                    return 0; // reject
            }
        }
        
        return state == 2;
    }
    
    int main() {
        char input[100];
        
        printf("Enter a binary string: ");
        scanf("%s", input);
        
        if (dfa_startsWith10(input))
            printf("Accepted: String starts with '10'\n");
        else
            printf("Rejected: Does NOT start with '10'\n");
            
        return 0;
    }
                

Enter a binary string: 101010  
Accepted: String starts with '10'  
Enter a binary string: 110101  
Rejected: Does NOT start with '10'  
Enter a binary string: 10  
Accepted: String starts with '10'

**State Diagram:**

State 0 (Start): 
  - Input '1' → State 1
  - Input '0' → State 3 (Reject)
State 1:
  - Input '0' → State 2 (Accept)
  - Input '1' → State 3 (Reject)
State 2 (Accept):
  - Input '0' or '1' → State 2 (Stay)
State 3 (Reject):
  - Any input → Reject
                

### 10.2 DFA for Strings Ending with "01" 26

    #include <stdio.h>
    #include <string.h>
    
    int dfa_endsWith01(char *str) {
        int state = 0;
        
        for (int i = 0; str[i] != '\0'; i++) {
            char ch = str[i];
            
            switch (state) {
                case 0:
                    if (ch == '0') state = 1;
                    else if (ch == '1') state = 0;
                    else return 0;
                    break;
                case 1:
                    if (ch == '0') state = 1;
                    else if (ch == '1') state = 2;
                    else return 0;
                    break;
                case 2:
                    if (ch == '0') state = 1;
                    else if (ch == '1') state = 0;
                    else return 0;
                    break;
            }
        }
        
        return state == 2;
    }
    
    int main() {
        char input[100];
        
        printf("Enter a binary string: ");
        scanf("%s", input);
        
        if (dfa_endsWith01(input))
            printf("Accepted: String ends with '01'\n");
        else
            printf("Rejected: Does NOT end with '01'\n");
            
        return 0;
    }
                

Enter a binary string: 110101  
Accepted: String ends with '01'  
Enter a binary string: 101010  
Rejected: Does NOT end with '01'  
Enter a binary string: 01  
Accepted: String ends with '01'

**State Diagram:**

State 0 (Start):
  - Input '0' → State 1
  - Input '1' → State 0
State 1:
  - Input '0' → State 1
  - Input '1' → State 2
State 2 (Accept):
  - Input '0' → State 1
  - Input '1' → State 0
                

### 10.3 DFA for Exactly One '0' 28

    #include <stdio.h>
    #include <string.h>
    
    int dfa_exactlyOneZero(char *str) {
        int state = 0;
        
        for (int i = 0; str[i] != '\0'; i++) {
            char ch = str[i];
            
            switch (state) {
                case 0: // no zeros seen
                    if (ch == '0') state = 1;
                    else if (ch == '1') state = 0;
                    else return 0;
                    break;
                case 1: // exactly one zero seen
                    if (ch == '0') state = 2; // too many zeros
                    else if (ch == '1') state = 1;
                    else return 0;
                    break;
                case 2: // more than one zero seen
                    return 0;
            }
        }
        
        return state == 1;
    }
    
    int main() {
        char input[100];
        
        printf("Enter a binary string: ");
        scanf("%s", input);
        
        if (dfa_exactlyOneZero(input))
            printf("Accepted: String contains exactly one '0'\n");
        else
            printf("Rejected: Does NOT contain exactly one '0'\n");
            
        return 0;
    }
                

Enter a binary string: 11011  
Accepted: String contains exactly one '0'  
Enter a binary string: 11001  
Rejected: Does NOT contain exactly one '0'  
Enter a binary string: 1111  
Rejected: Does NOT contain exactly one '0'

**State Diagram:**

State 0 (Start - No zeros):
  - Input '0' → State 1
  - Input '1' → State 0
State 1 (Accept - Exactly one zero):
  - Input '0' → State 2 (Reject)
  - Input '1' → State 1
State 2 (Reject - More than one zero):
  - Any input → Reject
                

### 10.4 DFA for Strings Containing "01" 30

    #include <stdio.h>
    #include <string.h>
    
    int dfa_contains01(char *str) {
        int state = 0;
        
        for (int i = 0; str[i] != '\0'; i++) {
            char ch = str[i];
            
            switch (state) {
                case 0:
                    if (ch == '0')
                        state = 1;
                    else if (ch == '1')
                        state = 0;
                    else
                        return 0;
                    break;
                case 1:
                    if (ch == '1')
                        state = 2; // found "01"
                    else if (ch == '0')
                        state = 1;
                    else
                        return 0;
                    break;
                case 2:
                    state = 2; // stay in accept state
                    break;
            }
        }
        
        return state == 2;
    }
    
    int main() {
        char input[100];
        
        printf("Enter a binary string: ");
        scanf("%s", input);
        
        if (dfa_contains01(input))
            printf("Accepted: String contains '01'\n");
        else
            printf("Rejected: String does NOT contain '01'\n");
            
        return 0;
    }
                

Enter a binary string: 110100  
Accepted: String contains '01'  
Enter a binary string: 1111  
Rejected: String does NOT contain '01'  
Enter a binary string: 01  
Accepted: String contains '01'

### 10.5 DFA for Even Number of '0's 32

    #include <stdio.h>
    #include <string.h>
    
    int dfa_evenZeros(char *str) {
        int state = 0; // state 0: even number of zeros, state 1: odd number of zeros
        
        for (int i = 0; str[i] != '\0'; i++) {
            char ch = str[i];
            
            switch (state) {
                case 0: // even number of zeros
                    if (ch == '0')
                        state = 1; // now odd
                    else if (ch == '1')
                        state = 0; // stay even
                    else
                        return 0;
                    break;
                case 1: // odd number of zeros
                    if (ch == '0')
                        state = 0; // now even
                    else if (ch == '1')
                        state = 1; // stay odd
                    else
                        return 0;
                    break;
            }
        }
        
        return state == 0; // accept if even number of zeros
    }
    
    int main() {
        char input[100];
        
        printf("Enter a binary string: ");
        scanf("%s", input);
        
        if (dfa_evenZeros(input))
            printf("Accepted: Even number of '0's\n");
        else
            printf("Rejected: Odd number of '0's\n");
            
        return 0;
    }
                

Enter a binary string: 110011  
Accepted: Even number of '0's  
Enter a binary string: 10101  
Rejected: Odd number of '0's  
Enter a binary string: 1111  
Accepted: Even number of '0's (zero is even)

**State Diagram:**

State 0 (Accept - Even zeros):
  - Input '0' → State 1
  - Input '1' → State 0
State 1 (Reject - Odd zeros):
  - Input '0' → State 0
  - Input '1' → State 1
                

11\. Key Concepts and Learning Outcomes 34
------------------------------------------

### 11.1 String Manipulation Mastery

*   Manual string operations without built-in functions
*   Character-by-character processing
*   Memory management for efficient string operations
*   Pattern recognition in textual data

### 11.2 Pattern Matching and Regular Expressions

*   Finite state logic implementation in C
*   Pattern validation using algorithmic approaches
*   Complex pattern recognition

### 11.3 Lexical Analysis Fundamentals

*   Token recognition and classification
*   Comment removal from source code
*   Identifier validation according to language rules
*   Article counting for NLP

### 11.4 Parsing and Syntax Analysis

*   Recursive descent parsing for expression evaluation
*   Grammar-based validation using formal rules
*   Operator precedence handling
*   Syntax tree construction concepts

### 11.5 Intermediate Code Generation

*   Intermediate representation design
*   Temporary variable management
*   Expression decomposition for optimization
*   Code transformation techniques

### 11.6 Expression Processing

*   Infix to postfix conversion using stack algorithms
*   Operator precedence implementation
*   Parentheses handling in complex expressions
*   Postfix evaluation techniques

### 11.7 Finite Automata Design

*   State machine design principles
*   Pattern recognition using finite states
*   Multiple acceptance criteria handling
*   Transition function implementation

12\. Conclusion 36
------------------

This comprehensive portfolio represents a systematic journey through the fundamental concepts of formal languages and compiler design. The progression from basic string operations to complex parsing and automata design has provided invaluable hands-on experience with both theoretical concepts and practical implementations.

### 12.1 Technical Mastery Achieved

*   Advanced C programming techniques for system-level development
*   Memory management and efficient algorithm implementation
*   Error handling and robust input validation
*   Modular code design and function organization

### 12.2 Problem-Solving Development

1.  Analytical Thinking
2.  Algorithm Design
3.  State Management
4.  Error Handling
5.  Optimization

### 12.3 Real-World Applications

*   Text processing utilities and string manipulation tools
*   Input validation systems for web applications
*   Configuration file parsers and processors
*   Data extraction and transformation utilities

### 12.4 Academic and Professional Growth

*   Mastery of formal language theory concepts
*   Practical implementation of theoretical algorithms
*   Comprehensive understanding of compiler design phases
*   Ability to translate theory into working code

### 12.5 Future Directions

*   LR and LALR parsing techniques
*   Semantic analysis and type checking
*   Code optimization algorithms
*   Target code generation strategies
*   Research opportunities
*   Professional development

### 12.6 Personal Reflection

This journey through formal languages and compiler design has been transformative, providing not just technical skills but also a deeper appreciation for the elegance of computational theory and its practical applications. The progression from basic string manipulation to sophisticated parsing systems illustrates the power of systematic learning and incremental skill building.

*   Theory and Practice Integration
*   Systematic Approach
*   Problem Decomposition
*   Code Quality

The skills and knowledge gained through these exercises will serve as a solid foundation for continued growth in computer science, whether in academic research, software development, or innovative technology creation. The journey continues with confidence and excitement for the advanced topics that lie ahead.

**Submitted By:** Shakhawat Hossain Bijoy  
**Student ID:** 231071041  
**Department:** Computer Science and Engineering  
**Semester:** 5th  
**Course Instructor:** MD TAHFIMUZZAMAN  
**Submission Date:** 01/08/2025  

© 2025 Shakhawat Hossain Bijoy | Formal Languages and Compiler Lab Portfolio