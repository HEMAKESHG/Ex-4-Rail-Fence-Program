# Ex-5 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.


# PROGRAM
```
#include <stdio.h>
#include <string.h>

void railFenceEncrypt(char str[], int rails) {
    int len = strlen(str);
    char code[rails][len];
    
    // Initialize the code matrix with empty spaces
    for (int i = 0; i < rails; i++) {
        for (int j = 0; j < len; j++) {
            code[i][j] = ' ';
        }
    }

    int row = 0, col = 0;
    int dirDown = 0;
    
    // Fill the matrix with the characters in a zigzag pattern
    for (int i = 0; i < len; i++) {
        code[row][col++] = str[i];
        
        // Change direction if we reach the top or bottom rail
        if (row == 0 || row == rails - 1) {
            dirDown = !dirDown;
        }
        
        // Move up or down
        row = dirDown ? row + 1 : row - 1;
    }

    // Print the encrypted message by reading the rows
    printf("Encrypted Message: ");
    for (int i = 0; i < rails; i++) {
        for (int j = 0; j < len; j++) {
            if (code[i][j] != ' ') {
                printf("%c", code[i][j]);
            }
        }
    }
    printf("\n");
}

void railFenceDecrypt(char str[], int rails) {
    int len = strlen(str);
    char code[rails][len];
    
    // Initialize the code matrix with empty spaces
    for (int i = 0; i < rails; i++) {
        for (int j = 0; j < len; j++) {
            code[i][j] = ' ';
        }
    }

    int row = 0, col = 0;
    int dirDown = 0;
    
    // Mark the positions where characters will go in the matrix
    for (int i = 0; i < len; i++) {
        code[row][col++] = '*';
        
        // Change direction if we reach the top or bottom rail
        if (row == 0 || row == rails - 1) {
            dirDown = !dirDown;
        }
        
        // Move up or down
        row = dirDown ? row + 1 : row - 1;
    }

    // Fill the matrix with the characters from the encrypted string
    int k = 0;
    for (int i = 0; i < rails; i++) {
        for (int j = 0; j < len; j++) {
            if (code[i][j] == '*' && k < len) {
                code[i][j] = str[k++];
            }
        }
    }

    // Now read the matrix in a zigzag manner to get the decrypted message
    row = 0, col = 0;
    dirDown = 0;
    
    printf("Decrypted Message: ");
    for (int i = 0; i < len; i++) {
        printf("%c", code[row][col++]);
        
        // Change direction if we reach the top or bottom rail
        if (row == 0 || row == rails - 1) {
            dirDown = !dirDown;
        }
        
        // Move up or down
        row = dirDown ? row + 1 : row - 1;
    }
    printf("\n");
}

int main() {
    char str[1000];
    int rails;

    printf("Enter a Secret Message: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0;  // Remove newline character if present

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    // Encrypt the message
    railFenceEncrypt(str, rails);

    // Decrypt the message
    railFenceDecrypt(str, rails);

    return 0;
}
```

# OUTPUT
![Screenshot 2025-04-08 234239](https://github.com/user-attachments/assets/6cdb14ef-c8ea-455e-8ac2-2db6f5e85c7d)


# RESULT
The program is executed successfully.
