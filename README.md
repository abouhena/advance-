# advance- 

task1:
import java.util.*;

public class RemoveDuplicates {
    public static char[] removeDuplicates(char[] array) {
        // Create a HashSet to store unique characters
        Set<Character> hashSet = new HashSet<>();
        
        // Create a new character array to store unique characters
        char[] newArray = new char[array.length];
        int index = 0;
        
        // Iterate over the input array
        for (char ch : array) {
            // Check if the character already exists in the HashSet
            if (!hashSet.contains(ch)) {
                // If not, add it to the HashSet and the new array
                hashSet.add(ch);
                newArray[index] = ch;
                index++;
            }
        }
        
        // Return a new array containing only the unique characters
        return Arrays.copyOf(newArray, index);
    }
}

    
    task2:
    
    import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] array1 = { 2, 5, 7, 4, 3, 8 };
        int[] array2 = { 7, 2, 5, 4, 8, 3 };
        
        if (hasSameElements(array1, array2)) {
            System.out.println("The arrays have the same set of elements.");
        } else {
            System.out.println("The arrays do not have the same set of elements.");
        }
    }
    
    public static boolean hasSameElements(int[] array1, int[] array2) {
        // Check if the arrays have the same length
        if (array1.length != array2.length) {
            return false;
        }
        
        // Sort the arrays
        Arrays.sort(array1);
        Arrays.sort(array2);
        
        // Check if the elements are the same
        for (int i = 0; i < array1.length; i++) {
            if (array1[i] != array2[i]) {
                return false;
            }
        }
        
        return true;
    }
}
