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
                                                            

    
    task4 :
    import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class CPUScheduler {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

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

    public ExpressionTree(String expression) {
        Stack<Node> stack = new Stack<>();
        for (int i = 0; i < expression.length(); i++) {
            char c = expression.charAt(i);
            if (c == '(') {
                continue;
            } else if (c == '+' || c == '-' || c == '*' || c == '/') {
                Node right = stack.pop();
                Node left = stack.pop();
                Node operator = new Node(c, left, right);
                stack.push(operator);
            } else if (Character.isDigit(c)) {
                int num = 0;
                while (i < expression.length() && Character.isDigit(expression.charAt(i))) {
                    num = num * 10 + expression.charAt(i) - '0';
                    i++;
                }
                i--;
                Node operand = new Node(num);
                stack.push(operand);
            }
        }
        root = stack.pop();
    }

    public void printInOrder() {
        printInOrder(root);
    }

    private void printInOrder(Node node) {
        if (node == null) {
            return;
        }
        printInOrder(node.getLeft());
        System.out.print(node.getValue() + " ");
        printInOrder(node.getRight());
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
        tree.printInOrder();
    }
}

                                                           
                                                           

task6 :
 import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

public class SpellChecker {
    private Set<String> lexicon;

    public SpellChecker(Set<String> lexicon) {
        this.lexicon = lexicon;
    }

    public List<String> check(String s) {
        List<String> results = new ArrayList<>();
        if (lexicon.contains(s)) {
            results.add(s);
        } else {
            for (String word : lexicon) {
                if (isSimilar(s, word)) {
                    results.add(word);
                }
            }
        }
        return results;
    }

    private boolean isSimilar(String s1, String s2) {
      
        return s1.length() == s2.length();
    }

    public static void main(String[] args) {
        Set<String> lexicon = new HashSet<>(Arrays.asList("hello", "world", "goodbye", "friend"));
        SpellChecker spellChecker = new SpellChecker(lexicon);

        String input = "helllo";
        List<String> suggestions = spellChecker.check(input);
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
        heapSort(arr);
        System.out.println("Sorted array: " + Arrays.toString(arr));
    }
    
    public static void heapSort(int[] arr) {
        int n = arr.length;
        
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(arr, n, i);
        
        for (int i = n - 1; i >= 0; i--) {
            
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
            
            heapify(arr, i, 0);
        }
    }
    
    public static void heapify(int[] arr, int n, int i) {
        int smallest = i;  
        int left = 2 * i + 1;
        int right = 2 * i + 2;
       
        if (left < n && arr[left] < arr[smallest])
            smallest = left;

        if (right < n && arr[right] < arr[smallest])
            smallest = right;
        
        if (smallest != i) {
            int temp = arr[i];
            arr[i] = arr[smallest];
            arr[smallest] = temp;
            
            heapify(arr, n, smallest);
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

                                                            
