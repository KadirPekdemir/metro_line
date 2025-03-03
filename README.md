# Metro System Path Finder

This C program simulates a metro system, allowing users to find the shortest path between two stations. The program works by calculating distances based on the coordinates of the stations and providing the user with the nearest stations based on their current location. It uses a simple representation of a metro system consisting of metro lines and stations.

### Problem Explanation:
The program simulates a metro system in a city. Each metro line consists of multiple stations, and each station is defined by its name and coordinates (x, y). The goal of the program is to find the shortest path between two stations, considering the metro lines and their stations. It calculates the nearest station from the user’s current location and the target location, then calculates the best path based on the metro network.

### How the Program Works:
1. **Input:**
   - The program starts with predefined metro lines, each containing a set of stations with their respective coordinates.
   - The user provides the starting coordinates (`myX`, `myY`) and the goal coordinates (`goalX`, `goalY`) for the location and target station.
   
2. **Nearest Station Calculation:**
   - The program finds the nearest station to both the user's current location and the target location, based on the Euclidean distance between points.

3. **Path Calculation:**
   - The program calculates the shortest path between the nearest stations of the user’s location and the target station (though this part is not yet fully implemented).

4. **Output:**
   - The program outputs the nearest stations to the user and the target location, and indicates whether the user can walk instead of using the metro.
   - If the stations are the same, the program will inform the user that it’s better to walk.
   - If a valid path is found, it will show the path (although this part is incomplete in the code provided).

### Example:

**Input:**
- User’s current location: `(1, 2)`
- Target location: `(62, 45)`

**Output:**
- The best path from Haydarpasa to Icmeler is: There is no path on the metro!


### Code Explanation:
1. **Structures:**
   - `MetroStation`: Represents a metro station with a name and coordinates (`x`, `y`).
   - `MetroLine`: Represents a metro line with a color and an array of `MetroStation` objects.
   - `MetroSystem`: Represents the metro system with a name and an array of `MetroLine` objects.

2. **Functions:**
   - `addStation`: Adds a station to a metro line.
   - `addLine`: Adds a metro line to the metro system.
   - `equals`: Checks if two stations are the same.
   - `getDistanceTravelled`: Calculates the total distance travelled by a path of stations.
   - `findNearestStation`: Finds the nearest station to a given coordinate.
   - `getNeighboringStations`: Retrieves the neighboring stations of a given station.
   - `findPath`: (commented out) intended to calculate the shortest path between two stations.
   
3. **Metro System Setup:**
   - The program sets up 3 metro lines (`red`, `blue`, and `green`) and defines 9 metro stations. These lines and stations are added to the `MetroSystem` object representing the Istanbul metro system.
   
4. **Path Finding Logic:**
   - The program computes the nearest stations to the user's location and the goal location.
   - It is set up to find the best path but the actual pathfinding logic (e.g., using Dijkstra’s algorithm or another approach) is incomplete in the provided code.

### How to Run:
1. Save the code in a file named `metro_system.c`.
2. Open a terminal and navigate to the directory containing the file.
3. Compile the program using a C compiler:
   ```bash
   gcc metro_system.c -o metro_system -lm
