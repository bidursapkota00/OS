```c
monitor dp {
    enum { THINKING, HUNGRY, EATING } state [5];
    condition self [5];

    void pickup(int i) {
        state [i] = HUNGRY;
        test (i);
        if (state [i] != EATING)
            self [i].wait();
    }
    void putdown(int i) {
        state [i] = THINKING;
        test ((i + 4) % 5);
        test ((i + 1) % 5);
    }
    void test(int i) {
        if ((state [(i + 4) % 5] != EATING) &&
            (state [i] == HUNGRY) &&
            (state [(i + 1) % 5] != EATING)) {
            state [i] = EATING;
            self [i].signal();
        }
    }
    initialization_code() {
        for (int i = 0; i < 5; i++)
            state [i] = THINKING;
    }
}

// Syntax of a Monitor
monitor monitor_name
{
    // shared variable declarations
    procedure P1 (...) { ... }
    procedure P2 (...) { ... }
    ...
    procedure Pn (...) { ... }
    initialization code (...) { ... }
}

// The structure of philosopher i
do {
    wait(chopstick[i]);
    wait(chopstick[(i + 1) % 5]);
    ....
    // eat
    signal(chopstick[i]);
    signal(chopstick[(i + 1) % 5]);
    // think
} while(TRUE);

// Reader
do {
    wait (mutex);
    readcnt++; // The number of readers has now increased by 1
    if (readcnt == 1)
        wait (wrt); // ensures no writer can enter if there is even one reader
    signal (mutex); // other readers can enter while this current reader is
                    // inside the critical section
    /* current reader performs reading here */
    wait (mutex);
    readcnt--; // a reader wants to leave
    if (readcnt == 0) // no reader is left in the critical section
        signal (wrt); // writers can enter
    signal (mutex); // reader leaves
} while(true);

// Writer
do {
    /* writer requests for critical section */
    wait(wrt);
    /* performs the write */
    // leaves the critical section
    signal(wrt);
} while(true);

// Producer
do {
    // 1. Wait until there is at least one empty slot
    wait(empty);
    // 2. Lock the buffer (Mutual Exclusion)
    wait(mutex);
    /* Critical Section: Add data to the buffer */
    // 3. Unlock the buffer
    signal(mutex);
    // 4. Increment the count of full slots
    signal(full);
} while(TRUE);

// Consumer
do {
    // 1. Wait until there is at least one full slot
    wait(full);
    // 2. Lock the buffer (Mutual Exclusion)
    wait(mutex);
    /* Critical Section: Remove data from the buffer */
    // 3. Unlock the buffer
    signal(mutex);
    // 4. Increment the count of empty slots
    signal(empty);
} while(TRUE);

// P0
wait(S);
wait(Q);
...
...
signal(S);
signal(Q);
```

```c
// P1
wait(Q);
wait(S);
...
...
signal(Q);
signal(S);
```

```c
// Binary semaphore initialized to 1
int S = 1;
// Defination of wait();
P (int S) {
    while (S <= 0) ; // do nothing
    S--;
}
// Defination of signal();
V (int S) {
    S++;
}

do {
    // non critical section

    while (turn != 0); // do nothing

        // critical section

    turn = 1; // exit critical section

    // remainder non critical section

} while (true);

// process 1
do {
    // non critical section

    while (turn != 1); // do nothing

        // critical section

    turn = 0; // exit critical section

    // remainder non critical section

} while (true);
```
