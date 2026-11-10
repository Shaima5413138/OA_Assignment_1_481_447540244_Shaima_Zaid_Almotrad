# My Answers - Assignment 1 (CFLP: VNS vs Gurobi)

**Student Information:**
- **Student ID:** 447540244
- **Student Name:** Shaima Zaid Almotrad
- **Gurobi Version Used:** [x] Academic [ ] Free
- **Date Completed:** 2026-11-10

---

## Section A: Solution Quality Analysis (4 marks)

### A.1 (2 marks) - Gap Analysis by Categories

**Analysis of Plot 01:**

The Large group has the highest median gap at **14.91%**. The Medium group has a median of **14.22%**, and the Small group has **12.22%**. The gap also depends on difficulty. Moderate problems have the highest median gap (**15.10%**), while Easy problems have the lowest (**10.48%**). This means VNS usually gives better results on Easy problems.

**Specific Observations:**
- **Highest median gap size:** Large.
- **Median gap value:** 14.91%.
- **Effect of difficulty on gap:** Moderate problems are generally harder for VNS than Easy problems. For example, the Large–Moderate group has a median gap of about **17.69%**.

**Outliers identified:**

Instance **119** (Large–Moderate) has the highest gap, about **26.84%**. Instance **027** (Small–Moderate) also has a high gap of **25.40%**. These cases may be difficult because the capacity limits make it harder to find a good combination of open facilities and client assignments.

**Interpretation:**

VNS searches for improvements around its current solution, but it does not always find the best solution. Some problems need several facility and client changes together. This is why the gap can be high even when VNS finishes quickly.

---

### A.2 (2 marks) - Overall Solution Quality Statistics

**From Excel File (Sheet "All Results"):**

- **Total instances analyzed:** 144
- **Instances with gap < 5%:** 0 (**0%**)
- **Instances with gap < 10%:** 31 (**21.5%**)
- **Mean gap across all instances:** **14.19%**
- **Standard deviation of gap:** **4.70 percentage points**

**Interpretation:**

On average, VNS solutions cost **14.19% more** than Gurobi's optimal solutions. No instance has a gap below 5%, and only 31 out of 144 are below 10%. The standard deviation also shows that the gap changes between problems. So, VNS is fast, but its solution quality is not consistently close to the optimum.

---

## Section B: Computational Efficiency Analysis (4 marks)

### B.1 (2 marks) - Time Comparison

**Analysis of Plot 02:**

**Size at which VNS becomes significantly faster:**

VNS is faster **on average for all three sizes**, especially in the Moderate and Expensive groups. The average times are:

| Problem size | VNS time | Gurobi time |
|---|---:|---:|
| Small | 0.23 s | 8.80 s |
| Medium | 0.29 s | 8.08 s |
| Large | 0.41 s | 2.50 s |

However, Gurobi is slightly faster on average for Easy problems (**0.17 s** compared with **0.22 s** for VNS).

**Most challenging configurations:**
- **For VNS:** Large–Moderate, with an average time of about **0.55 s**.
- **For Gurobi:** Medium–Expensive, with an average time of about **21.64 s**.

**Detailed Comparison:**

The overall average time is **0.31 s for VNS** and **6.46 s for Gurobi**. VNS saves about **6.15 seconds per problem** on average. But some Gurobi runs take much longer than others. For example, instance **096** takes about **285.45 s** with Gurobi. This makes Gurobi's average time higher.

---

### B.2 (2 marks) - Speedup Analysis

**Analysis of Plot 03:**

Speedup = Gurobi time / VNS time. A speedup above 1 means VNS is faster.

**Average speedup factors:**
- **Small:** **37.71×**
- **Medium:** **21.47×**
- **Large:** **6.86×**

**Instances where Gurobi is faster (speedup < 1):**

Yes. Gurobi is faster in **39 out of 144 instances (27.1%)**. Many of these are Easy problems. For example, in instance **002** (Small–Easy), Gurobi takes about **0.048 s**, while VNS takes **0.282 s**. The speedup is only **0.17×**.

**Practical Implications:**

VNS is helpful when we need answers quickly, especially for harder problems. Its overall average speedup is **22.01×**. But Gurobi can be faster for some Easy problems and also gives the optimal answer. The speedup does not increase with problem size in these results.

