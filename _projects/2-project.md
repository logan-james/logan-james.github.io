---
layout: page
title: Routing Program
description: Package delivery system.
img: assets/img/routing.jpeg
importance:
category: work
#related_publications: true
---

## Overview

In this write-up, I will explain the development and implementation of a package delivery system. This system utilizes data structures like hash tables and algorithms such as the Nearest Neighbor to optimize package delivery routes while adhering to time and mileage constraints.

## Hash Table Implementation

The core of the system is a custom-built **hash table** designed for fast data access and retrieval. The hash table uses **chaining** to handle collisions, ensuring that package data can be efficiently inserted, updated, and removed. Below is a brief description of the important functions in this implementation:

- **Insert method**: Inserts package data into the hash table.
- **Lookup method**: Retrieves a package based on its unique package ID.
- **Chaining mechanism**: Handles collisions to maintain data integrity.

This hash table ensures that all package data, such as delivery address, deadlines, status, and more, are stored and accessed efficiently.

## Package Lookup Functionality

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/lookup.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

In the package delivery system, the **lookup functionality** allows real-time retrieval of package data using the package ID. This is implemented through a combination of:

1. **HashTable’s lookup method**: Fetches the `Package` object using its unique ID.
2. **Package object attributes**: Provide access to key delivery data, including:
   - Delivery address
   - Delivery deadline
   - Delivery status

## Nearest Neighbor Algorithm for Route Optimization

The **Nearest Neighbor algorithm** plays a crucial role in optimizing delivery routes by selecting the nearest package for delivery based on the current location of the truck. This algorithm updates the truck's position and delivery times after each package is delivered, and repeats the process until all packages are delivered.

- **Strengths**: The Nearest Neighbor algorithm is computationally efficient and provides a balance between performance and practicality, making it ideal for scenarios where fast decisions are necessary.
- **Weaknesses**: Although not always the most optimal, it delivers near-optimal routes, which is satisfactory in real-world situations with time constraints.

## Alternate Algorithms

Two other algorithms that could have been considered for the WGUPS system are:

1. **Genetic Algorithm**: A more complex solution that evolves potential routes over time for optimization.
2. **Simulated Annealing**: Allows for greater flexibility by sometimes accepting worse solutions to avoid getting stuck in local optima.

While these alternatives offer better optimization, they come with the cost of higher computational complexity.

## Hash Table vs. Other Data Structures

The chosen **hash table** data structure provides O(1) average time complexity for lookups and updates, making it ideal for real-time systems like the WGUPS.

- **Binary Search Trees (BST)**: Offer O(log n) time complexity but can become unbalanced, reducing efficiency.
- **Array-based lists**: Provide fast sequential access but are inefficient for searching, with O(n) time complexity for lookups.

The hash table outperforms both in terms of speed and efficiency, making it the best fit for this scenario.

## Future Improvements

If I were to revisit this project, I would consider incorporating **hybrid algorithms** that combine the simplicity of Nearest Neighbor with the flexibility of Simulated Annealing. Real-time traffic data could also enhance the system's adaptability, improving delivery efficiency.

## Conclusion

The **WGUPS Routing Program** successfully implements a package delivery system using a custom hash table and the Nearest Neighbor algorithm. This system meets all necessary requirements, balancing efficiency, and practicality to optimize package deliveries.

---

### References

1. Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2009). _Introduction to Algorithms_ (3rd ed.). MIT Press.
2. Skiena, S. S. (2020). _The Algorithm Design Manual_ (3rd ed.). Springer.
3. Sedgewick, R., & Wayne, K. (2011). _Algorithms_ (4th ed.). Addison-Wesley Professional.
