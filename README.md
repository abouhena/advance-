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
