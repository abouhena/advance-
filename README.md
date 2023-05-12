# advance- 

Task1:


import java.util.*;

public class RemDuplicate {
    public static char[] remDuplicates(char[] array) {
        // Create a HashSet to store unique characters
        Set<Character> hashSet = new HashSet<>();

        // Create a new character array to store unique characters
        char[] n1Array = new char[array.length];
        int indexOfArray = 0;

        // Iterate over the input array
        for (char ff : array) {
            // Check if the character already exists in the HashSet
            if (!hashSet.contains(ff)) {
                // If not, add it to the HashSet and the new array
                hashSet.add(ff);
                n1Array[indexOfArray] = ff;
                indexOfArray++;
            }
        }

        // Return a new array containing only the unique characters
        return Arrays.copyOf(n1Array, indexOfArray);
    }

    public static void main(String[] args) {
        char[] printArray = { 'a', 'b', 'c', 'd', 'a', 'e', 'f', 'c', 'b', 'd', 'e', 'f' };
        System.out.println(Arrays.toString(remDuplicates(printArray)));
    }
}




    
    task2:
    
 
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr1 = { 2, 5, 7, 4, 3, 8 };
        int[] arr2 = { 7, 2, 5, 4, 8, 3 };
        
        if (hasSameElements(arr1, arr2)) {
            System.out.println("The arrays include the same set of elements.");
        } else {
            System.out.println("The arrays do not include the same set of elements.");
        }
    }
    
    public static boolean hasSameElements(int[] arrayOf1, int[] arrayOf2) {
        // Check if the arrays have the same length
        if (arrayOf1.length != arrayOf2.length) {
            return false;
        }
        
        // Sort the arrays
        Arrays.sort(arrayOf1);
        Arrays.sort(arrayOf2);
        
        // Check if the elements are the same
        for (int c = 0; c < arrayOf1.length; c++) {
            if (arrayOf1[c] != arrayOf2[c]) {
                return false;
            }
        }
        
        return true;
    }
}

                                                            
                                                            
                                                            
                                                            
                                       
                                                            
