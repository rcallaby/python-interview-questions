# Question 01 - Data Types

## Can you explain why immutability is important in Python and describe scenarios where immutability offers advantages over mutable types? 

Immutability is a key concept in Python that ensures that an object's state cannot be modified after it is created. Immutable objects in Python include types like `int`, `float`, `str`, and `tuple`. Here’s why immutability is important and how it can be advantageous in certain scenarios:

---

### **Why Immutability Is Important**
1. **Predictable Behavior:**  
   Immutability prevents accidental changes to objects, making it easier to reason about the program and avoid subtle bugs caused by unintended mutations.

2. **Thread Safety:**  
   Immutable objects are inherently thread-safe since they cannot be changed, avoiding race conditions in multi-threaded environments.

3. **Hashability and Dictionary Keys:**  
   Immutable objects can be hashed (e.g., using `hash()`), making them suitable as keys in dictionaries or elements in sets.

4. **Performance Optimization:**  
   Immutable objects enable internal optimizations in Python, such as interning (e.g., for small integers and strings). These optimizations improve memory and computational efficiency.

---

### **Advantages of Immutability with Examples**

#### **1. Avoiding Side Effects**
With mutable types, changes to an object in one part of the program can inadvertently affect other parts. Immutable types prevent this.

```python
def add_to_list(lst, element):
    lst.append(element)
    return lst

# Mutable example
my_list = [1, 2, 3]
add_to_list(my_list, 4)
print(my_list)  # [1, 2, 3, 4] -> Unintended side effect!

# Immutable example
def add_to_tuple(tpl, element):
    return tpl + (element,)

my_tuple = (1, 2, 3)
new_tuple = add_to_tuple(my_tuple, 4)
print(my_tuple)   # (1, 2, 3) -> Original is unchanged
print(new_tuple)  # (1, 2, 3, 4)
```

#### **2. Thread Safety**
Immutable types can be shared between threads without risk of data corruption.

```python
from threading import Thread

shared_data = (1, 2, 3)  # Immutable tuple

def read_shared_data():
    print("Reading:", shared_data)

# Create multiple threads that read shared_data
threads = [Thread(target=read_shared_data) for _ in range(5)]
for t in threads:
    t.start()
for t in threads:
    t.join()
```
Since the tuple `shared_data` cannot be modified, it is safe to share across threads without synchronization mechanisms like locks.

#### **3. Using Immutable Keys in Dictionaries**
Immutable objects (e.g., `str` or `tuple`) can be used as dictionary keys, while mutable objects cannot.

```python
# Immutable tuple as key
locations = {
    (40.7128, -74.0060): "New York",
    (34.0522, -118.2437): "Los Angeles"
}
print(locations[(40.7128, -74.0060)])  # New York

# Mutable list as key -> Raises TypeError
# locations[[40.7128, -74.0060]] = "New York"
```

#### **4. Functional Programming**
Immutability is a cornerstone of functional programming, where functions avoid modifying external state.

```python
# Immutable: Pure function
def increment_tuple(tpl):
    return tuple(x + 1 for x in tpl)

original_tuple = (1, 2, 3)
new_tuple = increment_tuple(original_tuple)
print(original_tuple)  # (1, 2, 3) -> Unchanged
print(new_tuple)       # (2, 3, 4)
```

---

### **When to Use Immutability**

1. **Shared State Across Threads:**  
   Use immutability to avoid race conditions.
   
2. **Keys in Dictionaries or Elements in Sets:**  
   Use immutable types like `str` or `tuple` for reliable hashing.

3. **Functional Programming:**  
   Embrace immutability to improve predictability and avoid side effects.

4. **Caching and Memory Efficiency:**  
   Leverage Python's optimizations for immutable objects, such as string interning.

---

### **Comparison: Mutable vs Immutable**

| Feature                  | Mutable (e.g., `list`, `dict`)       | Immutable (e.g., `tuple`, `str`) |
|--------------------------|--------------------------------------|----------------------------------|
| Modifiable               | Yes                                | No                              |
| Thread Safety            | No                                 | Yes                             |
| Hashable (can be a key)  | No                                 | Yes                             |
| Performance Optimizations| Limited                            | Yes (e.g., interning)           |

By choosing immutability, you can make your code more predictable, safe, and performant, especially in scenarios where objects are shared across functions or threads.
