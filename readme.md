https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3

gpt https://chatgpt.com/c/67ae5619-15c4-8001-be16-ecbae5ca68b0

# unit 2 hasing **Double Hashing, Rehashing, Extendible Hashing, and Skip Lists**
The following information is extracted and structured based on **your uploaded document**. Below, you will find **definitions, advantages, disadvantages, applications, time complexities**, and a **detailed comparison table** for **Double Hashing, Rehashing, Extendible Hashing, and Skip Lists**.

---

# **1. Double Hashing**
### **Definition**  
Double hashing is an **open-addressing collision resolution technique** where a second **hash function** determines the probing sequence.  
It follows this formula:  
\[
h(k, i) = (h_1(k) + i \times h_2(k)) \mod m
\]
- **h₁(k)**: Primary hash function.  
- **h₂(k)**: Secondary hash function (must never return 0).  
- **i**: Probe number.

### **Advantages**  
✔ **Avoids clustering** (compared to linear/quadratic probing).  
✔ **More uniform key distribution**.  
✔ **Efficient in large hash tables**.  
✔ **Works well when load factor is high**.  
✔ **Prevents cyclic probing sequences**.

### **Disadvantages**  
✘ **Two hash computations per lookup (higher computational cost)**.  
✘ **Careful selection of h₂(k) is needed** (to prevent cycles).  
✘ **Not memory efficient for sparse datasets**.  
✘ **Requires prime table size for best performance**.  
✘ **Performance degrades as load factor approaches 1**.

### **Applications**  
✅ **Database indexing**.  
✅ **Memory management (hash-based caching systems)**.  
✅ **Cryptographic applications**.  
✅ **Symbol tables in compilers**.  
✅ **Hash-based lookup tables**.  

### **Time Complexity**
| Operation  | Best Case | Average Case | Worst Case |
|------------|----------|--------------|------------|
| **Insertion** | O(1) | O(1) | O(n) |
| **Deletion** | O(1) | O(1) | O(n) |
| **Search** | O(1) | O(1) | O(n) |

---

# **2. Rehashing**
### **Definition**  
Rehashing is a **technique used to resize hash tables** when the **load factor** exceeds a threshold. It involves:
1. **Creating a new hash table** with a larger size (typically doubled).
2. **Recomputing hash values** for all keys.
3. **Reinserting all elements** into the new table.

### **Advantages**  
✔ **Reduces collisions** by increasing table size.  
✔ **Improves search performance** in dynamic datasets.  
✔ **Prevents performance degradation due to clustering**.  
✔ **Load factor is maintained at an optimal level**.  
✔ **Ensures O(1) average search time**.

### **Disadvantages**  
✘ **Expensive operation** (all elements must be rehashed).  
✘ **Increased memory usage temporarily**.  
✘ **Interrupts ongoing operations** (can cause latency spikes).  
✘ **Choosing the right resizing factor is tricky**.  
✘ **May cause fragmentation issues**.

### **Applications**  
✅ **Dynamic hash-based data structures**.  
✅ **Database systems requiring dynamic growth**.  
✅ **Network routing tables**.  
✅ **Cryptographic hash tables**.  
✅ **Load balancing in distributed systems**.  

### **Time Complexity**
| Operation  | Best Case | Average Case | Worst Case |
|------------|----------|--------------|------------|
| **Insertion** | O(1) | O(1) | O(n) (when rehashing occurs) |
| **Deletion** | O(1) | O(1) | O(n) |
| **Search** | O(1) | O(1) | O(n) |

---

# **3. Extendible Hashing**
### **Definition**  
Extendible hashing is a **dynamic hashing technique** that grows/shrinks based on the number of elements.  
- Uses **directories** that map to **buckets**.
- The **global depth (GD)** determines how many bits are used for indexing.  
- **When a bucket overflows**, it **splits**, and the directory doubles if necessary.

### **Advantages**  
✔ **Efficient disk access** (minimizes I/O operations).  
✔ **Only required buckets are expanded**.  
✔ **Load factor remains optimal** (O(1) average lookup).  
✔ **No need to rehash all elements** like traditional rehashing.  
✔ **Supports dynamic insertions without performance degradation**.

