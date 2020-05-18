![슬라이드1](https://user-images.githubusercontent.com/65477551/82135396-4a961c00-983d-11ea-93af-c4f6b1735d7f.PNG)


# MOC: Moving Object Coordinates
3차원 물체의 좌표 옮기기 플러그인

The MOC copies a three-dimensional coordinate group to another location coordinate.

![슬라이드2](https://user-images.githubusercontent.com/65477551/82135390-410cb400-983d-11ea-927c-bfef4269531e.PNG)

The MOC move a three-dimensional coordinate group to a specified coordinate, and adjust the degree of clump between each coordinate.

## Values

* gap >>> To adjust the spacing of coordinates.
* from_x1, from_y1, from_z1, to_x1, to_y1, to_z1 >>> starting coordinates
* move_x, move_y, move_z >>> values to move

![프레젠테이션2](https://user-images.githubusercontent.com/65477551/82137009-b339c480-984e-11ea-9420-3a1b9c26d3fd.png)

Assume that when coordinates from_x1, from_y1, to_x1, to_x1, to_y1 are passed, the size of the blocks in the room is all fixed at 1.
Move the coordinates by the value of move_x, move_y, and move_z. If the gap is "1", it retains its original size and if it is "2", the coordinates change by twice the interval.

## Develop
* Java
```java
package MovingObjectCoordinates;

import java.util.ArrayList;

public class MoveObject {
	//Array containing moved coordinate values
	private ArrayList<Coordinate> coordinates = new ArrayList<Coordinate>();
	//coordinates
	double from_x1, from_y1, from_z1;
	double to_x1, to_y1, to_z1;
	//values to move
	double move_x, move_y, move_z;
	//To adjust the spacing of coordinates.
	double gap;
	
	public MoveObject(
			double from_x1, double from_y1, double from_z1, 
			double to_x1, double to_y1, double to_z1,
			double move_x, double move_y, double move_z, 
			double gap
			) {
		super();
		this.from_x1 = from_x1;
		this.from_y1 = from_y1;
		this.from_z1 = from_z1;
		this.to_x1 = to_x1;
		this.to_y1 = to_y1;
		this.to_z1 = to_z1;
		this.move_x = move_x;
		this.move_y = move_y;
		this.move_z = move_z;
		this.gap = gap;
	}

	//Move Coordinate Values
	public void moving() {
		//Number of blocks in the original group
		double num_between_x = Math.abs(from_x1 - to_x1);
		double num_between_y = Math.abs(from_y1 - to_y1);
		double num_between_z = Math.abs(from_z1 - to_z1);
		
		//Debug
		//System.out.println("Number of blocks: " + num_between_x + ", " + num_between_y + ", " + num_between_z);
				
		//Center coordinates of the original group
		double center_x = from_x1 + (num_between_x / 2);
		double center_y = from_y1 + (num_between_y / 2);
		double center_z = from_z1 + (num_between_z / 2);
		
		//Debug
		//System.out.println("center conrdinates: " + center_x + ", " + center_y + ", " + center_z);
		
		//Start coordinates of the group to be moved
		double start_x = center_x + move_x - ((num_between_x * gap) / 2);
		double start_y = center_y + move_y - ((num_between_y * gap) / 2);
		double start_z = center_z + move_z - ((num_between_z * gap) / 2);
		
		//Debug
		//System.out.println("Start conrdinates: " + start_x + ", " + start_y + ", " + start_z);		
		
		for(int y = 0; y <= num_between_y; y++) {
			for(int z = 0; z <= num_between_z; z++) {
				for(int x = 0; x <= num_between_x; x++) {
					/*
					 * values to add, a = x, b = y, c = z
					 * Add a value in proportion to "gap".
					 */
					double a = start_x + (x * gap);
					double b = start_y + (y * gap);
					double c = start_z + (z * gap);
					
					//debug
					//System.out.println("abc: " + a + ", " + b + ", " + c);
					
					Coordinate coordinate = new Coordinate(a, b, c);
					coordinates.add(coordinate);
					
					//debug
					//System.out.println("coordinate: " + coordinate.getX() + ", " + coordinate.getY() + ", " + coordinate.getZ());
				}
			}
		}
	}
	
	/*
	 * Receive coordinate values as an array
	 */
	public ArrayList<Coordinate> getCoordinates() {
		return coordinates;
	}
	
	/*
	 * Print all index of array
	 */
	public void printCoordinates() {
		//Number of blocks in the original group
		double num_between_x = Math.abs(from_x1 - to_x1);
		double num_between_y = Math.abs(from_y1 - to_y1);
		double num_between_z = Math.abs(from_z1 - to_z1);
				
		int index = 0;
		
		for(int y = 0; y <= num_between_y; y++) {
			for(int z = 0; z <= num_between_z; z++) {
				for(int x = 0; x <= num_between_x; x++) {
					Coordinate coordinate = coordinates.get(index++);
					double a = coordinate.getX();
					double b = coordinate.getY();
					double c = coordinate.getZ();
					
					System.out.print(" {" + a + "/" + b + "/" + c + "} ");
				}
				System.out.println(" ");
			}
			System.out.println("-----------------------------------");
		}
	}
	
	/*
	 * Receive coordinate values through the Index Number
	 */
	public Double getValueX(int index) {
		return coordinates.get(index).getX();
	}
	public Double getValueY(int index) {
		return coordinates.get(index).getY();
	}
	public Double getValueZ(int index) {
		return coordinates.get(index).getZ();
	}
	
}

```
