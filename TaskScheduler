import java.util.ArrayList;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Queue;
import java.util.Timer;
import java.util.TimerTask;

public class TaskScheduler {

    private Map<Integer, List<Integer>> map;
    private List<Integer> res;

    public static void main(String[] args) {
        TaskScheduler taskScheduler = new TaskScheduler();

        int[][] tasks = null;
        taskScheduler.runTask(0, tasks, false);

        int[][] tasks1 = {};
        taskScheduler.runTask(1, tasks1, false);
        System.out.println("****************************");

        int[][] tasks2 = { null };
        taskScheduler.runTask(1, tasks2, false);
        System.out.println("****************************");

        int[][] tasks3 = { {} };
        taskScheduler.runTask(1, tasks3, false);
        System.out.println("****************************");

        int[][] tasks4 = { { 1, 0 } };
        taskScheduler.runTask(2, tasks4, false);  // should be 0, 1
        System.out.println("****************************");

        int[][] tasks5 = { { 1, 0 }, { 2, 0 }, { 3, 1 }, { 3, 2 } }; // should be 0, 1, 2, 3
        taskScheduler.runTask(4, tasks5, true);
    }

    private void runTask(int tasks, int[][] prerequisites, boolean recur) {

        if (prerequisites == null || prerequisites.length == 0 || prerequisites[0] == null
            || prerequisites[0].length == 0) {
            System.out.println("No runnable task found!");
            return;
        }

        try {
            List<Integer> runnableTaskOrder = findOrder(tasks, prerequisites);
            if (runnableTaskOrder.size() == 0) {
                System.out.println("No runnable task found!");
                return;
            }

            Timer t = new Timer();
            TimerTask tt = new TimerTask() {
                @Override
                public void run() {
                    for(int task : runnableTaskOrder) {
                        System.out.println(task);
                    }
                    if(!recur){
                        t.cancel();
                    }
                }
            };
            t.scheduleAtFixedRate(tt,500,1000);
        } catch(Exception ex) {
            ex.printStackTrace();
        }
    }

    private List<Integer> findOrder(int tasks, int[][] prerequisites) {
        map = new HashMap<>();
        res = new ArrayList<>();
        int[] inDegree = new int[tasks];

        for (int[] pr : prerequisites) {
            int pre = pr[1];
            int cur = pr[0];
            inDegree[cur]++;
            map.putIfAbsent(pre, new ArrayList<>());
            map.get(pre).add(cur);
        }

        Queue<Integer> que = new LinkedList<>();
        for (int i = 0; i < tasks; i++) {
            if (inDegree[i] == 0) {
                que.offer(i);
            }
        }

        while (!que.isEmpty()) {
            int cur = que.poll();
            res.add(cur);
            if (map.containsKey(cur)) {
                List<Integer> elems = map.get(cur);
                for (int e : elems) {
                    inDegree[e]--;
                    if (inDegree[e] == 0) {
                        que.offer(e);
                    }
                }
            }
        }

        if (res.size() != tasks) {
            return new ArrayList<>();
        }
        return res;
    }
}
