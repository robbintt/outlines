
### Vector Packing: An NP-Hard Problem Made Easy

**Speaker:** Conor Frailey, https://github.com/conorfrailey
**Turnout:** 12 people = 10 students, 1 speaker, and 1 of me.

The Knapsack Problem - playing tetris for a living, sort of.

[Jupyter Notebook Presentation Online](https://github.com/conorfrailey/Presentations)


#### Technical Details of Problem:

See instructor notes, the definitions are very detailed.

1. Knapsacks are each identical in the context of the problem (volume, weight reqs.)
2. Items have a volume and a weight
    - Weight can be described for items as a percentage a knapsack.
    - In this description, all knapsacks can contain (1,1) which means (100%, 100%)
3. You want to use as few knapsacks as possible
4. You group items by partition to find the solution
    - cannot just brute force it, factorial combinations means takes TOO long
    - e.g. 40 boxes means 40! tries which is not possible to brute force

#### Notes

- partition (math) - distinct groups of your set
- bin packing is different - uses three linear dimensions
- What is NP-Hard
    1. Is P == NP? 
    2. P means problems solvable in polynomial time
    3. If you can solve this in polynomial time you can solve almost anything in polynomial time
- If you can form a problem into a `convex optimization problem`, you are super happy
    - space has to be convex
    - it keeps on curving up, you want to find the minimum
    - gradient descent is used in high dimensions to find the minimum
    - pick a point and go towards zero
- if you have `mixed integer program` you can do a noncontiguous set of point
    - you can't have a continuous number of cases of beef
        - thus you can't use gradient descent on cases of beef
    - list of MIP solvers in the notes
    - MIP programs are super expensive so we can't use it today
    - we can use online tool: `Arc-flow VPSolver`
- `VPSolver` has a docker image available on docker hub
- Hypergraph - a collection of distinct objects and a connection between two or more
    - example: customer orders a subset of the products, a "group". Another customer orders a second subset, different group. They might overlap some products, or even be identical but different customer.
    - solving with a hypergraph. use the first item as a reference, then start optimizing and reducing symmetry. Hit hotspots where employee has to go to more than one (too many) aisles.



#### Other Examples
    1. Vacationing on a short vacation, want to do as many things as possible
        - Each day has finite time
        - You can only walk so much a day
        - You can only spend so much money per day (per diem)
    2. Data centers and their virtual machines
    3. Refrigerated warehouses
        - Fixed height rack, movable height shelves inside racks
        - All pallets are standard, except height
        - Get the pallets onto the shelves


#### References


