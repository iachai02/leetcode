# 238. Product of Array Except Self

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`. The product of any prefix or suffix of `nums` is guaranteed to fit in a 32-bit integer. You much write an algorithm that runs in `O(n)` time and without using the division operation. 

- solution: 
    - multiply the values to the left of a number and to the right of a number and then multiply those two solutions together. 
    - We can do this by having a prefix array and a postfix array which would contain the values of the numbers multiplied before and after each indicated number in the list
    - iterate through the `nums` list and get value of the prefix at index - 1 and the value of the postfix at index + 1 and multiply them together and add to a result array
    - If there is no prefix or postfix, assume 1
    - this solution uses more memory, but still works

- solution using less memory: 
    - use a pass going from beginning to the end of the list and add the prefix multiplication values to the output at one index to the right
    - use a pass going from the end of the list to the beginning and now you multiply that value with the prefix value which is at one index to the left to get the final result for each number

    ```python
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = [1] * (len(nums))

        # fills the res array with the product of all the elements to the left of the current element in the nums array
        for i in range(1, len(nums)):

            res[i] = res[i - 1] * nums[i - 1]

        # keeps track of the product of elements to the right of the current element
        postfix = 1

        # goes through the nums array in reverse order
        for i in range(len(nums) - 1, -1, -1):
            # adds the final product of both prefix and postfix values to res
            res[i] *= postfix

            # update postfix to include the current element in nums
            postfix *= nums[i]
        return res
    ```
    - Time: `O(n)`
    - Space: `O(1)`

    ## Example

    1. `nums = [1, 2, 3, 4]`
    2. `res = [1, 1, 1, 1]`
    3. `res[1] = res[1-1] * nums[1-1] = res[0] * nums[0] = 1 * 1 = 1`
    4. `res[2] = res[2-1] * nums[2-1] = res[1] * nums[1] = 1 * 2 = 2`
    5. `res[3] = res[3-1] * nums[3-1] = res[2] * nums[2] = 2 * 3 = 6`
    6. `res = [1, 1, 2, 6]`
    7. go through the nums array in reverse order
    8. `res[3] = res[3] * 1 = 6`, `postfix = 1 * 4 = 4`
    9. `res[2] = res[2] * 4 = 2 * 4 = 8`, `postfix = 4 * 3 = 12`
    10. `res[1] = res[1] * 12 = 1 * 12 = 12`, `postfix = 12 * 2 = 24`
    11. `res[0] = res[0] * 24 = 1 * 24 = 24`, `postfix = 24 * 1 = 24`
    12. return `res = [24, 12, 8, 6]` 