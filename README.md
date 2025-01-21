### The Lip Language

Lip is a data-flow-centric, declarative programming language designed to
    process and transform data in a concise and elegant way.
The core concept is to treat data as a stream that flows through a pipeline
    and is processed through a series of operators.

1. **core concepts:**

* **Stream:** All data in the Lip exists in the form of a stream.
    Streams can be finite (e.g., lists, dict) or infinite (e.g., generators, sensor data).

* **Pipeline:** A pipeline is a sequence of operators connected through which
    data flows and is sequentially processed.

* **Operator:** The operator transforms or processes data streams,
    such as `map`, `filter`, `reduce`, etc.

* **Site:** site is the source or end of the data flow, such as
    `range`, `file`, `print`, `database`, etc.

* **Controller:** Controller is used to control the direction of data flow,
    such as `branch`, `merge`, `loop`, etc.


2. **Data type:**

Lip supports common data types, including:

* **Value type:** integer, floating point number
* **Boolean type:** True, False
* **string type:** "string"  'string2' '''multi-line strings'''
* **List Type:** [1, 2, 3]
* **Dictionary types:** {key1: value1, key2: value2}
* **None value:** None (any type has a None value)


3. **Operator:**

Lip provides a rich set of built-in operators that cover common data processing needs:

* **take(n):** Gets the first n elements of the data stream.
* **drop(n):** Drops the first n elements of the data stream.
* **sort(key=None, reverse=False):** Sorts the data stream.
* **filter(predicate):** Filters out elements that do not satisfy the predicate `predicate`.
* **map(func):** Applies the function `func` to each element in the data stream.
* **reduce(func, initial):** Performs a cumulative calculation of the data stream using
    the function `func`, where `initial` is the initial value.
* **flatten():** Flattens the nested list into a flat list.
* **distinct():** Removes duplicate elements in the data stream.
* **zip(stream1, stream2):** Merges two data streams into a new data stream with the elements as tuples.
* **concat(stream1, stream2):** Joins two data streams into a new data stream.


4. **Controller:**

* **branch {label1: pipeline1, label2: pipeline2, ...}:** Copies and distributes the data stream to different branches.
* **merge(label1, label2, ...):** Merges data streams from different branches into a single data stream.
* **loop(condition, pipeline):** loops through the pipeline until the condition is not satisfied.


5. **Site:**

* **range(start, stop, step):** Generates a sequence of values.
* **file(path, mode):** Reads or writes files.
* **print(value):** Outputs the value to the console.
* **database(connection, query):** Executes database queries.
* **http(url, method, data):** Create an HTTP connection.


6. **Function definition:**

```Lip
func function_name(param1, param2, ...)  => pipeline
```

The function can take multiple arguments and return a pipe.


7. **Variable:**

Use `->` to assign the result of the data flow to the variable:

```Lip
pipeline -> variable
```

8. **Module:**

Lip supports modular programming, and other modules can be imported using the `import` keyword:

```Lip
import "module_name/sub_module"
```


9. **Example:**

```Lip
// Calculate the sum of squares from 1 to 10
range(1, 11) >> map(x => x * x) >> reduce(sum(), 0) -> result
print(result)

// Read the contents of the file and count the number of word occurrences
file("input.txt", "r") >> lines() >> flatMap(words) >> groupBy(identity) >> map({key: key, value: len(value)}) -> wordCounts
print(wordCounts)


// Parallel processing of data
range(100) >> branch {
    even: filter(x => x % 2 == 0) >> process_even(),
    odd: filter(x => x % 2 ! = 0) >> process_odd()
} >> merge(even, odd) -> result
print(result)
```

10. **Future direction:**

* **Type system:** Introduces static type checking to improve code reliability.
* **Error handling:** Provides a more complete error handling mechanism.
* **Concurrent:** Supports concurrent execution pipelines to improve performance.
* **Library:** Develop a rich standard library to facilitate users to carry out various data processing tasks.

---

The design goal of the Lip language is to provide a concise, elegant, and efficient way of processing data.
It makes it easy to build complex data processing processes through
a combination of pipes, operators, sites, and controllers. In the future, Lip will continue to evolve and
improve to become a more powerful and easy-to-use data processing language.
