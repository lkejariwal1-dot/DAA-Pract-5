Task: 1

Code: 
#include <stdio.h>
#include <string.h>

#define MAX 100

void findLCS(char *X, char *Y) {
    int m = strlen(X);
    int n = strlen(Y);
    int L[m+1][n+1];

    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X[i-1] == Y[j-1])
                L[i][j] = L[i-1][j-1] + 1;
            else
                L[i][j] = (L[i-1][j] > L[i][j-1]) ? L[i-1][j] : L[i][j-1];
        }
    }

    int index = L[m][n];

    char lcsStr[index + 1];
    lcsStr[index] = '\0'; 
    
    int i = m, j = n;
    while (i > 0 && j > 0) {
        if (X[i-1] == Y[j-1]) {
            lcsStr[index-1] = X[i-1];
            i--;
            j--;
            index--;
        } else if (L[i-1][j] > L[i][j-1]) {
            i--;
        } else {
            j--;
        }
    }

    printf("Length of LCS: %d\n", L[m][n]);
    printf("LCS: %s\n", lcsStr);
}

int main() {
    
    char X[MAX], Y[MAX];
    printf("Enter first DNA sequence: ");
    scanf("%s", X);
    printf("Enter second DNA sequence: ");
    scanf("%s", Y);

    findLCS(X, Y);

    return 0;
}



Task: 2

Code:
#include <stdio.h>
#include <string.h>

#define MAX 100

void findLRS(char *S) {
    int n = strlen(S);
    int L[n+1][n+1];

    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (S[i-1] == S[j-1] && i != j)
                L[i][j] = L[i-1][j-1] + 1;
            else
                L[i][j] = (L[i-1][j] > L[i][j-1]) ? L[i-1][j] : L[i][j-1];
        }
    }

    int index = L[n][n];

    char lrsStr[index + 1];
    lrsStr[index] = '\0';

    int i = n, j = n;
    while (i > 0 && j > 0) {
        if (S[i-1] == S[j-1] && i != j) {
            lrsStr[index - 1] = S[i - 1];
            i--;
            j--;
            index--;
        } else if (L[i-1][j] > L[i][j-1]) {
            i--;
        } else {
            j--;
        }
    }

    printf("Length of Longest Repeating Subsequence: %d\n", L[n][n]);
    printf("Longest Repeating Subsequence: %s\n", lrsStr);
}

int main() {
    char S[MAX];

    printf("Enter the DNA sequence: ");
    scanf("%s", S);

    findLRS(S);

    return 0;
}

