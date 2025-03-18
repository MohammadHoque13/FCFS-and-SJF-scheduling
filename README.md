# FCFS-and-SJF-scheduling
import java.util.Arrays;
import java.util.Comparator;
import java.util.Scanner;

class Process {
    int id, burstTime, waitingTime, turnaroundTime;

  public Process(int id, int burstTime) {
        this.id = id;
        this.burstTime = burstTime;
    }
}

public class SchedulingAlgorithms {

  public static void computeFCFS(Process[] processes) {
        int n = processes.length;
        int totalWaitingTime = 0, totalTurnaroundTime = 0;

   processes[0].waitingTime = 0;
   processes[0].turnaroundTime = processes[0].burstTime;

  for (int i = 1; i < n; i++) {
            processes[i].waitingTime = processes[i - 1].waitingTime + processes[i - 1].burstTime;
            processes[i].turnaroundTime = processes[i].waitingTime + processes[i].burstTime;
        }

   System.out.println("\n----------------- FCFS -----------------");
   printResults(processes);
    }

  public static void computeSJF(Process[] processes) {
        int n = processes.length;
        Arrays.sort(processes, Comparator.comparingInt(p -> p.burstTime));

  processes[0].waitingTime = 0;
        processes[0].turnaroundTime = processes[0].burstTime;

  for (int i = 1; i < n; i++) {
            processes[i].waitingTime = processes[i - 1].waitingTime + processes[i - 1].burstTime;
            processes[i].turnaroundTime = processes[i].waitingTime + processes[i].burstTime;
        }

  System.out.println("\n----------------- SJF -----------------");
        printResults(processes);
    }

  public static void printResults(Process[] processes) {
        int totalWaitingTime = 0, totalTurnaroundTime = 0;
        System.out.println("Process ID | Waiting Time | Turnaround Time");

for (Process p : processes) {
            System.out.printf("    %d      |      %d       |       %d%n", p.id, p.waitingTime, p.turnaroundTime);
            totalWaitingTime += p.waitingTime;
            totalTurnaroundTime += p.turnaroundTime;
        }

  System.out.printf("\nAverage Waiting Time: %.2f\n", (double) totalWaitingTime / processes.length);
  System.out.printf("Average Turnaround Time: %.2f\n", (double) totalTurnaroundTime / processes.length);
    }

  public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter number of processes: ");
        int n = scanner.nextInt();
        Process[] processes = new Process[n];
        for (int i = 0; i < n; i++) {
            System.out.print("Enter burst time for Process " + (i + 1) + ": ");
            int burstTime = scanner.nextInt();
            processes[i] = new Process(i + 1, burstTime);
        }

   computeFCFS(processes.clone());
        computeSJF(processes.clone());
        
  scanner.close();
    }
}
