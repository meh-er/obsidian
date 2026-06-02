Correct way to index
```
int i;
pthread_t tid[10];
int values[10];

for (i = 0; i < 10; i++) {
    values[i] = i + 1; // Stores 1 through 10
    pthread_create(&tid[i], NULL, myfunc, &values[i]);
}
```

