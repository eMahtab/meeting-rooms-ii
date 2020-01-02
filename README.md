# Meeting Rooms II
## https://www.lintcode.com/problem/meeting-rooms-ii
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

## Approach :
Say you are an event organizer and you are organizing a tech event, which involves 4 different training sessions on a single day (e.g. one for Developers, one for DevOps folks, one for Security folks and one for DBAs) and out of these 4 sessions some of them will be held in parallel which means different training sessions running at the same time. 

As an organizer you got the timings for each session : `[2, 4] [1,7] [7, 8] [3, 5]`, e.g. 2 to 4 is Developers session, 1 to 7 is for DevOps folks and so on, now at **minimum** how many training rooms will you require to organize all the sessions? knowing that at anytime there can only be one training going on in one training room, but if a training room is free (means the next training session starts after the end of, one of the previous training session) then we can reuse the same training room.

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
