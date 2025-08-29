# Process Synchronization Solutions
## Lock variable
- 0 means CS is vacant
- Process entering CS sets it 1
- Doesn't provide mutual exclusion in some cases
- Busy Waiting

```py
while lock != 0: continue
lock = 1
# Critical Section
lock = 0
```

## Peterson's Solution
- Have 2 shared variables
  - bool flag[2]: Which processes wants to enter CS
  - int turn: Whose turn is to enter CS
- Satisfies all CS conditions
- Involves busy waiting (Pi waiting for Pj): not preferred because it wastes CPU cycles
- Limited to 2 processes at a time
- Cannot be used in modern architecture with multiple CPUs

```py
while (True):
  # Pi wants to enter CS
  flag[i] = True

  # Give preference to Pj to avoid conflicts
  turn = j
  # Wait if Pj is executing
  while (flat[j] && turn == j): continue

  # Critical Section

  flag[i] = False

  # Remainder Section
```

## Dekker's Solution
- One of the first mutual exclusion algorithms. The latest revision satisfies all 3 conditions of CS.
- Uses shared memory for communication
- Have 2 shared variables
  - bool flag[2]: Which processes wants to enter CS
  - int turn: Whose turn is to enter CS
- Involves busy waiting (Pi waiting for Pj)
- Limited to 2 processes at a time
- Cannot be used in modern architecture with multiple CPUs

```py
while (True):
  # Pi wants to enter CS
  flag[i] = True

  # Wait if Pj is executing
  while flat[j]:
    if turn == j:
      flag[i] = False
      while turn == j: continue
      flag[i] = True

  # Critical Section

  turn = j
  flag[i] = False

  # Remainder Section
```

## Bakery Algorithm
- Follows first come first serve
- Each process is assigned a number (ticket) in lexicographical order
- The process with the smallest ticket enters CS
- If the ticket number is same, then lower PID is given preference
- No deadlock, no starvation
- Not scalable (overhead increases with number of processes)
- High time complexity, Memory overhead, Busy waiting

```py
while True:
  choosing_number[i] = True
  number[i] = max(number) + 1
  choosing_number[i] = False

  for j in range(0, n):
    while choosing_number[j]: continue
    while number[j] != 0 and [number[j], j] < [number[i], i]: continue

  # Critical Section
  number[i] = 0
  # Remainder Section
```

## Semaphore
- Signaling mechanism: A process waiting on a semaphore will be signaled by another process
- Stores available resources in a variable
- Types: Counting semaphore, Binary semaphore
- Uses two atomic operations
  - Wait
    - Decrements the value for semaphore
    - The caller process will be blocked until another process performs a signal operation
  - Signal
    - Increments the value of semaphore
- Any process can release a resource by calling signal
- Limitations
  - Priority inversion
  - Deadlock
  - Busy waiting: To solve maintain a waiting queue

```py
int semaphore = S # Maximum number of processes that can enter CS at this time

def wait(semaphore):
  while semaphore <= 0: continue # Wait till CS is available
  semaphore -= 1

def signal(sempahore):
  semaphore += 1

# Process P
wait(semaphore)
# Critical Section
signal(semaphore)
# Remainder Section
```

## Mutex
- Mutual Exclusion Object
- Locking or ownership mechanism
- Unlike semaphore, it is not a variable but an object
- Operations
  - Lock
  - Unlock
- Only the process that has the lock can unlock the resource
- Can be used as Binary semaphore, but vice-versa is not true
- Priority inversion is solved by priority inheritance

```py
def lock():
  while not available: continue
  available = False

def unlock():
  available = True

# Process P
lock()
# Critical Section
unlock()
# Remainder Section
```

## Monitors
- A module that encapsulates a shared resource and provides access through a set of procedures
- Used to simplify implementation of concurrent programs by providing high level abstraction
- Provides mutual exclusion
- There are condition variables (with their own queues) on which wait and signal are performed
- Waiting processes are suspended and put in the queue of the condition variable
- Processes outside the monitor can't access internal variables but can call its procedures
- Eliminates the need for complex synchronization primitives like semaphores & mutex, but can be less efficient
