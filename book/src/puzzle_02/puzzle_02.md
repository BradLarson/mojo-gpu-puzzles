# Puzzle 2: Zip

## Overview

Implement a kernel that adds together each position of vector `a` and vector `b` and stores it in `out`.

**Note:** _You have 1 thread per position._

![Zip](./media/videos/720p30/puzzle_02_viz.gif)

## Key concepts

In this puzzle, you'll learn about:
- Processing multiple input arrays in parallel
- Element-wise operations with multiple inputs
- Thread-to-data mapping across arrays
- Memory access patterns with multiple arrays

For each thread \\(i\\): \\[\Large out[i] = a[i] + b[i]\\]

### Memory access pattern

```txt
Thread 0:  a[0] + b[0] → out[0]
Thread 1:  a[1] + b[1] → out[1]
Thread 2:  a[2] + b[2] → out[2]
...
```

💡 **Note**: Notice how we're now managing three arrays (`a`, `b`, `out`) in our kernel. As we progress to more complex operations, managing multiple array accesses will become increasingly challenging.

## Code to complete

```mojo
{{#include ../../../problems/p02/p02.mojo:add}}
```
<a href="{{#include ../_includes/repo_url.md}}/blob/main/problems/p02/p02.mojo" class="filename">View full file: problems/p02/p02.mojo</a>

<details>
<summary><strong>Tips</strong></summary>

<div class="solution-tips">

1. Store `thread_idx.x` in `local_i`
2. Add `a[local_i]` and `b[local_i]`
3. Store result in `out[local_i]`
</div>
</details>

## Running the code

To test your solution, run the following command in your terminal:

```bash
magic run p02
```

Your output will look like this if the puzzle isn't solved yet:
```txt
out: HostBuffer([0.0, 0.0, 0.0, 0.0])
expected: HostBuffer([0.0, 2.0, 4.0, 6.0])
```

## Solution

<details class="solution-details">
<summary></summary>

```mojo
{{#include ../../../solutions/p02/p02.mojo:add_solution}}
```

<div class="solution-explanation">

This solution:
- Gets thread index with `local_i = thread_idx.x`
- Adds values from both arrays: `out[local_i] = a[local_i] + b[local_i]`
</div>
</details>

### Looking ahead

While this direct indexing works for simple element-wise operations, consider:
- What if arrays have different layouts?
- What if we need to broadcast one array to another?
- How to ensure coalesced access across multiple arrays?

These questions will be addressed when we [introduce LayoutTensor in Puzzle 4](../puzzle_04/).