---

## Section C: Scalability Analysis (3 marks)

### C.1 (1.5 marks) - Scalability Behavior

**Analysis of Plot 04:**

**VNS Scalability:**

VNS time increases slowly from **0.23 s** for Small problems to **0.29 s** for Medium and **0.41 s** for Large. Its time stays fairly low in all three groups.

**Gurobi Scalability:**

Gurobi does not show a regular increase. Its average time is **8.80 s** for Small, **8.08 s** for Medium, and **2.50 s** for Large. Some smaller Expensive problems take a very long time, so size alone does not explain the results.

**Comparison:**

In this experiment, VNS has more stable running times. Gurobi's time changes a lot between instances. I would say VNS scales better across the tested problems, but larger experiments are needed before making a conclusion about very large problems.

---

### C.2 (1.5 marks) - Growth Rate and Predictions

**Observed Growth of Average Runtime:**

| Algorithm | Small → Medium | Medium → Large |
|---|---:|---:|
| VNS | 0.23 → 0.29 s (**1.26×**) | 0.29 → 0.41 s (**1.41×**) |
| Gurobi | 8.80 → 8.08 s (**0.92×**) | 8.08 → 2.50 s (**0.31×**) |

**Shape of growth in Plot 04:**
- **VNS:** [ ] Roughly steady [x] Steadily increasing [ ] Sharply increasing
- **Gurobi:** [x] Roughly steady / irregular [ ] Steadily increasing [ ] Sharply increasing

**Justification:**

VNS gets a little slower when problem size increases. Gurobi's average time goes down in this data, mainly because some Small and Medium problems are unusually difficult. So Gurobi's time pattern is irregular, not a normal steady increase.

**Rough Prediction for Extra Large Instance (n = 50, m = 20):**
- **Predicted VNS time:** About **0.58 s**.
- **Predicted Gurobi time:** About **0.77 s**.
- **Calculation:** I used the Medium-to-Large ratio again: VNS = 0.41 × (0.41 / 0.29) ≈ 0.58 s; Gurobi = 2.50 × (2.50 / 8.08) ≈ 0.77 s.

These are only rough estimates. The Gurobi prediction is especially uncertain because its times vary a lot.

**Suitability for Very Large Instances:**

VNS may be useful for very large problems because its times were more stable in this experiment. However, its average gap is still **14.19%**, so I would improve the algorithm and test it on larger cases first.

---

## Section D: Quality-Time Tradeoff Analysis (3 marks)

### D.1 (1.5 marks) - Sweet Spot Identification

**Analysis of Plot 05:**

**Sweet Spot:**

Instance **040** (Small–Expensive) is a good example. It has a **5.56% gap**, and VNS takes **0.401 s** compared with **22.435 s** for Gurobi. VNS is about **55.88× faster** on this instance. This is a good balance between speed and quality, although the gap is still above 5%.

**Time Savings for High-Quality Solutions (gap < 5%):**
- **Average VNS time:** Not applicable.
- **Average Gurobi time:** Not applicable.
- **Absolute savings:** Cannot be calculated.
- **Relative savings:** Cannot be calculated.

**Interpretation:**

There are **no instances with a gap below 5%**, so it would be incorrect to give a time-saving number for that group. If a company needs a gap below 5%, the current VNS results do not meet that requirement.

---

### D.2 (1.5 marks) - Practical Decision Making

**Scenarios Justifying a 10–15% Gap:**

1. When a company is comparing many warehouse locations and only needs a quick first answer.
2. When demand changes suddenly and the company must make a fast decision.
3. When computing resources are limited and getting a good feasible solution quickly matters more than finding the exact best one.

**Recommendation for a Real-World Logistics Company:**

I would use **VNS for quick planning** and **Gurobi for important final decisions**. VNS is fast, but its average gap of **14.19%** could mean higher costs. Gurobi is better when the company needs the lowest possible cost and has enough time to solve the problem.

---

## Section E: Algorithm Understanding (3 marks)

### E.1 (1.5 marks) - VNS Neighborhood Structures

**Role of Each Neighborhood:**

