# Done
[Leetcode Link](https://leetcode.com/problems/employee-free-time/)

---
Problem Explanation:

Given a list of employee work schedules with each employee having a list of non-overlapping intervals representing their working hours, we are tasked with finding the common free time for all employees, or in other words, the times when all employees are not working.

The input is a nested list of intervals, each interval as `[start, end]`, with `start < end`. The intervals are non-overlapping and are already sorted in ascending order. The output should also be a list of sorted intervals.

For example, consider `schedule = [[[1,3],[6,7]],[[2,4]],[[2,5],[9,12]]]`. Here, Employee 1 works from 1 to 3 and 6 to 7. Employee 2 works from 2 to 4 and Employee 3 works from 2 to 5 and 9 to 12. The common free time for all employees is `[5,6]` and `[7,9]` as these are the intervals when all employees are free.

Solution Approach:

The proposed solution concatenates all work schedules into a single list, sorts this list and then identifies the gaps between work intervals, which represent the common free time for all employees.

First, the solution creates an empty array to store the result. Then, it goes through the work shifts of each employee and combines all the intervals to a single list.

Next, this combined list of work intervals is sorted using the start of the work intervals. This will ensure that the work schedules are in chronological order.

After that, the solution stores the end time of the first shift in a variable called `prevEnd`, and then iterates through each work interval.

If the start of a work interval is greater than `prevEnd`, this means there's a gap between the end of the previous work shift and the start of the current work shift. This gap represents a common free time, which is then added to the result list.

Finally, `prevEnd` is updated with the maximum end time of the current work interval or the `prevEnd`.

Through this approach, the algorithm successfully identifies the common free time of all employees.

