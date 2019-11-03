# Search Algorithms in Java
#Introduction
Searching is one of the most common actions performed in regular business applications. This involves fetching some data stored in data structures like Arrays, List, Map, etc. More often than not, this search operation determines the responsiveness of the application for the end-user.

In this article, let's take a look at some of the searching strategies that can be used to cater to different scenarios. We will also implement them in Java and analyze their performance with some well-known parameters like Time and Space Complexity.


#Linear Search
Linear or Sequential Search is the simplest of search algorithms. While it most certainly is the simplest, it's most definitely not the most common, due to its inefficiency. It's a brute-force algorithm. Very rarely is it used in production, and in most cases, it's outperformed by other algorithms.

Linear Search has no pre-requisites for the state of the underlying data structure.

#Explanation
Linear Search involves sequential searching for an element in the given data structure until either the element is found or the end of the structure is reached.

If the element is found, we usually just return its position in the data structure. If not, we usually return -1.

#Implementation
Now let's see how to implement Linear Search in Java:

public static int linearSearch(int arr[], int elementToSearch) {

    for (int index = 0; index < arr.length; index++) {
        if (arr[index] == elementToSearch)
            return index;
    }
    return -1;
}
To test it, we'll use a simple Array of integers:

int index = linearSearch(new int[]{89, 57, 91, 47, 95, 3, 27, 22, 67, 99}, 67);
print(67, index);
With a simple helper method to print the result:

public static void print(int elementToSearch, int index) {
    if (index == -1){
        System.out.println(elementToSearch + " not found.");
    }
    else {
        System.out.println(elementToSearch + " found at index: " + index);
    }
}
Output:

67 found at index: 8
Time Complexity
Here we are iterating through the entire set of N elements sequentially to get the location of the element being searched. The worst case for this algorithm will be if the element we are searching for is the last element in the array.

In this case, we will iterate N times before we find the element.

Hence, the Time Complexity of Linear search is O(N).

Space Complexity
This type of search requires only a single unit of memory to store the element being searched. This is not relevant to the size of the input Array.

Hence, the Space Complexity of Linear Search is O(1).

#Applications
Linear Search can be used for searching in a small and unsorted set of data which is guaranteed not to increase in size by much.

It is a very basic search algorithm but due to its linear increase in time complexity, it does not find application in many production systems.


#Binary Search
Binary or Logarithmic Search is one of the most commonly used search algorithms primarily due to its quick search time.

#Explanation
This kind of search uses the Divide and Conquer methodology and requires the data set to be sorted beforehand.

It divides the input collection into equal halves, and with each iteration compares the goal element with the element in the middle.

If the element is found, the search ends. Else, we continue looking for the element by dividing and selecting the appropriate partition of the array, based on if the goal element is smaller or bigger than the middle element.

This is why it's important to have a sorted collection for Binary Search.

The search terminates when the firstIndex (our pointer) goes past lastIndex (last element), which implies we have searched the whole array and the element is not present.

There are two ways to implement this algorithm - iterative and recursive.

There shouldn't be a difference regarding time and space complexity between these two implementations, though this doesn't hold true to all languages.

#Implementation
#Iterative
Let's first take a look at the iterative approach:

public static int binarySearch(int arr[], int elementToSearch) {

    int firstIndex = 0;
    int lastIndex = arr.length - 1;

    // termination condition (element isn't present)
    while(firstIndex <= lastIndex) {
        int middleIndex = (firstIndex + lastIndex) / 2;
        // if the middle element is our goal element, return its index
        if (arr[middleIndex] == elementToSearch) {
            return middleIndex;
        }

        // if the middle element is smaller
        // point our index to the middle+1, taking the first half out of consideration
        else if (arr[middleIndex] < elementToSearch)
            firstIndex = middleIndex + 1;

        // if the middle element is bigger
        // point our index to the middle-1, taking the second half out of consideration
        else if (arr[middleIndex] > elementToSearch)
            lastIndex = middleIndex - 1;

    }
    return -1;
}
We can use the algorithm like this:

int index = binarySearch(new int[]{89, 57, 91, 47, 95, 3, 27, 22, 67, 99}, 67);
print(67, index);
Output:

67 found at index: 5
#Recursive
And now let's take a look at the recursive implementation:

public static int recursiveBinarySearch(int arr[], int firstElement, int lastElement, int elementToSearch) {

    // termination condition
    if (lastElement >= firstElement) {
        int mid = firstElement + (lastElement - firstElement) / 2;

        // if the middle element is our goal element, return its index
        if (arr[mid] == elementToSearch)
            return mid;

        // if the middle element is bigger than the goal element
        // recursively call the method with narrowed data
        if (arr[mid] > elementToSearch)
            return recursiveBinarySearch(arr, firstElement, mid - 1, elementToSearch);

        // else, recursively call the method with narrowed data
        return recursiveBinarySearch(arr, mid + 1, lastElement, elementToSearch);
    }

    return -1;
}
The difference in the recursive approach is that we invoke the method itself once we get the new partition. In the iterative approach, whenever we determined the new partition we modified the first and last elements and repeated the process in the same loop.

Another difference here is that recursive calls are pushed on the method call-stack and they occupy one unit of space per recursive call.

We can use this algorithm like this:

int index = binarySearch(new int[]{3, 22, 27, 47, 57, 67, 89, 91, 95, 99}, 0, 10, 67);
print(67, index);
Output:

67 found at index: 5
#Time Complexity
Since Binary Search divides the array into half each time its time complexity is O(log(N)). This time complexity is a marked improvement on the O(N) time complexity of Linear Search.

#Space Complexity
This search requires only one unit of space to store the element to be searched. Hence, its space complexity is O(1).

If Binary Search is implemented recursively, it needs to store the call to the method on a stack. This may require O(log(N)) space in the worst case scenario.

#Applications
It is the most commonly used search algorithm in most of the libraries for searching. The Binary Search tree is used by many data structures as well which store sorted data.

Binary Search is also implemented in Java APIs in the Arrays.binarySearch method.