**N1 (Open Facility):**
- **Purpose:** Opens another facility and tries to reassign clients.
- **Contribution:** [ ] Intensification [x] Diversification
- **Explanation:** It explores a different set of open facilities. This can give clients more choices but also adds an opening cost.

**N2 (Close Facility):**
- **Purpose:** It is supposed to close a facility and reassign its clients.
- **Contribution (intended):** [x] Intensification [ ] Diversification
- **Explanation:** Closing an unnecessary facility can reduce fixed costs. However, the provided code actually closes one facility and opens another, so this neighborhood works more like a swap.

**N3 (Swap Facilities):**
- **Purpose:** Closes one open facility and opens a different one.
- **Contribution:** [ ] Intensification [x] Diversification
- **Explanation:** It checks different facility locations without necessarily changing how many facilities are open.

**N4 (Reassign Clients):**
- **Purpose:** Moves a client to another open facility if there is enough capacity.
- **Contribution:** [x] Intensification [ ] Diversification
- **Explanation:** It tries to lower assignment costs while keeping the same facilities open.

**How They Complement Each Other:**

N1 and N3 explore different facility choices. N4 improves assignments within those choices. N2 should help reduce the number of open facilities, but its current code does not do that properly. Together, the neighborhoods are meant to help VNS find better solutions.

---

### E.2 (1.5 marks) - Convergence Behavior Analysis

**Source:** I used the original `convergence_grid_small_easy.png` generated by the assignment notebook. The red line shows the best VNS cost, while the dashed blue line shows Gurobi's optimal cost.

**Plot 1: Instance 003 (`003_cflp_small_easy_fac16_cli56`)**

This plot is in row 1, column 3. The VNS cost stayed at about **14,731.26** without any improvement. The final gap was about **10.1%**. The flat red line shows that VNS did not find a better solution after the initial one.

**Plot 2: Instance 001 (`001_cflp_small_easy_fac17_cli66`)**

This plot is in row 1, column 1. The cost decreased once at **iteration 2**, from about **14,622.15** to **14,465.44**. After that, the line stayed flat. The final gap was about **16.2%**. VNS improved early but could not get closer to the optimal cost.

**Plot 3: Instance 012 (`012_cflp_small_easy_fac17_cli51`)**

This plot is in row 3, column 4. The red line decreased twice, at about **iterations 7 and 13**. The cost went from around **10,033.60** to **10,024.04**, then **10,023.28**. The final gap was about **14.2%**. The improvements were small, but VNS found a better solution more than once.

**What I noticed:**

Some instances stay flat, while others improve in one or two steps. The red line only goes down when VNS finds a lower cost. In all three cases, the final VNS cost is still above the blue Gurobi line.

**Role of shaking:**

Shaking makes a random change to the current solution. This helps VNS try a different area when local search is stuck. It can lead to new improvements, but it does not always work, as seen in Instance 003.

---

## Section F: Critical Reflection (3 marks)

### F.1 (1 mark) - Limitations and Improvements

**Main Limitations of Current VNS Implementation:**

1. N2 does not close a facility by itself. It also opens another facility, so it repeats part of N3's work.
2. The search checks a limited number of neighboring solutions and may miss better options.
3. VNS can stop after several iterations with no improvement, even when the gap is still high.

**Suggested Improvements:**

1. Fix N2 so it can close an unneeded facility and reduce fixed costs.
2. Try more client reassignment moves or allow swaps between clients.
3. Test different numbers of neighbors and stopping limits to see if longer searches improve the results.

---

### F.2 (1 mark) - Real-World Deployment Considerations

**Additional Constraints for a Real Logistics Company:**

1. **Delivery time windows:** Customers may need deliveries before a certain time.
2. **Vehicles and routes:** Delivery trucks have limited capacity, and the actual routes affect costs.
3. **Changing demand:** The company must plan for busy periods and unexpected increases in orders.

**Additional Objectives:**

The company should consider delivery speed, customer service, and reliability as well as cost. For example, opening another warehouse may cost more but help deliver orders faster. A useful model should balance these needs.

---

### F.3 (1 mark) - Exact Method vs Heuristic in Practice

