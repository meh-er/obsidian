```
#include <stdio.h>
#include <stdlib.h>

int* create_scores() {
    int scores[3] = {92, 85, 77};
    return scores;
}

int main() {
    int *user_scores = create_scores();
    printf("First score: %d\n", user_scores[0]);
    return 0;
}
```

- int create_Scores returns scores, which is a local variable, but is then called in main. This would cause an error (returning pointers to local stack variables)

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void setup_username(char *input) {
    char *username = (char *)malloc(16 * sizeof(char));
    if (username == NULL) return;

    strcpy(username, input);
    printf("Username set to: %s\n", username);
    
    // Additional cleanup omitted for brevity
}

int main() {
    setup_username("Admin_User_Account_99");
    return 0;
}
```
- if username == NULL returns but does not free username (memory leaks)
- strcpy doesn't check the length of input, so username could be bigger than the size allocated, causing a buffer overflow

```
#include <stdio.h>
#include <stdlib.h>

void process_matrix(int size) {
    int *matrix = (int *)malloc(size * sizeof(int));
    if (matrix == NULL) return;

    // Initialize matrix
    for(int i = 0; i < size; i++) {
        matrix[i] = i * 2;
    }

    if (size > 10) {
        printf("Size is too large for standard processing.\n");
        return; 
    }

    printf("Processing complete for size %d.\n", size);
    free(matrix);
}
```
- memory leak - if (matrix == NULL) return without freeing matrix
- same with returning is size > 10, matrix not freed

```
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    char *name;
    int id;
} User;

void clean_up(User *u) {
    free(u);
    free(u->name);
}
```
- frees u before u-> name even though you use u to get u-> name? Use after free



```
#include <stdio.h>
#include <stdlib.h>

void execute_calculation() {
    int *data = (int *)malloc(5 * sizeof(int));
    // ... assume data is populated and used ...
    
    free(data);
    
    // ... generic logging code ...
    if (data != NULL) {
        printf("First element was: %d\n", data[0]);
    }
}
```
- use after free: printing after freeeing data, leads to unexpected behaviour