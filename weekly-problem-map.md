# Weekly LeetCode Problem Map

This curated practice path aligns to [`ROADMAP.md`](../ROADMAP.md) and draws on LeetCode's [Top Interview 150 study plan](https://leetcode.com/studyplan/top-interview-150/). It is a menu, not a quota: use enough time to derive, implement, test, and review each problem. If one problem takes the full session, that is useful practice. Optional extensions should not displace review.

**Suggested use:** Start with the first problem as a guided example, then remove support progressively. Hide the tier/pattern labels during independent practice. For a retry, use a blank editor and explain the invariant before coding.

**Tier key:** The numbered core progression is the week's **Must Know** practice set. An **Optional extension** is **Should Know** practice unless explicitly called an advanced challenge/mock. Advanced problems are stretch material; attempting them is not a condition for moving on. The tier refers to curriculum priority, not LeetCode's difficulty rating.

## Weeks 1–2 — Foundations and linear patterns

### Week 1 — Interview problem-solving and Java toolkit

**Core progression**

1. [Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array/) — trace state and bounds.
2. [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) — compare direct search with a set.
3. [Valid Anagram](https://leetcode.com/problems/valid-anagram/) — frequency counting and character assumptions.
4. [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) — maintain a running invariant.
5. [Two Sum](https://leetcode.com/problems/two-sum/) — derive a lookup strategy and discuss its time/space tradeoff.

**Optional extension:** [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) — prefix/suffix reasoning without division.

### Week 2 — Hashing, two pointers, windows, prefix sums

**Core progression**

1. [Two Sum II – Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) — sorted two-pointer invariant.
2. [Move Zeroes](https://leetcode.com/problems/move-zeroes/) — same-direction read/write pointers.
3. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) — variable window and last-seen state.
4. [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/) — window validity and positive-input assumption.
5. [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) — prefix-frequency map; distinguish from a sliding window.

**Optional extension:** [3Sum](https://leetcode.com/problems/3sum/) — sorting, duplicate handling, and two pointers.

## Weeks 3–4 — Ordering, search, and linked structures

### Week 3 — Sorting, binary search, intervals

**Core progression**

1. [Binary Search](https://leetcode.com/problems/binary-search/) — state the interval convention.
2. [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) — boundary searches.
3. [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) — identify the sorted half.
4. [Merge Intervals](https://leetcode.com/problems/merge-intervals/) — sort order and overlap condition.
5. [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) — binary search over an answer space.

**Optional extension:** [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) — interval scheduling and greedy proof.

### Week 4 — Linked lists, stacks, queues, monotonic structures

**Core progression**

1. [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) — stack state.
2. [Min Stack](https://leetcode.com/problems/min-stack/) — design operations and auxiliary state.
3. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) — fast/slow pointers.
4. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) — pointer invariants and iterative/recursive forms.
5. [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) — monotonic stack and what each index means.

**Optional extension:** [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/) — monotonic stack boundaries.

## Weeks 5–6 — Trees and heaps

### Week 5 — Binary trees and BSTs

**Core progression**

1. [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) — recursive return value and base case.
2. [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) — BFS queue and level boundaries.
3. [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) — propagate valid bounds.
4. [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) — separate returned height from global answer.
5. [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) — reason from recursive results.

**Optional extension:** [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) — define an unambiguous format.

### Week 6 — Heaps, priority queues, tree review

**Core progression**

1. [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) — heap versus selection tradeoff.
2. [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) — frequency map plus bounded heap or buckets.
3. [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) — ordered traversal.
4. [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) — priority queue and comparator design.

**Optional extension:** [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) — two heaps and balance invariant.

## Weeks 7–8 — Graphs and backtracking

### Week 7 — Graph modeling and traversal

**Core progression**

1. [Flood Fill](https://leetcode.com/problems/flood-fill/) — grid as graph; visited-state timing.
2. [Number of Islands](https://leetcode.com/problems/number-of-islands/) — components and visited state.
3. [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/) — multi-source BFS by levels.
4. [Course Schedule](https://leetcode.com/problems/course-schedule/) — cycle detection/topological order.
5. [Clone Graph](https://leetcode.com/problems/clone-graph/) — visited map from original node to copy.

**Optional extension:** [Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/) — BFS/DFS coloring.

### Week 8 — Shortest paths, union-find, backtracking

**Core progression**

1. [Number of Provinces](https://leetcode.com/problems/number-of-provinces/) — compare traversal and DSU models.
2. [Redundant Connection](https://leetcode.com/problems/redundant-connection/) — DSU union/find invariant.
3. [Combination Sum](https://leetcode.com/problems/combination-sum/) — recursive choices and state restoration.
4. [Permutations](https://leetcode.com/problems/permutations/) — used-state backtracking.
5. [Network Delay Time](https://leetcode.com/problems/network-delay-time/) — Dijkstra with a min-priority queue.

**Optional extension:** [N-Queens](https://leetcode.com/problems/n-queens/) — constraint tracking and pruning; or [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/) — bounded-edge shortest path.

## Weeks 9–11 — Greedy and dynamic programming

### Week 9 — Greedy reasoning

**Core progression**

1. [Assign Cookies](https://leetcode.com/problems/assign-cookies/) — sort and match resources.
2. [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) — explain the earliest-finish choice.
3. [Jump Game](https://leetcode.com/problems/jump-game/) — maintain farthest reachable position.
4. [Gas Station](https://leetcode.com/problems/gas-station/) — derive why a failed prefix can be discarded.
5. [Jump Game II](https://leetcode.com/problems/jump-game-ii/) — greedy frontier layers.

**Optional extension:** [Candy](https://leetcode.com/problems/candy/) — two directional constraints.

### Week 10 — Dynamic programming foundations

**Core progression**

1. [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) — define state and recurrence.
2. [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/) — base cases and top-of-stairs interpretation.
3. [House Robber](https://leetcode.com/problems/house-robber/) — take/skip state.
4. [Unique Paths](https://leetcode.com/problems/unique-paths/) — grid DP and evaluation order.
5. [Coin Change](https://leetcode.com/problems/coin-change/) — unbounded choice and unreachable states.

**Optional extension:** [Decode Ways](https://leetcode.com/problems/decode-ways/) — local validity and careful base cases.

### Week 11 — DP patterns and reconstruction

**Core progression**

1. [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) — quadratic DP first; derive the faster form as an extension.
2. [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) — 0/1 knapsack and reverse iteration.
3. [Word Break](https://leetcode.com/problems/word-break/) — prefix segmentation state.
4. [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) — two-sequence state.
5. [Edit Distance](https://leetcode.com/problems/edit-distance/) — transitions and operation interpretation.

**Optional extension:** [Burst Balloons](https://leetcode.com/problems/burst-balloons/) — interval DP; or [Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/) — state-machine DP.

## Weeks 12–13 — Advanced structures and consolidation

### Week 12 — Tries, range queries, advanced graph/tree topics

**Core progression**

1. [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/) — node representation and prefix queries.
2. [Range Sum Query – Mutable](https://leetcode.com/problems/range-sum-query-mutable/) — implement with a Fenwick or segment tree and compare.
**Should Know practice**

1. [Accounts Merge](https://leetcode.com/problems/accounts-merge/) — DSU or graph components.

**Advanced challenges**

- [Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network/) — bridge-finding.
- [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/) — Fenwick/segment tree or merge-sort counting.

### Week 13 — Pattern integration and weak-area repair

Do these as a **closed-book, unlabeled diagnostic**. Choose one per session; write the first approach and cues before coding. Revisit earlier problems that exposed a weak pattern.

1. [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
2. [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
3. [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
4. [Word Ladder](https://leetcode.com/problems/word-ladder/)
5. [Target Sum](https://leetcode.com/problems/target-sum/)

**Optional extension:** [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) — compare two pointers, prefix maxima, and stack reasoning.

## Weeks 14–16 — Interview performance

### Week 14 — Mixed medium practice and explanation

Use as interview-style rounds. Do not read the pattern tags until after the attempt.

1. [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
2. [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
3. [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)
4. [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
5. [Coin Change](https://leetcode.com/problems/coin-change/) — spaced DP retrieval, not a first exposure.

### Week 15 — Timed mocks and adaptation

Pick two problems for a mock pair; reserve time for a verbal postmortem and a redo of the weaker one.

1. [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
2. [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)
3. [Subsets](https://leetcode.com/problems/subsets/)
4. [Path Sum II](https://leetcode.com/problems/path-sum-ii/)
5. [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) — explain both standard formulations if ready.

### Week 16 — Final review and durable reference

Use a fresh, unlabeled selection, prioritizing previous misses. Treat these as mock prompts rather than a set to finish in one sitting.

1. [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
2. [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
3. [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
4. [Word Break](https://leetcode.com/problems/word-break/)
5. [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) — optional advanced mock after core review.

## Recording attempts

For each attempt, note date; problem; independent or assisted; minutes to a viable approach; hint level; correctness; complexity; Java issue; missed edge case; one lesson; and next review date. When repeating a problem, change a constraint or explain a second approach to check whether the pattern generalized.