### **Disadvantages**  
✘ **Directory size can grow exponentially**.  
✘ **Complex implementation**.  
✘ **Extra storage required for directories**.  
✘ **Splitting logic adds computational overhead**.  
✘ **Performance depends on the distribution of keys**.

### **Applications**  
✅ **Databases (e.g., dynamic indexing)**.  
✅ **File systems (used in NTFS, HFS+ for metadata storage)**.  
✅ **Large-scale data storage (Big Data systems)**.  
✅ **Dynamic hashing in distributed databases**.  
✅ **Efficient caching mechanisms**.  

### **Time Complexity**
| Operation  | Best Case | Average Case | Worst Case |
|------------|----------|--------------|------------|
| **Insertion** | O(1) | O(1) | O(log n) (in case of bucket splits) |
| **Deletion** | O(1) | O(1) | O(log n) |
| **Search** | O(1) | O(1) | O(log n) |

---

# **4. Skip Lists**
### **Definition**  
A **skip list** is a probabilistic data structure that maintains multiple levels of linked lists, where **higher levels skip more elements**, allowing **faster searches**.

### **Advantages**  
✔ **Faster than linked lists (O(log n) average search time)**.  
✔ **Dynamic resizing without rehashing**.  
✔ **Works well in concurrent applications**.  
✔ **Simpler than balanced trees (e.g., Red-Black Trees, AVL Trees)**.  
✔ **Good alternative to self-balancing trees**.

### **Disadvantages**  
✘ **Extra memory overhead** for storing multiple pointers per node.  
✘ **Insertion/deletion requires updating multiple levels**.  
✘ **Randomized balancing means performance is not always optimal**.  
✘ **Not cache-efficient compared to trees**.  
✘ **Higher space complexity (O(n log n))**.

### **Applications**  
✅ **Distributed databases (Cassandra, BigTable use skip lists)**.  
✅ **Concurrent programming (lock-free search structures)**.  
✅ **Memory management systems**.  
✅ **Alternative to balanced trees in certain scenarios**.  
✅ **Indexing in NoSQL databases**.  

### **Time Complexity**
| Operation  | Best Case | Average Case | Worst Case |
|------------|----------|--------------|------------|
| **Insertion** | O(1) | O(log n) | O(n) |
| **Deletion** | O(1) | O(log n) | O(n) |
| **Search** | O(1) | O(log n) | O(n) |

---

## **Comparison Table: Key Differences**
| **Feature** | **Double Hashing** | **Rehashing** | **Extendible Hashing** | **Skip Lists** |
|------------|----------------|--------------|------------------|-------------|
| **Concept** | Uses **two hash functions** to determine probes | **Resizes hash table** when load factor is high | **Uses dynamic directory & bucket expansion** | **Multi-level linked list with probabilistic balancing** |
| **Collision Handling** | Avoids clustering with secondary hash function | Reduces collisions by expanding table size | Splits buckets dynamically | Not applicable |
| **Performance Impact** | High if hash functions are not well chosen | Temporary slowdown during rehashing | Efficient for dynamic insertions | Logarithmic search time |
| **Resizing Required?** | No | Yes (expensive operation) | No (only expands when necessary) | No |
| **Memory Usage** | Low | High (during rehashing) | Higher (stores directory pointers) | High (multiple pointers per node) |
| **Best Used In** | **Static hash tables** | **Dynamic but rarely growing datasets** | **Databases, disk-based storage** | **Concurrent data access** |
| **Search Complexity** | **O(1) average** | **O(1) average** | **O(1) average** | **O(log n) average** |
| **Insert/Delete Complexity** | O(1) | O(1) (except during rehashing) | O(1) (except bucket splits) | O(log n) |
| **Use in Databases?** | No | Sometimes | Yes | Yes |
| **Use in Caching?** | Yes | No | No | Yes |

🚀 **Final Verdict**:  
✅ **Double Hashing** is best for **fast, static hash tables**.  
✅ **Rehashing** is used when **dynamic size adjustment is needed**.  
✅ **Extendible Hashing** is **best for databases**.  
✅ **Skip Lists** work well in **concurrent programming and indexing**.

https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
