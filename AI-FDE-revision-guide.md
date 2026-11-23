# AI FDE Revision Guide

Live recordings 4–14 · October 11–November 22, 2026

Each chapter ends with a short exercise you can do from memory. The dates follow the academy's lesson and attachment dates. The guide is based on the downloaded notebooks and code. The academy transcript links were listed, but Cloud Browser blocked access during this pass, so the guide does not claim transcript coverage.

## Contents

| Chapter | Session date | Revision topic |
| --- | --- | --- |
| [1](#chapter-1--python-variables-types-and-collections) | Oct 11 | Python variables, types, and collections |
| [2](#chapter-2--sets-dictionaries-strings-and-io) | Oct 17 | Sets, dictionaries, strings, and I/O |
| [3](#chapter-3--control-flow-functions-and-scope) | Oct 18 | Control flow, functions, and scope |
| [4](#chapter-4--http-requests-and-generators) | Oct 24 | HTTP requests and generators |
| [5](#chapter-5--exceptions-and-files) | Oct 25 | Exceptions and files |
| [6](#chapter-6--object-oriented-python) | Oct 31 | Object-oriented Python |
| [7](#chapter-7--threads-processes-and-executors) | Nov 1 | Threads, processes, and executors |
| [8](#chapter-8--asyncio-fundamentals) | Nov 14 | Asyncio fundamentals |
| [9](#chapter-9--blocking-work-in-async-applications) | Nov 15 | Blocking work in async applications |
| [10](#chapter-10--linux-processes-and-fastapi) | Nov 21 | Linux processes and FastAPI |
| [11](#chapter-11--fastapi-validation-and-dependencies) | Nov 22 | FastAPI validation and dependencies |

## Chapter 1 — Python variables, types, and collections

**October 11 · Recording 4 · Python Recap 1**

- Assignment binds a name to an object. Reassigning an integer creates a new binding, while calling `append()` changes the existing list. If two variables reference that list, both observe the change.
- Use `type()` to inspect values. `True` is a Boolean, `"True"` is a string, and `None` represents the absence of a value. Use `is None` for a None check and `==` for ordinary value comparison.
- Review arithmetic, comparison, and membership operations. Choose a list for a mutable sequence and a tuple for a fixed sequence. A tuple can still hold mutable objects.

**Recall drill:** Predict the contents of both names after `a = [1]`, `b = a`, and `b.append(2)`. Repeat after replacing `b = a` with `b = a.copy()`.

[Source notebook and handout](https://github.com/tejamallidi/AI-FDE/blob/main/2026-10-11/resources.md)

## Chapter 2 — Sets, dictionaries, strings, and I/O

**October 17 · Recording 5 · Python Recap 2**

- Sets hold distinct hashable values. Use `set()` for an empty set. `remove()` raises `KeyError` for a missing value, while `discard()` leaves the set unchanged. Use `|`, `&`, and `-` for union, intersection, and difference.
- Dictionaries map unique hashable keys to values. Use `d[key]` when the key is required, `d.get(key, default)` for an optional key, and `d.items()` to iterate over key–value pairs.
- Strings are immutable. Operations such as `strip()` and `lower()` return new strings. `input()` returns a string, so convert numeric input explicitly. Review `print()` formatting in the separate demo.

**Recall drill:** Normalize two lists of service names, find the names that appear in both lists, and store a status per service in a dictionary.

[Source notebook and I/O examples](https://github.com/tejamallidi/AI-FDE/blob/main/2026-10-17/resources.md)

## Chapter 3 — Control flow, functions, and scope

**October 18 · Recording 6 · Python Recap 3**

- `if`/`elif` selects the first matching branch. Test truthiness when empty values and zero can be treated the same way. Use explicit comparisons when zero and missing data have different meanings.
- `range(start, stop)` excludes `stop`. `continue` skips the rest of the current iteration, `break` exits the loop, and `pass` is a no-op. Use `enumerate()` when you need an index and a value.
- Keep calculations in functions and pass inputs as parameters. A local assignment stays in the function's scope. `return` passes a value to the caller, while `print()` writes output.

**Recall drill:** Write a function that receives order quantities and prices, skips invalid entries, and returns a total. Decide which cases should be skipped and which should raise an error.

[Source notebook and function demos](https://github.com/tejamallidi/AI-FDE/blob/main/2026-10-18/resources.md)

## Chapter 4 — HTTP requests and generators

**October 24 · Recording 7 · Python FDE 1**

- The networking notebook calls a test endpoint and a product endpoint with `requests.get()`. Query parameters such as `limit` and `skip` go in `params`. Status and parsed JSON answer different questions. In your own client, set a timeout and check the HTTP status before relying on the payload.
- A generator yields one value at a time. `next()` advances it, and exhaustion ends iteration. Converting the generator to a list materializes all remaining values.
- The notebook contrasts assembling PDF page text up front with yielding page text as it is needed. The streaming version reduces retained data when the consumer also processes one page at a time.

**Recall drill:** Sketch an iterator that requests one page of products at a time and yields each product. Explain where to stop, where to handle a failed request, and what would cause memory to grow.

[Source networking notebook and assignment](https://github.com/tejamallidi/AI-FDE/blob/main/2026-10-24/resources.md)

## Chapter 5 — Exceptions and files

**October 25 · Recording 8 · Advanced Python**

- Catch errors you know how to handle, such as `ZeroDivisionError` or `FileNotFoundError`. A broad handler can hide unrelated mistakes. The notebook introduces a custom provider error, and the inspection example defines a domain-specific exception.
- `else` runs when the `try` block finishes without an exception. `finally` runs during normal exit and exception unwinding. Use `with open(...)` to manage file closure.
- `r` reads an existing file. `w` opens for writing and truncates it. `a` appends. A plus mode enables both reading and writing. Use `tell()` and `seek()` when the current file position matters.

**Recall drill:** Design a file-backed inspection score calculator. Handle a missing file, malformed score, and zero inspections distinctly. Decide which errors the caller should see.

[Source exception and file-handling examples](https://github.com/tejamallidi/AI-FDE/blob/main/2026-10-25/resources.md)

## Chapter 6 — Object-oriented Python

**October 31 · Recording 9 · Academy label “Linux-1”**

- The attached notebook focuses on classes and objects. `__init__` initializes instance state and `self` refers to the instance. Compare the procedural game with the version where a `Character` owns its health and damage behavior.
- Inheritance lets a subtype reuse or customize base behavior. The notebook's `Dog` example uses `super().__init__()` to initialize the base `Animal` state.
- An abstract base class declares a contract for implementations. The notification example uses `ABC` and `@abstractmethod`. Callers can depend on the notification interface while the concrete class handles delivery.

**Recall drill:** Design email and console implementations of a notification interface. Explain how a caller can switch implementations without changing its send logic.

[Source OOP notebook and game examples](https://github.com/tejamallidi/AI-FDE/blob/main/2026-10-31/resources.md)

## Chapter 7 — Threads, processes, and executors

**November 1 · Recording 10 · Academy label “API-1”**

| Workload | Starting point | What to check |
| --- | --- | --- |
| Blocking I/O such as service checks | `ThreadPoolExecutor` | Worker count and shared-state safety |
| CPU-heavy pure Python such as prime counting | `ProcessPoolExecutor` | Serialization and startup overhead |
| Direct worker control | `Thread` or `Process` | Startup, completion, and result transport |

- The threading examples progress from sequential work to concurrent checks and shared counters. `join()` waits for a worker. A lock protects a critical section when threads update shared state.
- The multiprocessing examples use queues to send results across process boundaries. Compare the sequential prime counter with the process-based versions. Include setup and result collection when measuring elapsed time.
- Executors manage a pool. `submit()` returns a future, and `result()` retrieves its value or raises its exception. The archive also includes Multipass setup handouts.

**Recall drill:** Choose a concurrency model for 50 blocking service checks and for four CPU-intensive calculations. Explain how you'd collect failures from individual workers.

[Source worker, pool, and Multipass examples](https://github.com/tejamallidi/AI-FDE/blob/main/2026-11-01/resources.md)

## Chapter 8 — Asyncio fundamentals

**November 14 · Recording 11 · Advanced Python**

- Calling an `async def` function produces a coroutine. `await` runs or waits for it in the event loop, and `asyncio.run(main())` is a script entry point. Consecutive awaits can serialize independent work.
- Use tasks to schedule independent coroutines and `gather()` when you need their results together. The thread-pool example uses `as_completed()` to process futures as they finish. That's useful when a slow task shouldn't delay handling an early result.
- The `httpx` example uses an async client for URL checks. Await async I/O and use `asyncio.sleep()` to yield during a simulated wait. A blocking call such as `time.sleep()` stalls the event loop thread.

**Recall drill:** Start three simulated checks with delays of one, two, and three seconds. Predict runtime and result handling for sequential awaits and concurrent tasks.

[Source asyncio and futures examples](https://github.com/tejamallidi/AI-FDE/blob/main/2026-11-14/resources.md)

## Chapter 9 — Blocking work in async applications

**November 15 · Recording 12 · Advanced Python**

- A synchronous call inside an async function can still block the event loop. The customer lookup example illustrates the problem. The legacy database examples offload blocking work to a thread pool.
- Use `run_in_executor()` to keep a legacy blocking function off the event loop thread. Use a thread pool for waiting on I/O and consider a process pool for CPU-intensive pure Python, as in the prime-counting example.
- Await the results where they are needed. Set a worker limit and measure throughput under concurrent calls. Reuse pools for repeated work and manage their shutdown explicitly.

**Recall drill:** An async API calls an old synchronous database client and then performs a large pure-Python transformation. Pick where each step should run and explain what happens when both execute inline.

[Source executor demos and lab setup](https://github.com/tejamallidi/AI-FDE/blob/main/2026-11-15/resources.md)

## Chapter 10 — Linux processes and FastAPI

**November 21 · Recording 13 · API-1**

- The Linux lab includes shell conditionals, file checks, background jobs, and Python signal handlers. Practice telling a running program to shut down gracefully and checking its logs or exit status.
- The first FastAPI script defines simple GET routes for a health check and a hello response. A route decorator maps an HTTP method and path to a Python function.
- The second script demonstrates a work-order route with a path parameter, query inputs, validation metadata, and `HTTPException`. Put resource identity in the path and optional request controls in the query. Distinguish invalid input from a valid ID that doesn't exist.

**Recall drill:** Build a small work-order API with a health route and one lookup route. Test a successful lookup, an invalid parameter, and an unknown ID. Explain the response for each and how you'd stop the service gracefully.

[Source FastAPI and Linux examples](https://github.com/tejamallidi/AI-FDE/blob/main/2026-11-21/resources.md)

## Chapter 11 — FastAPI validation and dependencies

**November 22 · Recording 14 · FastAPI-2**

- Compare integer path parameters with bounded `Path` and `Query` values. Invalid inputs are rejected during validation. A valid ID missing from the store yields 404.
- Use a Pydantic request model to validate work-order creation. A PATCH model can use `model_dump(exclude_unset=True)` to preserve omitted fields. Decide explicitly whether a supplied null should clear a field.
- Declare a public response model to control which fields the API returns. Use `Depends()` to share store access and pagination across endpoints. The header example demonstrates dependency-based checks in a lab.

**Recall drill:** Design a PATCH endpoint for a work order. Explain what happens when the status is omitted, invalid, or valid but the order does not exist.

Source coverage is based on the code in the resource archive. The transcript was listed in the academy and was not reviewed for this chapter.

[Source inventory](2026-11-22/resources.md)
