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
                                                            
                                                            
                                                            
                                                            
                                       
                                                            
task3 :
public class TwoColorDoubleStack<ItemType> {
    private static final int DEFAULT_CAPACITY = 10;
    private int capacity;
    private int redTop;
    private int blueTop;
    private ItemType[] array;

    public TwoColorDoubleStack() {
        this(DEFAULT_CAPACITY);
    }

    public TwoColorDoubleStack(int capacity) {
        this.capacity = capacity;
        this.redTop = -1;
        this.blueTop = capacity;
        this.array = (ItemType[]) new Object[capacity];
    }

    public void pushRed(ItemType item) {
        if (isFull()) {
            throw new IllegalStateException("Stack is full");
        }
        array[++redTop] = item;
    }

    public void pushBlue(ItemType item) {
        if (isFull()) {
            throw new IllegalStateException("Stack is full");
        }
        array[--blueTop] = item;
    }

    public ItemType popRed() {
        if (isRedEmpty()) {
            throw new IllegalStateException("Red stack is empty");
        }
        return array[redTop--];
    }

    public ItemType popBlue() {
        if (isBlueEmpty()) {
            throw new IllegalStateException("Blue stack is empty");
        }
        return array[blueTop++];
    }

    public boolean isRedEmpty() {
        return redTop == -1;
    }

    public boolean isBlueEmpty() {
        return blueTop == capacity;
    }

    public boolean isFull() {
        return redTop + 1 == blueTop;
    }

    public static void main(String[] args) {
        TwoColorDoubleStack<Integer> stack = new TwoColorDoubleStack<>(5);

        stack.pushRed(1);
        stack.pushBlue(2);
        stack.pushRed(3);
        stack.pushBlue(4);

        System.out.println(stack.popRed());   
        System.out.println(stack.popBlue());  
        System.out.println(stack.popRed());   
        System.out.println(stack.popBlue());  

       
        stack.popRed();   
    }
}                                                           
                                                            
                                                            
                                                            
