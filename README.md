# Common Data Structures and Algorithms

- Store data in a way that meets the needs of your application
- Trade-offs between how long it takes to first **populate the structure**, how long it takes to **add/find** elements

## Hash Tables

- A data structure that organises data in key-value pairs
- Also referred to as a `dictionary` or `associative array`
- Allow efficient access `O(1)`
- The basic idea of a hash table is to allow efficient access to data that is indexed by a key
- To implement a hash we need:
  - A place to store the table entries - typically relies on Array primitive data type
  - A way to assign key/value pairs to a specific position (index) inside the data store - hash function

> A hash function transforms the key into an index that can be used to lookup or update its associated value

```rb
# @params [key] - anything
# @returns Integer - this is the index of the array data store
def hash_function(key); end
```

Hash function implementations

- division method `integer % size` = index
- One way hash function(digest) over the key and then apply the division method to get the location

```rb
class FooHash
  def initialize(bucket_size = 256)
    @store = [].tap do |arr|
      (0..bucket_size).each { |i| arr << [] }
    end
  end

  def []=(key)
    store[digest(key)]
  end

  private

  attr_reader :store

  def digest(key)
  end
end
```

Handling collisions

- Double hashing
- Linear probing
- Separate chaining (use a linked a list)

## Big O Analysis

### O(1)

An algorithm that will always execute in the same time (or space) regardless of the size of the dataset

```ts
bool IsFirstElementNumm(IList<string> elements) {
  return elements[0] == null;
}
```

### O(N)

An algorithm where the performance degrades linearly; directly proportional to the size of the data set

```ts
bool ContainsValue(IList<string> elements, string value) {
  foreach (var element in elements) {
    if (element == value) return true;
  }
  return false;
}
```

### O(log N)

Produces a growth curve that peaks at the beginning and slowly flattens out as the size of the data sets increases

E.g.

If an input data set containing 10 items takes one second to complete, then 100 will take 2 seconds

### O(nlog n)


### Sorting

Bubble Sort

- larger elements will bubble towards the end and smaller elements will bubble towards to beginning
- compares the current element against the next one

Insertion Sort

- just like bubble sort but looks compares the previous element against the current

Selection Sort

- Look for the minimum element, add it to the front of a (separate) array


### Concurrency

- Ruby threads run concurrently on a single core, rather than being scheduled across multiple cores in true parallel fashion
- Adding threads to Ruby doesn't necessarily result in faster execution times

Atomicity - (prevent race conditions) atomically modify the states if other threads cannot see intermediate states of the object
Visibility - can this thread see things from another thread
Ordering

_Global interpreter lock_ - lock around the execution of ruby code, before a thread can execute any code it first needs to acquire this
lock. prevents two Ruby threads from being executed at the same time.

Atomicity

```rb
counters = [0,0,0,0,0,0,0,0,0,0]

5.times.map do
  Thread.new do
    100_000.times do
      counters.map! { |counter| counter + 1 } # this is note atomic
    end
  end
end
threads.each(&:join)
puts counter.to_s
# => [500000, 447205, 500000, 500000, 500000, 500000, 203656, 500000, 500000, 500000]
```

`Mutex#synchronize` - prevent a thread from being interuppted by others

```rb
mutex = Thread::Mutex.new
counters = [0,0,0,0,0,0,0,0,0,0]

5.times.map do
  Thread.new do
    100_000.times do
      mutex.synchronize do # this is atomic
        counters.map! { |counter| counter + 1 }
      end
    end
  end
end
threads.each(&:join)
puts counter.to_s
```

Node

```rb
class Node
  attr_accessor :data, :left, :right, :name

  def initialize(options = {})
    @data = options[:data]
    @name = options[:name]
  end

  def children
    [left, right].compact
  end
end

class LinkedList
  attr_acc
end

def dfs
end

def bfs(node)
  queue = [node]
  while queue.size != 0
    current_node = queue.shift
    puts current_node.value
    current_children = current_node.children
    current_children.each { |child| queue.push(child) }
  end
end

def dfs(node)
  puts node.value
  node.children.each { |child| dfs(child) }
end
```
