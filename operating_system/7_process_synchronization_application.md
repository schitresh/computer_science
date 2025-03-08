## Producer Consumer
- Also known as Bounded Buffer Problem
- Details
  - We have a buffer of fixed size
  - Producer produces an item and puts it in the buffer
  - Consumer consumes an item by picking up from the buffer
- Problems
  - Both processes may try to update the buffer at the same time which can lead to data loss & inconsistency
  - Consumer might consume faster, so it might have to wait
  - Producer might produce faster which can lead to buffer overflow
  - There may be multiple producers & consumers, and same item may be processed multiple times
- Solution
  - Use a mutex for locking & unlocking the buffer
  - Use a semaphore for empty slots
  - Use a semaphore for occupied slots
- Variations
  - Unbounded buffer
  - Sleep and wake
    - Producer sleeps if consumer is not consuming
    - Consumer sleeps if producer is not producing
    - Each wake up the other when process starts
    - Problem
      - Producer starts when consumer was about to sleep
      - Consumer will sleep and afterwards producer as consumer is not consuming

```py
def producer():
  while True:
    wait(empty_slots)
    lock(buffer)
    # Put in buffer
    unlock(buffer)
    signal(occupied_slots)

def consumer():
  while True:
    wait(full_slots)
    lock(buffer)
    # Consume from buffer
    unlock(buffer)
    signal(occupied_slots)
```

## Dining Philosophers
- There is one chopstick/fork between two philosophers
- A philosopher can eat only if he picks up two chopsticks
- Deadlock will happen if all philosophers pick their left chopstick simultaneously. Solutions:
  - Odd philosophers pick left chopstick first & even ones pick right chopstick first
  - Both chopsticks should be available before picking up
- Solution
  - Mutex to ensure that only one philosopher attempts to pick up a fork at a time
  - One semaphore per philosopher
  - One state per philosopher (thinking, hungry, or eating)

```py
def philosopher(index):
  while True:
    think(index)
    take_forks(index)
    eat(index)
    put_forks(index)

def check(index):
  if state[index] == 'hungry' and state[left] != 'eating' and state[right] != 'eating':
    philosopher_semaphore[index].wait()
    state[index] = 'eating'

def take_forks(index):
  mutex.lock()
  state[index] = 'hungry'
  check(index)
  mutex.unlock()

def put_forks(index)
  mutex.lock()
  state[index] = 'thinking'
  check(left)
  check(right)
  mutex.unlock()
  philosopher_semaphore[index].signal()

def think(index):
  time.sleep(random.randint(1, 5))

def eat(index):
  time.sleep(random.randint(1, 3))
```

## Readers Writers
- A resoure (e.g. file) shared between multiple users or processes
  - Reading: Any number of readers can read the write_semaphore
    - No one is allowed to write because the changes won't be visible to readers
  - Writing: Only the writer is allowed access
    - No one else can write or read because the changes won't be visible to others
- Solution
  - Semaphore
    - Semaphore to control write action to the write_semaphore
    - Variable to track reader count
    - Mutex to control edits to reader count
  - Monitor
    - Gives equal chance to both readers & writers
    - If writer is active, readers queue up
    - If readers are active, writers queue up
- Types: Reader is given preference, Writer is given preference, Both have equal preference

```py
def writer():
  while True:
    wait(write_semaphore)

    # Write

    signal(write_semaphore)

def reader():
  while True:
    # Reader wants to enter
    wait(read_mutex)
    read_count += 1
    # Disable writer access, readers are being preferred
    if read_count == 1: wait(write_semaphore)
    signal(read_mutex)

    # Reading

    # Reader wants to exit
    wait(read_mutex)
    read_count -= 1
    # Enable writer access
    if read_count == 0: signal(write_semaphore)
    signal(read_mutex)
```

## Sleeping Barber
- Details
  - There is one barbar and a number of chairs for waiting customers
  - Customers arrive at random times and take a chair if available to wait
  - If no chairs are available, the customer leaves
  - When the barber is finished with a customer, he picks up the next customer
  - If there are no customers, the barber goes to sleep
- Solution
  - Semaphore for the barber's chair
  - Semaphore for the waiting chairs
  - Mutex to update waiting chairs
- It can become complex if multiple barbers are employed

```py
def barber():
  while True:
    barber_semaphore.wait()
    mutex.lock()

    if len(waiting_customers) > 0
      customer = waiting_customers.pop(0)
      mutex.unlock()

      cut_hair()
      customer_semaphore.signal()
    else:
      mutex.unlock()

def customer(index):
  mutex.lock()

  if len(waiting_customers) < number_of_chairs:
    waiting_customers.append(index)
    mutex.unlock()

    barber_semaphore.signal()
    customer_semaphore.wait()
    get_haircut()
  else:
    mutex.unlock()
```
