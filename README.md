# Coding_asses
package coding_assignment;

public class Main {
	 public static void main(String[] args) {

		 int initialCapacity = 3;
	        RecentlyPlayedSongs store = new RecentlyPlayedSongs(initialCapacity);
	        
	        store.playSong("user1", "S1");
	        store.playSong("user1", "S2");
	        store.playSong("user1", "S3");
	        store.printRecentlyPlayedSongs("user1"); // Output: S3,S2,S1
	        
	        store.playSong("user1", "S4");
	        store.printRecentlyPlayedSongs("user1"); // Output: S4,S3,S2

	        store.playSong("user1", "S2");
	        store.printRecentlyPlayedSongs("user1"); // Output: S2,S4,S3
	        
	        store.playSong("user1", "S1");
	        store.printRecentlyPlayedSongs("user1"); // Output: S1,S2,S4
	}

}

package coding_assignment;

import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.Map;

public class RecentlyPlayedSongs {
	private final int capacity;
    private final Map<String, LinkedList<String>> userSongsMap;

    public RecentlyPlayedSongs(int capacity) {
        this.capacity = capacity;
        this.userSongsMap = new LinkedHashMap<>();
    }

    public void playSong(String user, String song) {
        if (!userSongsMap.containsKey(user)) {
            userSongsMap.put(user, new LinkedList<>());
        } else {
            LinkedList<String> songsList = userSongsMap.get(user);
            songsList.remove(song); // Remove the song if it already exists to add it to the front later
        }

        LinkedList<String> songsList = userSongsMap.get(user);
        songsList.addFirst(song);

        if (songsList.size() > capacity) {
            songsList.removeLast(); // Remove the least recently played song
        }
    }

    public LinkedList<String> getRecentlyPlayedSongs(String user) {
        return userSongsMap.getOrDefault(user, new LinkedList<>());
    }

    public void printRecentlyPlayedSongs(String user) {
        LinkedList<String> songsList = getRecentlyPlayedSongs(user);
        System.out.println(String.join(",", songsList));
    }
}

