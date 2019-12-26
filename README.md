# Meeting Rooms II

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

```
Example

Example 1

Input: intervals = [(0,30),(5,10),(15,20)]
Output: 2
Explanation: We need two meeting rooms
room1: (0,30)
room2: (5,10),(15,20)

Example 2

Input: intervals = [(2,7)]
Output: 1
Explanation: Only need one meeting room
```

### Implementation

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.PriorityQueue;

class Interval {
	int start, end;

	Interval(int start, int end) {
		this.start = start;
		this.end = end;
	}
}

public class App {
     public static void main(String[] args) {
	  List<Interval> meetings = new ArrayList<Interval>();
	  meetings.add(new Interval(0, 30));
	  meetings.add(new Interval(5, 10));
	  meetings.add(new Interval(15, 20));
	  System.out.println(minMeetingRooms(meetings));
     }

     public static int minMeetingRooms(List<Interval> intervals) {
          if(intervals == null || intervals.size() == 0){
            return 0;
          }
	  Collections.sort(intervals, (a, b) -> a.start - b.start);
	  PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>();
		
	  for(Interval meeting : intervals){
		 if(!minHeap.isEmpty() && minHeap.peek() <= meeting.start){
		    minHeap.poll();
		  }
	      minHeap.add(meeting.end);
	  }
        
	return minHeap.size();
     }

}

```

The above implementation have runtime complexity of O(nlogn) and space complexity of O(n)

```
Runtime Complexity = O(nlogn)
Space Complexity   = O(n)
```

## References :
1. https://www.callicoder.com/java-priority-queue/

2. https://www.youtube.com/watch?v=RBlcUlUkDCU
