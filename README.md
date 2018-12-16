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
