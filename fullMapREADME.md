# Final Project for NB Foundation class


## Getting Started
This program helps you find the route between two cities from the following list of following cities:

["Sandy", "Boring", "Gresham", "East Portland", "i5", "West Portland", "Sylvan", "Beaverton", "Tanasbourne", "Hillsboro", "North Plains", "Mountaindale"]
["Vancouver", "North Portland", "Hwy 26", "South Portland", "Tigard", "Lake Oswego", "Tualatin", "Stafford", "Wilsonville", "Aurora", "Hubbard", "Woodburn"]

### Pseudo code.
Our approach to this program is pretty straightforward. The search algorithm first looks for the origin.
Then it starts looking for the destination on the same branch where the origin is present. If it doesn't find it, it then looks for the junction node, then traverse through the other branch, with junction as the base.

```
typedef struct Location {
	char name[20];
	struct Location *east;
	struct Location *west;
	struct Location *north;
	struct Location *south;
}Location;
```

Search algorithm looking for the origin

```
for (int i = 0; i < 12; i++){
	if (strcmp(From, ewCities[i].name) == 0) {
		origin = &ewCities[i];
		isEWOrigin = 1;
		break;
	}
	if (strcmp(From, nsCities[i].name) == 0) {
		origin = &nsCities[i];
		isNSOrigin = 1;
		break;
	}
}
```

This section of code is looking for the destination on it's own branch

```
if (isEWOrigin == 1) {
	while (east == 0) {
		strcpy(route[e], currentNode->name);
		if (strcmp(currentNode->name, EWJunction->name) == 0) {
			isJuncationFound = 1;
			directionOfJunction = 'e';
		}
		totalCities += 1;
		if (strcmp(currentNode->name, To) == 0) {
			destinationFound = 1;
			break;
		}
		if (currentNode->east == NULL) {
			east = 1;
			//Given destinationFound is 0, if it's an end node, this resets the route list
			if (destinationFound == 0) {
				for (int a = 0; a < 23; a++) {
					for (int b = 0; b < 15; b++) {
						route[a][b] = '\0';
					}
				}
			}
			currentNode = origin;
			totalCities = 0;
			e = 0;
			break;
		}
		currentNode = currentNode->east;
		e += 1;
	}
	while (west == 0 && destinationFound == 0) {
		strcpy(route[w], currentNode->name);
		if (strcmp(currentNode->name, EWJunction->name) == 0) {
			isJuncationFound = 1;
			directionOfJunction = 'w';
		}
		totalCities += 1;
		if (strcmp(currentNode->name, To) == 0) {
			destinationFound = 1;
			break;
		}
		if (currentNode->west == NULL) {
			west = 1;
			//Given destinationFound is 0, if it's an end node, this resets the route list
			if (destinationFound == 0) {
				for (int a = 0; a < 23; a++) {
					for (int b = 0; b < 15; b++) {
						route[a][b] = '\0';
					}
				}
			}
			currentNode = origin;
			totalCities = 0;
			isJuncationFound = 0;
			w = 0;
			break;
		}
		currentNode = currentNode->west;
		w += 1;
		}
```

### Working with the code

The program runs on a case-sensitive code. So please input the names of cities according to the list provided above.


```
Hello!, please enter the origin:  Sandy

Please enter the destination:  South Portland

Here is the route from Sandy to South Portland
Sandy	Boring	Gresham	East Portland	i5	South Portland	
```

### Tests
```
```

## License

This project is licensed under the MIT License

## Acknowledgments

* Inspiration
