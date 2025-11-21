#include <stdio.h>

// Function to calculate string length (my_strlen)
int my_strlen(char *str) {
    int len = 0;
    while (str[len] != '\0') {
        len++;
    }
    return len;
}

// Function to compare two strings (my_strcmp)
int my_strcmp(char *str1, char *str2) {
    int i = 0;
    while (str1[i] != '\0' && str2[i] != '\0' && str1[i] == str2[i]) {
        i++;
    }
    return str1[i] - str2[i];
}

// Function to copy a string (my_strcpy)
void my_strcpy(char *dest, char *src) {
    int i = 0;
    while (src[i] != '\0') {
        dest[i] = src[i];
        i++;
    }
    dest[i] = '\0'; // Ensure destination is null-terminated
}

// Function to concatenate two strings (my_strcat)
void my_strcat(char *dest, char *src) {
    int dest_len = my_strlen(dest);
    int i = 0;
    while (src[i] != '\0') {
        dest[dest_len + i] = src[i];
        i++;
    }
    dest[dest_len + i] = '\0'; // Ensure concatenated string is null-terminated
}

// --- Validation Function ---

// Returns 1 if valid, 0 if invalid. Builds an error message in result_msg.
int validateEmail(char *email, char *result_msg) {
    int len = my_strlen(email);
    // Use my_strcpy to start building the message
    my_strcpy(result_msg, "Status: Invalid. Reason: ");

    if (len < 5) {
        my_strcat(result_msg, "Email is too short.");
        return 0;
    }

    int atPos = -1;
    int dotPos = -1;
    for (int i = 0; i < len; i++) {
   if (email[i] == '@') {
            if (atPos != -1) { // Found a second '@'
                my_strcat(result_msg, "Contains more than one '@' symbol.");
                return 0;
            }
            atPos = i;
        } else if (email[i] == '.') {
            dotPos = i;
        }
    }

    if (atPos == -1) {
        my_strcat(result_msg, "Missing '@' symbol.");
        return 0;
    }

    if (atPos == 0) {
        my_strcat(result_msg, "Missing local part (before '@').");
        return 0;
    }

    if (dotPos == -1 || dotPos < atPos) {
         my_strcat(result_msg, "Missing or misplaced '.' symbol after '@'.");
        return 0;
    }
    
    // If all checks pass
    my_strcpy(result_msg, "Status: Valid.");
    return 1;
}

// --- Main Function (Menu) ---

int main() {
    char email[100];
    char result[150];

   printf("\nEnter email address to validate (or type 'quit' to exit): ");
        scanf("%s", email);
        printf("Your email address:%s\n",email);
        // Use my_strcmp to check for the exit command
        if (my_strcmp(email, "quit") == 0) {
            printf("Exiting program. Goodbye!\n");
        
        }

        validateEmail(email, result);
        printf("%s\n", result);
    

    return 0;
}

