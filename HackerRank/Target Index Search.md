# Solution

C#

```csharp
    // first version
    public static int binarySearch(List<int> nums, int target)
    {
        var lowIndex = 0;
        var highIndex = nums.Count - 1;
        var result = -1;

        if(nums.Count == 0)
            return result;

        // lowIndex > highIndex then Stop
        while(lowIndex <= highIndex){
            // aviod int overflow
            var midIndex = lowIndex+(highIndex - lowIndex)/2;

            if(target < nums[midIndex] && target > nums[lowIndex])
            {
                highIndex = midIndex -1;
                lowIndex +=1;
                continue;
            }

            if(target > nums[midIndex] && target < nums[highIndex])
            {
                lowIndex = midIndex +1;
                highIndex -=1;
                continue;
            }

            switch (target)
            {
                case var value when value == nums[highIndex]:
                    result = highIndex;
                    break;
                case var value when value == nums[midIndex]:
                    result = midIndex;
                    break;
                case var value when value == nums[lowIndex]:
                    result = lowIndex;
                    break;
                default:
                    break;
            }
            break;
        }

        return result;
    }

    // second version
    public static int binarySearch(List<int> nums, int target)
    {
        var lowIndex = 0;
        var highIndex = nums.Count - 1;
        var result = -1;

        if(nums.Count == 0)
            return result;

        // lowIndex > highIndex then Stop
        while(lowIndex <= highIndex){
            // avoid int overflow
            var midIndex = lowIndex+(highIndex - lowIndex)/2;

            if(target < nums[midIndex])
            {
                highIndex = midIndex -1;
                continue;
            }

            if(target > nums[midIndex])
            {
                lowIndex = midIndex +1;
                continue;
            }

            switch (target)
            {
                case var value when value == nums[highIndex]:
                    result = highIndex;
                    break;

                case var value when value == nums[midIndex]:
                    result = midIndex;
                    break;

                case var value when value == nums[lowIndex]:
                    result = lowIndex;
                    break;
                default:
                    break;
            }
            break;
        }

        return result;
    }
```