task3 :
                                                            

      public class TwoColourDoubleStack<ItemType> {
    private static final int DEFAULT_CAPACITY = 10;
    private int capacityOfArray;
    private int topInRed;
    private int topInBlue;
    private ItemType[] arrayS1;

    public TwoColourDoubleStack() {
        this(DEFAULT_CAPACITY);
    }

    public TwoColourDoubleStack(int desiredCap) {
        this.capacityOfArray = desiredCap;
        this.topInRed = -1;
        this.topInBlue = desiredCap;
        this.arrayS1 = (ItemType[]) new Object[desiredCap];
    }

    public void pushRed(ItemType element1) {
        if (isStacked()) {
            throw new IllegalStateException("Stack full");
        }
        arrayS1[++topInRed] = element1;
    }

    public void pushBlue(ItemType element1) {
        if (isStacked()) {
            throw new IllegalStateException("Stack full");
        }
        arrayS1[--topInBlue] = element1;
    }

    public ItemType popRed() {
        if (isRedVacant()) {
            throw new IllegalStateException("Red stack empty");
        }
        return arrayS1[topInRed--];
}

    public ItemType popBlue() {
        if (isBlueVacant()) {
            throw new IllegalStateException("Blue stack empty");
        }
        return arrayS1[topInBlue++];
    }

    public boolean isRedVacant() {
        return topInRed == -1;
    }

    public boolean isBlueVacant() {
        return topInBlue == capacityOfArray;
    }

    public boolean isStacked() {
        return topInRed + 1 == topInBlue;
    }

    public static void main(String[] args) {
        TwoColourDoubleStack<Integer> stack = new TwoColourDoubleStack<>(5);

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

    
                                                            

    
    task4 :
 
    
    
   import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class CPUScheduler {
    public static void main(String[] args) {
        Scanner insert = new Scanner(System.in);

        // Input for job 1
        System.out.println("Enter job 1 priority:");
        int job1Priority = sc.nextInt();
        System.out.println("Enter job 1 duration:");
        int job1Duration = sc.nextInt();

        // Input for job 2
        System.out.println("Enter job 2 priority:");
        int job2Priority = sc.nextInt();
        System.out.println("Enter job 2 duration:");
        int job2Duration = sc.nextInt();

        // Create the job list
        List<Job> jobs = new ArrayList<>();
        jobs.add(new Job("Job 1", job1Priority, job1Duration));
        jobs.add(new Job("Job 2", job2Priority, job2Duration));

        // Create the scheduler and schedule the jobs
        CPUScheduler scheduler = new CPUScheduler();
        List<String> schedule = scheduler.scheduleJobs(jobs);

        // Output the scheduling sequence
        for (int i = 0; i < schedule.size(); i++) {
            System.out.println("System time [" + i + "] - " + schedule.get(i));
        }

        sc.close();
    }
public List<String> scheduleJobs(List<Job> jobs) {
        List<String> schedule = new ArrayList<>();
        int timeSlice = 0;

        while (!jobs.isEmpty()) {
            Job jobToRun = getJobToRun(jobs);

            if (jobToRun != null) {
                schedule.add(jobToRun.getName() + " is running");
                jobToRun.decrementDuration();
                if (jobToRun.getDuration() == 0) {
                    jobs.remove(jobToRun);
                }
            } else {
                schedule.add("No job is running");
            }

            timeSlice++;
        }

        return schedule;
    }

    private Job getJobToRun(List<Job> jobs) {
        if (jobs.isEmpty()) {
            return null;
        }

        // First come first served
        Job jobToRun = jobs.get(0);

        // Highest priority
        for (Job job : jobs) {
            if (job.getPriority() > jobToRun.getPriority()) {
                jobToRun = job;
            }
        }
        // Shortest remaining time first
        for (Job job : jobs) {
            if (job.getDuration() < jobToRun.getDuration()) {
                jobToRun = job;
            }
        }

        return jobToRun;
    }

    private static class Job {
        private String name;
        private int priority;
        private int duration;

        public Job(String name, int priority, int duration) {
            this.name = name;
            this.priority = priority;
            this.duration = duration;
        }

        public String getName() {
            return name;
        }

        public int getPriority() {
            return priority;
        }

        public int getDuration() {
            return duration;
        }

        public void decrementDuration() {
            duration--;
        }
    }
}

 
    
    
                                                           
     task5:

  import java.util.Stack;

public class ExpressionTree {
    private Node root;

    public ExpressionTree(String arithmeticExp) {
        Stack<Node> stack = new Stack<>();
        for (int i = 0; i < arithmeticExp.length(); i++) {
            char c = arithmeticExp.charAt(i);
            if (c == '(') {
                continue;
            } else if (c == '+' || c == '-' || c == '*' || c == '/') {
                Node right = stack.pop();
                Node left = stack.pop();
                Node operator = new Node(c, left, right);
                stack.push(operator);
            } else if (Character.isDigit(c)) {
                int num = 0;
                while (i < arithmeticExp.length() && Character.isDigit(arithmeticExp.charAt(i))) {
                    num = num * 10 + arithmeticExp.charAt(i) - '0';
                    i++;
                }
                i--;
                Node operand = new Node(num);
                stack.push(operand);
            }
        }
        root = stack.pop();
    }

    public void printInSequence() {
        printInSequence(root);
    }

    private void printInSequence(Node node) {
        if (node == null) {
            return;
        }
        printInSequence(node.getLeft());
        System.out.print(node.getValue() + " ");
        printInSequence(node.getRight());
    }

    private static class Node {
        private char value;
        private int numValue;
        private Node left;
        private Node right;

        public Node(char value, Node left, Node right) {
            this.value = value;
            this.left = left;
            this.right = right;
        }

        public Node(int numValue) {
            this.numValue = numValue;
        }

        public char getValue() {
            return value;
        }

        public int getNumValue() {
            return numValue;
        }

        public Node getLeft() {
            return left;
        }

        public Node getRight() {
            return right;
        }
    }

    public static void main(String[] args) {
        ExpressionTree tree = new ExpressionTree("(5+3)*(8-2)");
        tree.printInSequence();
    }
}
 
                                                           
                                                           
                                                           

task6 :
    
import java.util.ArrayList;
import java.util.Arrays; 
import java.util.HashSet; 
import java.util.List; 
import java.util.Set;

public class SpellChecker { private Set lexicon;

public SpellChecker(Set<String> lexicon) {
    this.lexicon = lexicon;
}

public List<String> scan(String s) {
    List<String> results = new ArrayList<>();
    if (lexicon.contains(s)) {
        results.add(s);
    } else {
        for (String word : lexicon) {
            if (isEquivalent(s, word)) {
                results.add(word);
            }
        }
    }
    return results;
}

private boolean isEquivalent(String a1, String a2) {
  
    return a1.length() == a2.length();
}

public static void main(String[] args) {
    Set<String> lexicon = new HashSet<>(Arrays.asList("hello", "world", "goodbye", "friend"));
    SpellChecker spellChecker = new SpellChecker(lexicon);

    String input = "helllo";
    List<String> suggestions = spellChecker.scan(input);
    if (suggestions.isEmpty()) {
        System.out.println("'" + input + "' is a correct spelling");
    } else {
        System.out.println("'" + input + "' is not a correct spelling. Did you mean:");
        for (String suggestion : suggestions) {
            System.out.println("  - " + suggestion);
        }
    }
}
}

    
    
task 7 :
    
    
import java.util.*;

public class HeapSort {
    public static void main(String[] args) {
        int[] arr = { 12, 11, 13, 5, 6, 7 };
        System.out.println("Original array: " + Arrays.toString(arr));
        heapSorting(arr);
        System.out.println("Sorted array: " + Arrays.toString(arr));
    }
    
    public static void heapSorting(int[] array1) {
        int n = array1.length;
        
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(array1, n, i);
        
        for (int i = n - 1; i >= 0; i--) {
            
            int temp = array1[0];
            array1[0] = array1[i];
            array1[i] = temp;
            
            heapify(array1, i, 0);
        }
    }
    
    public static void heapify(int[] arr, int x, int y) {
        int smallest = y;  
        int leftChild = 2 * y + 1;
        int rightChild = 2 * y + 2;
       
        if (leftChild < x && arr[leftChild] < arr[smallest])
            smallest = leftChild;

        if (rightChild < x && arr[rightChild] < arr[smallest])
            smallest = rightChild;
if (smallest != y) {
            int temp = arr[y];
            arr[y] = arr[smallest];
            arr[smallest] = temp;
            
            heapify(arr, x, smallest);
        }
    }
}
    
    


 
    task 8:
    
   import java.util.*;

public class RoutingTableBuilder {

    public static void main(String[] args) {

        
        Map<String, List<String>> connectivity = new HashMap<>();
        connectivity.put("A", Arrays.asList("B", "C", "D"));
        connectivity.put("B", Arrays.asList("A", "C"));
        connectivity.put("C", Arrays.asList("A", "B", "D"));
        connectivity.put("D", Arrays.asList("A", "C"));

        
        Map<String, Map<String, String>> routingTables = new HashMap<>();
        for (String node : connectivity.keySet()) {
            Map<String, String> routingTable = buildRoutingTable(node, connectivity);
            routingTables.put(node, routingTable);
        }

        
        for (String node : routingTables.keySet()) {
            System.out.println("Routing table for node " + node + ":");
            for (String dest : routingTables.get(node).keySet()) {
                String nextHop = routingTables.get(node).get(dest);
                System.out.println("  - Destination: " + dest + ", Next hop: " + nextHop);
            }
            System.out.println();
        }
    }

    private static Map<String, String> buildRoutingTable(String source, Map<String, List<String>> connectivity) {
        Map<String, String> routingTable = new HashMap<>();
        Map<String, Integer> distances = new HashMap<>();
        Set<String> visited = new HashSet<>();

        for (String node : connectivity.keySet()) {
            distances.put(node, Integer.MAX_VALUE);
        }
        distances.put(source, 0);

        
        PriorityQueue<String> queue = new PriorityQueue<>(Comparator.comparingInt(distances::get));
        queue.offer(source);
        while (!queue.isEmpty()) {
            String node = queue.poll();
            visited.add(node);
            for (String neighbor : connectivity.get(node)) {
                if (!visited.contains(neighbor)) {
                    int newDist = distances.get(node) + 1;  
                    if (newDist < distances.get(neighbor)) {
                        distances.put(neighbor, newDist);
                        routingTable.put(neighbor, node); 
                        queue.offer(neighbor);
                    }
                }
            }
        }

        return routingTable;
    }
}
                       
