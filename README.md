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
#include <stdlib.h>

char* encrypt(char* msg, int rails) {
    int len = strlen(msg), k = 0, row = 0, down = 1;
    char* enc = malloc(len + 1);
    char mat[rails][len];
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            mat[i][j] = '\0';

    for (int i = 0; i < len; i++) {
        mat[row][i] = msg[i];
        if (row == 0) down = 1;
        else if (row == rails - 1) down = 0;
        row += down ? 1 : -1;
    }

    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            if (mat[i][j]) enc[k++] = mat[i][j];
    enc[k] = '\0';
    return enc;
}

char* decrypt(char* msg, int rails) {
    int len = strlen(msg), k = 0, row = 0, down = 1;
    char* dec = malloc(len + 1);
    char mat[rails][len];
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            mat[i][j] = '\0';

    // Mark zigzag
    for (int i = 0; i < len; i++) {
        mat[row][i] = '*';
        if (row == 0) down = 1;
        else if (row == rails - 1) down = 0;
        row += down ? 1 : -1;
    }

    // Fill zigzag with ciphertext
    int idx = 0;
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            if (mat[i][j] == '*' && idx < len)
                mat[i][j] = msg[idx++];

    // Read zigzag
    row = 0; down = 1;
    for (int i = 0; i < len; i++) {
        dec[k++] = mat[row][i];
        if (row == 0) down = 1;
        else if (row == rails - 1) down = 0;
        row += down ? 1 : -1;
    }
    dec[k] = '\0';
    return dec;
}

int main() {
    char msg[100];
    int rails;
    printf("Message: ");
    fgets(msg, sizeof(msg), stdin);
    msg[strcspn(msg, "\n")] = 0;
    printf("Rails: ");
    scanf("%d", &rails);

    char* enc = encrypt(msg, rails);
    printf("Encrypted: %s\n", enc);
    char* dec = decrypt(enc, rails);
    printf("Decrypted: %s\n", dec);

    free(enc);
    free(dec);
    return 0;
}

```

# OUTPUT
![image](https://github.com/user-attachments/assets/38cd629f-5cf0-4d20-85a2-9e02384a6253)



# RESULT
The program is executed successfully.