**Gurobi Optimality Status (from the `gurobi_status` column):**
- **Instances solved to proven optimality:** **144 out of 144**.
- **Instances stopped at the time limit:** **0**.
- **Do time-limit instances share a size/difficulty?** Not applicable, because no case stopped at the time limit.

**What VNS Gives Up and What It Gains:**

VNS does not guarantee the best solution. Its average gap is **14.19%**, but it takes only **0.31 s** on average compared with **6.46 s** for Gurobi. VNS is faster in **105 out of 144** cases.

**Practical Value of Heuristics:**

VNS is useful when a fast, feasible answer is needed. Gurobi is better when the exact best solution is important. I would use VNS for quick decisions and Gurobi to check major decisions where extra costs matter.

---

## Section G: BONUS - VNS Improvement Challenge (+3 marks, optional)

### G.1 - Bug Identification

I found two problems in the VNS implementation. First, `n2_close_open_facility()` should close an open facility. But in the original code it closes one facility and opens another:

```python
neighbor_facility_opened[j_open] = 0
neighbor_facility_opened[j_close] = 1
```

This is a swap, just like N3. It means N2 cannot reduce the number of open facilities, so VNS may keep unnecessary fixed costs. Second, the client assignment function processes clients in their original order. For some instances, this leaves later clients without enough capacity. I checked the main acceptance condition too. In my original notebook, `if new_cost < best_cost` was already correct, so I left it unchanged.

### G.2 - The Fix

I changed N2 so it closes one facility without opening another one, and then checks if all clients can still be served. The main change is:

```python
neighbor_facility_opened = facility_opened.copy()
neighbor_facility_opened[j_open] = 0  # Close one facility only
# Reassign clients and keep the neighbor only when it is feasible.
```

I also changed `assign_clients_to_nearest_open_facility()`. If assigning clients in their original order fails, the function tries again with the largest client demands first:

```python
if failed and client_order is None:
    return assign_clients_to_nearest_open_facility(
        service_costs, facility_opened, facility_capacities, client_demands,
        client_order=np.argsort(-client_demands)
    )
```

I kept the same capacity check, VNS stopping settings, and Gurobi solutions. Both modifications are marked `BONUS FIX` in the improved notebook.

### G.3 - Demonstrated Improvement

For the bonus test, I ran both versions of VNS on the **same 144 generated instances** with student ID **447540244**. I used the same initial random state for the two runs and the same settings: 100 maximum iterations, 20 iterations without improvement, and 15 neighbors. I also checked the solutions against the capacity constraints. These are results from the controlled Python comparison; running the notebook again may give slightly different VNS results.

| Result | Original VNS | Improved VNS |
|---|---:|---:|
| Feasible solutions (out of 144) | 136 | 144 |
| Average solution cost on the 136 cases feasible in both runs | 23,501.55 | 22,832.63 |
| Cases with a lower cost (among these 136) | — | 123 |
| Cases with the same cost (among these 136) | — | 10 |
| Cases with a higher cost (among these 136) | — | 3 |

The mean relative cost reduction on the 136 comparable, feasible cases was **2.70%**. The other 8 cases were infeasible in the original run but became feasible with the improved assignment routine. Their old costs should not be treated as valid solutions.

Here are some gap comparisons using the Gurobi optimal costs from the original results:

| Instance | Original gap | Improved gap |
|---|---:|---:|
| 001 (Small–Easy) | 16.25% | 13.46% |
| 003 (Small–Easy) | 10.07% | 8.12% |
| 010 (Small–Easy) | 15.45% | 10.00% |
| 012 (Small–Easy) | 14.16% | 13.12% |
| 019 (Small–Moderate) | 21.35% | 10.69% |

The improved version had a lower cost in most of the cases we could compare, and all its assignments passed the capacity checks in this test. It does not reach a gap below 5% in all cases. The full controlled test is in `bonus_validation_student_447540244.csv`. The corrected code is in `447540244_Shaima_Zaid_Almotrad_Assignment1_IMPROVED.ipynb`. The notebook can also make new `_IMPROVED` results on my own computer.

---

## Additional Comments (Optional)

The results show that VNS is usually faster, while Gurobi gives better solution quality. The best choice depends on how much time and extra cost the company can accept.

---

## Declaration

**Signature:** Shaima Zaid Almotrad
**Date:** 10/11/2026
